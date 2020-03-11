---

copyright:
  years: 2015, 2020
lastupdated: "2020-03-011"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka, replication, failover, scenario, disaster recovery, mirroring

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}
{:deprecated: .deprecated}
{:important: .important}

# Event Streams mirroring 
{: #replication}

Mirroring enables messages in one service instance to be copied continually to a second instance, allowing disaster recovery scenarios to be implemented easily. This improves resilience because if a service instance becomes unavailable, applications can, without change, simply reconnect to the second instance and continue their normal operation, using the same credentials, authorizations, and topic definitions. This is provided as a fully managed capability.
{:shortdesc}

Currently mirroring is in early access status. This means that a limited function version is being made available to a small group of users for the purpose of gathering feedback, and rapidly iterating on the design. This feature is only available for service instances using the Enterprise plan.

Current features are:
- Mirror topics and consumer groups between two Event Streams service instances
- SLA of 99.99% availability, consistent with that of the Event Streams service
- Monitoring via IBM Cloud™ Monitoring with Sysdig

Current limitations are:
- All topics and groups are mirrored
- Enablement and disablement is via a support ticket
- Unidirectional

Before starting:
- For seamless switchover, applications are recommended to follow the coding guidelines as outlined below.
- The network bandwidth used by mirroring must be taken in to account during capacity planning. For example, if 10 MB/s of message traffic is being produced by applications into the source service instance, then an additional 10 MB/s of outgoing bandwidth will be required to mirror these messages into the target instance. This must be allowed for alongside any existing outgoing bandwidth already being consumed by applications. The monitoring dashboards can be used to determine the network usage in a service instance, see https://cloud.ibm.com/docs/services/EventStreams?topic=eventstreams-metrics

To enable mirroring, see Mirroring Setup Guide.

## Mirroring overview
{: #mirroring_overview}

Mirroring happens between two clusters and is unidirectional, meaning data will be mirrored in one direction from a single source cluster to a single target cluster. In this document, the source cluster will be named `A` and the target cluster will be named `B`. Note that these cluster aliases are configurable when enabling mirroring, so for example they could be "us-south" and "us-east".

A topic called `mytopic` from the source cluster (A) will appear on the target cluster (B) as `mytopic.A` indicating it originates from `A`. Such topics are called "remote topics", in that they originate from the remote cluster. In contrast, any topics directly created on a cluster by users are called "local topics".

To allow consumer groups to switch between clusters, special topics are used to mirror consumer group offsets. These topics are named `<ALIAS>.checkpoints.internal`, where `<ALIAS>` is the alias of the remote cluster. For example `us-east.checkpoints.internal`. Consumers will need to access these topics to seamlessly switch between clusters.

Finally, because of the naming of remote topics, we recommend avoiding using cluster aliases as part of the Kafka resource names.

## IAM access policies for mirroring
{: #iam_mirroring}

Because applications will need access to the source and destination clusters, IAM access policies will need to be set up on both clusters and use the API key from the service ID that the policies are attached to.  We can take advantage of the IAM wildcarding features https://cloud.ibm.com/docs/iam?topic=iam-wildcard to simplify the access policies that control access to the mirrored resources.

If you are new to IAM access policies, see the IAM documentation https://cloud.ibm.com/docs/iam?topic=iam-getstarted and the Event Streams access control documentation https://cloud.ibm.com/docs/EventStreams?topic=eventstreams-security for more details before reading further.

Define the following IAM access policies on **both** clusters:

| Resource type | Resource ID| Role|
|----------|---------|---------|
|cluster     |  |Reader |
|group     | <RESOURCE_NAME>.* |As required by the application |
|topic     | <RESOURCE_NAME>.* |As required by the application |
|txnid     | <RESOURCE_NAME>.* |As required by the application |
|topic     | <ALIAS>.checkpoints.internal | Reader |

where <ALIAS> is the alias for other cluster. For example, on cluster B, the Resource ID should be `A.checkpoints.internal`.

Fine-grained access policies should be granted to individual applications. For example, applications simply consuming should only have Reader access policies.

## Considerations when sharing clusters between multiple entities
{: #sharing_clusters}

When multiple entities, such as different business units, are sharing an instance and require isolation from each other, it is recommended that you follow naming guidelines to simplify the management and operation of mirrored clusters.

We recommend naming Kafka resources using the following template:
<ENTITY_PREFIX><SEPARATOR><NAME>

Where:
<ENTITY_PREFIX> is the prefix for the entity using this topic
<SEPARATOR> is an optional character used to easily separate the entities and resource names
<NAME> is the name of the Kafka resource

For example, if the accounting business unit requires a topic called invoices, it could be called `accounting.invoices`.

The required access policies will need to be adjusted. For example, for the accounting business unit, the following policies are required on cluster B:

| Resource type | Resource ID| Role|
|----------|---------|---------|
|cluster     |  |Reader |
|group     | accounting.* |As required by the application |
|topic     | accounting.* |As required by the application |
|txnid     | accounting.* |As required by the application |
|topic - (NB - Specific to the checkpoint topic)    | A.checkpoints.internal | Reader |

Cluster A should have the same access policies apart from the last one which should be on B.checkpoints.internal.

## Building mirroring aware applications 
{: #building_apps}

### Producers
We recommend producers to only produce to local topics, hence they should not require changes when switching between clusters.

### Consumers
Consumers should subscribe and consume to both the local and remote topics. This can be done with one wild-carded subscription, that is to consume from both  `accounting.invoice` and `accounting.invoice.<ALIAS>` use the subscription to `accounting.invoice.*`.

When consuming both local and remote topics, care should be taken if the application requires strict ordering. In such a case, remote topics should be fully consumed first before starting to consume from local topics. This way messages are processed in the order they were produced.

### Consumer offsets
Note that while consumer groups offsets are replicated between clusters, they must be explicitly used by consumers in order to reset their position when switching cluster.

The RemoteClusterUtils package allows to easily make these changes. Such logic is demonstrated in https://github.ibm.com/messagehub/event-streams-samples/blob/mm2/kafka-java-console-sample/src/main/java/com/eventstreams/samples/ConsumerRunnable.java#L68-L119

## Monitoring mirroring
{: #monitoring}

Mirroring can be monitored using IBM Cloud™ Monitoring with Sysdig. To enable Monitoring, see https://cloud.ibm.com/docs/services/EventStreams?topic=eventstreams-metrics. The Monitoring dashboard is available on the target cluster.

The Event Streams Mirroring dashboard exposes the following metrics:
- Mirroring throughput: the bytes per second of mirroring throughput from the source Event Streams instance. This is useful to see if mirroring is active and for capacity planning.
- Mirroring latency: the 95% quantile of mirroring latency in second from the source Event Streams instance. For example, if this is 1 second, it means 95% of the partitions being mirrored are less than 1 second behind the source cluster. This is useful to determine how far behind the target cluster is.

Data produced within the latency window might not be present on the target cluster yet and still might be lost if a disaster happens on the source cluster. However if mirroring is up to date, failing over while both clusters stay healthy can be achieved without any data loss.

## Understanding Recovery Objectives with mirroring

In a data protection plan such as mirroring, Recovery Point Objective (RPO) and Recovery Time Objective (RTO) are key parameters. You must understand the decisions associated with these objectives.

The Recovery Point Objective can be monitored using the mirroring latency metric provided in the Mirroring dashboard. This metric shows the lag between both clusters and allows to estimate the amount of data loss in the event of a disaster. You are responsible for monitoring that value and ensuring it fits in your RPO.

The Recovery Time Objective is fully controlled by users and is made of the following timing windows:
- the time it takes the user to decide to fail over
- the time it takes the user to fail over their applications

### Testing
We recommend you testing failing over and back when you have made your applications mirroring aware. You can follow the steps outlined in the Disaster Recovery Example Scenario and use the Monitoring dashboards to ensure all steps complete as expected.



