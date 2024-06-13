---

copyright:
  years: 2015, 2023
lastupdated: "2023-12-19"

keywords: replication, failover, scenario, disaster recovery, mirroring

subcollection: EventStreams

---

{{site.data.keyword.attribute-definition-list}}

# Using mirroring 
{: #mirroring}

Mirroring enables messages in one service instance to be copied continually to a second instance, allowing disaster recovery scenarios to be implemented easily. This feature improves resilience because if a service instance becomes unavailable, applications can, without change, reconnect to the second instance and continue their normal operation, by using the same credentials, authorizations, and topic definitions. This feature is provided as a fully managed capability.
{: shortdesc}

This feature is only available for service instances that use the Enterprise plan.

The current features are:

- Mirror topics and consumer groups between two {{site.data.keyword.messagehub}} service instances.
- SLA of 99.99% availability, consistent with the {{site.data.keyword.messagehub}} service.
- Monitoring by using {{site.data.keyword.mon_full}}.

The current limitations are:

- Unidirectional.

Before you start mirroring, consider the following points:
- For seamless switchover, applications are to follow the coding guidelines.
- [Capacity planning](#capacity_planning)

To enable mirroring, see [Mirroring setup guide](/docs/EventStreams?topic=EventStreams-mirroring_setup).

## Mirroring overview
{: #mirroring_overview}

Mirroring of selected topics happens between two clusters and is unidirectional, meaning data is mirrored in one direction from a single source cluster to a single target cluster. Each cluster has a mirroring alias. In this document, `A` is used for the source cluster alias and `B` for the target cluster alias. The aliases are configurable when mirroring is enabled, so for example, they could be "us-south" and "us-east".

A topic called `mytopic` from the source cluster (A) appears on the target cluster (B) as `mytopic.A` indicating it originates from `A`. This type of topic is called a _remote topic_ because it originates from the remote (source) cluster. In contrast, any topics that are directly created on the target cluster by users are called _local topics_.

To select which topics are mirrored, a regular expression pattern can be configured by using [Mirroring User Controls](/docs/EventStreams?topic=EventStreams-mirroring#user_controls).

To allow consumer groups to switch between clusters, special topics are used to mirror consumer group offsets. These topics are named `A.checkpoints.internal`, where `A` is the alias of the source cluster. For example, `us-east.checkpoints.internal`. Consumers need to access these topics to seamlessly switch between clusters.

Finally, because of the naming of remote topics, avoid using cluster aliases as part of the Kafka resource names.

## Capacity planning
{: #capacity_planning}

Both the network usage and geographical location of the source and target service instances must be considered when you plan capacity.

### Network bandwidth
{: #network_bandwidth}

The network bandwidth needed to mirror the selected topics must be considered in the bandwidth allowance of both the source and target service instances. For example, if 10 MB/s of message traffic is produced by applications in the source service instance to the mirrored topics, an extra 10 MB/s of outgoing bandwidth is required to mirror these messages into the target instance. This must be allowed for alongside any existing outgoing bandwidth that is already used by consuming applications. The monitoring dashboards can be used to determine the network usage in a service instance. For more information, see [Monitoring {{site.data.keyword.messagehub}} metrics](/docs/EventStreams?topic=EventStreams-metrics).

### Geographical location
{: #geographical_location}

As with any networking, the maximum achievable throughput is a factor of the distance over which the data is transmitted (due to the increasing latency and packet loss). This affects the maximum throughput that can be achieved between the source and target instances. Place the target service instances in as geographically close location as possible to the source.

The following table provides guidance for the achievable throughputs:

| Regions | Max per-partition throughput | Max total throughput |
| ------- |:------:|:------:|
| us-south <-> us-east | 1.5 MB/s | 35 MB/s |
| eu-gb <-> eu-de | 2.5 MB/s | 35 MB/s |
| au-syd <-> jp-tok | 0.4 MB/s| 12 MB/s|
| within same region eu-gb <-> eu-gb | 2.5 MB/s| 35 MB/s|
{: caption="Table 1. Throughput guidance" caption-side="bottom"}

The numbers indicate:
- **Max total throughput**: The maximum total MB/s that can be mirrored across all selected topics. 
- **Max per-partition throughput**: The maximum MB/s that can be mirrored within a single partition. Select the number of partitions that are configured for the source topics to ensure the per partition load remains within this limit.

Exceeding the limits results in an increasing lag between the data in the source and target instances. Having a large data lag can result in significant data loss. The monitoring dashboards can be used to determine the latency for each topic. For more information, see [Monitoring mirroring](#monitoring_mirroring).

### Deleting redundant target topics
{: #delete_redundant}

To avoid accidental deletion of data in the target instance, topics are not automatically deleted from the target instance when they are deleted from the source. It is the user's responsibility to delete the topics on the target instance. If mirrored topics are frequently deleted and created, more disk and partition allowance can be consumed in the target cluster. The usage can be monitored with the monitoring dashboard in the target cluster, see [Monitoring {{site.data.keyword.messagehub}} metrics](/docs/EventStreams?topic=EventStreams-metrics). You can delete topics that are no longer required by using the CLI, UI, or admin interfaces.

## IAM access policies for mirroring
{: #iam_mirroring}

Because applications need access to the source and destination clusters, IAM access policies must be set up on both clusters, and use the API key from the service ID that the policies are attached to. We can use the IAM wildcarding features [Assigning access by using wildcard policies](/docs/account?topic=account-wildcard) to simplify the access policies that control access to the mirrored resources.

If you are new to IAM access policies, see [How IBM Cloud IAM works](/docs/account?topic=account-iamoverview) and [Managing authentication to your {{site.data.keyword.messagehub}} instances](/docs/EventStreams?topic=EventStreams-security) for more details.

Define the following IAM access policies on **both** clusters, where &lt;ALIAS&gt; is the alias for the other cluster. For example, on cluster B, the resource ID is `A.checkpoints.internal`.

| Resource type | Resource ID| Role|
|----------|---------|---------|
|cluster     |  |Reader |
|group     | &lt;RESOURCE_NAME&gt;.* |As required by the application |
|topic     | &lt;RESOURCE_NAME&gt;.* |As required by the application |
|txnid     | &lt;RESOURCE_NAME&gt;.* |As required by the application |
|topic (specific to the checkpoint topic)    | &lt;ALIAS&gt;.checkpoints.internal | Reader |
{: caption="Table 2. Access policies" caption-side="bottom"}

Grant fine-grained access policies to individual applications. For example, for applications simply consuming grant only Reader access.

For mirroring user controls, you must have the following permissions on the target cluster.

| Resource type | Resource ID| Role|
|----------|---------|---------|
|cluster |  |Manager |
{: caption="Table 3. Target cluster permissions" caption-side="bottom"}

## Considerations when you share clusters between multiple entities
{: #sharing_clusters}

When multiple entities, such as different business units, are sharing an instance and require isolation from each other, follow naming guidelines to simplify the management and operation of mirrored clusters.

Name Kafka resources by using the following template:
&lt;ENTITY_PREFIX&gt;&lt;SEPARATOR&gt;&lt;NAME&gt;

Where:
- &lt;ENTITY_PREFIX&gt; is the prefix for the entity that uses this topic.
- &lt;SEPARATOR&gt; is an optional character that is used to easily separate the entities and resource names.
- &lt;NAME&gt; is the name of the Kafka resource.

For example, if the accounting business unit requires a topic that is called invoices, you can call it `accounting.invoices`.

The required access policies must be adjusted. For example, for the accounting business unit, the following policies are required on cluster B:

| Resource type | Resource ID| Role|
|----------|---------|---------|
|cluster     |  |Reader |
|group     | accounting.* |As required by the application |
|topic     | accounting.* |As required by the application |
|txnid     | accounting.* |As required by the application |
|topic (note, this is specific to the checkpoint topic)    | A.checkpoints.internal | Reader |
{: caption="Table 4. Access policies needed on cluster B" caption-side="bottom"}

Cluster A must have the same access policies apart from the last one that must be on `B.checkpoints.internal`.

## Mirroring user controls
{: #user_controls}

You can configure mirroring by using the [CLI](/docs/EventStreams?topic=EventStreams-cli) or [Administration REST API](/docs/EventStreams?topic=EventStreams-admin_api). All mirroring user controls are performed on the target cluster.

### Setting the topic selection
{: #setting_topic_selection}

The mirroring selection is made based on the topic names on the source cluster by using regular expression (regex) patterns. Choose the names of the topics on your source cluster carefully, by considering the advice from the [Considerations when you share clusters between multiple entities](#sharing_clusters) section.

With well-structured topic names, such as adding a prefix to topics that are part of the same group or application, it is easy to control mirroring. With such a naming convention in place, any future topics that match the pattern are automatically mirrored without the need for more changes.

The topic selection is given in the form of a list of one or more regex patterns. A topic is selected if it matches any of the patterns in the list.

Some examples of patterns to select topics for mirroring:

Example Patterns | Explanation
------------ | -------------
`^topic1$` | Full topic names. \n This matches only the single topic named `topic1`.
`^topic1$,^topic2$` | List of patterns matching full topic names. \n This matches the two topics named `topic1` and `topic2`.
`^aaa.*` | Match on the prefix. \n This matches any topic name that starts with `aaa`.
`^aaa.*,^bbb.*` | List of patterns matching on the prefix. \n This matches any topic name that starts with `aaa` or `bbb`.
`^branch_[0-9]{3}_[a-z]*$` | More complex regex pattern to match topic names. \n This matches any topic name that starts with `branch_`, followed by exactly 3 digits, followed by `_` and any number of lowercase letters.
`.*` | Mirror all source topics.
{: caption="Table 5. Example patterns" caption-side="bottom"}

When using the CLI, the patterns are given as a comma-separated list. For example, the following command will select all topics whose name has the prefix `accounting` or `hr`.

```sh
ibmcloud es mirroring-topic-selection-set --select '^accounting.*,^hr.*'
```

The following command shows how to make the same selection by using the Administration REST API. The patterns are in the form of a JSON array named `"includes"`.

```sh
curl -s -X POST -H "Content-Type: application/json" -H "Authorization: <bearer token>" <admin url>/admin/mirroring/topic-selection -d '{"includes":["^accounting.*", "^hr.*"]}'
```

Updating a topic selection replaces the current set of patterns.
{: note}

To remove the selection so that no topics are mirrored, use the `--none` option with the CLI, or an empty pattern with the Administration REST API, as follows.

```sh
ibmcloud es mirroring-topic-selection-set --none
```

```sh
curl -s -X POST -H "Content-Type: application/json" -H "Authorization: <bearer token>" <admin url>/admin/mirroring/topic-selection -d '{"includes":[""]}'
```

To selectively disable mirroring, re-apply the topic selection leaving out the patterns that you want to disable.
For example, when topic1, topic2, topic3 are currently being mirrored, the following commands disable mirroring for topic2 but leaves the other two enabled.

```sh
ibmcloud es mirroring-topic-selection-set --select '^topic1$,^topic3$'
```

```sh
curl -s -X POST -H "Content-Type: application/json" -H "Authorization: <bearer token>" <admin url>/admin/mirroring/topic-selection -d '{"includes":["^topic1$","^topic3$"]}'
```

### Retrieving the topic selection
{: #retrieving_topic_selection}

You can retrieve the mirroring selection by using the following interfaces:

CLI:

```sh
ibmcloud es mirroring-topic-selection
```

REST API:

```sh
curl -s -X GET -H "Authorization: <bearer token>" <admin url>/admin/mirroring/topic-selection
```

### Retrieving the active topics
{: #retrieve_topics}

You can retrieve the topics that are being actively mirrored by using the following interfaces:

CLI:

```sh
ibmcloud es mirroring-active-topics
```

REST API:

```sh
curl -s -X GET -H "Authorization: <bearer token>" <admin url>/admin/mirroring/active-topics
```

## Building mirroring aware applications 
{: #building_apps}

### Producers
{: #producers}

We recommend producers to produce to local topics only, hence they should not require changes when they switch between clusters.

### Consumers
{: #consumers}

Consumers should subscribe to and consume from both the local and remote topics. This can be done with one wild-carded subscription. For example, to consume from both  `accounting.invoice` and `accounting.invoice.<ALIAS>`, use the subscription to `accounting.invoice.*`.

When you consume both local and remote topics, check if the application requires strict ordering. In such a case, remote topics are to be fully consumed first before you start to consume from local topics. This way messages are processed in the order that they were produced.

### Consumer offsets
{: #consumer_offsets}

While consumer groups offsets are replicated between clusters, they must be explicitly used by consumers to reset their position when they switch cluster.
{: note}

The RemoteClusterUtils package allows to easily make these changes. 

## Monitoring mirroring
{: #monitoring_mirroring}

You can monitor mirroring by using IBM Cloud Monitoring. To enable monitoring, see [Monitoring {{site.data.keyword.messagehub}} metrics](/docs/EventStreams?topic=EventStreams-metrics). The **Monitoring** dashboard is available on the target cluster.

The **{{site.data.keyword.messagehub}} Mirroring** dashboard exposes the following metrics:

- Mirroring throughput: The bytes per second of mirroring throughput from the source {{site.data.keyword.messagehub}} instance. This is useful to see whether mirroring is active and for capacity planning.
- Mirroring latency: The per-topic mirroring latency in second from the source {{site.data.keyword.messagehub}} instance. This is useful to determine how far behind a topic on the target cluster is.

Data that is produced within the latency window might not be present on the target cluster yet and still might be lost if a disaster happens on the source cluster. However, if mirroring is up to date, failing over while both clusters stay healthy can be achieved without any data loss.

## Understanding recovery objectives with mirroring
{: #recovery_objectives}

In a data protection plan such as mirroring, recovery point objective (RPO) and recovery time objective (RTO) are key parameters. You must understand the decisions that are associated with these objectives.

You can monitor the recovery point objective by using the mirroring latency metric that is provided in the **Mirroring dashboard**. This metric shows the lag between both clusters, so you can estimate the amount of data loss if a disaster occurs. You are responsible for monitoring that value and ensuring that it fits in your RPO.

The recovery time objective is fully controlled by users and is made of the following timing windows:

- The time that it takes the user to decide to fail over.
- The time that it takes the user to fail over their applications.

### Testing
{: #mirroring_testing}

Test failing over and back when you made your applications mirroring aware. Complete the steps that are outlined in the [Disaster recovery example scenario](/docs/EventStreams?topic=EventStreams-disaster_recovery_scenario) and use the **Monitoring** dashboards to ensure that all steps complete as expected.

## Deleting and re-creating topics with the same name on the source cluster
{: #delete_recreate_topics}

When topics are deleted on the source cluster, the corresponding topic on the target cluster is not automatically deleted. If you delete a topic on the source cluster and then re-create a topic of the same name, replication of topic might not start immediately. Therefore, if you intend to re-create the source topic, delete the corresponding topic on the target cluster before you re-create the topic on the source cluster. Do not delete and then re-create topics with the same name.

## Considerations for Kafka Streams and Kafka Connect
{: #kafka_considerations}

Kafka Streams and Kafka Connect rely on internal topics with specific names to store state and configuration. When these topics are mirrored, they are renamed on the target cluster. For this reason, Kafka Streams and Kafka Connect applications cannot failover and failback seamlessly between clusters. Consider this when you plan disaster recovery of such applications.
