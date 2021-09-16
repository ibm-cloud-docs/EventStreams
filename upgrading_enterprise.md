---

copyright:
  years: 2015, 2020
lastupdated: "2020-04-29thu2"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka, migration. Dedicated, upgrade, wildcarding, IAM, wildcard, policies

subcollection: EventStreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}
{:deprecated: .deprecated}
{:important: .important}

# Upgrading to the {{site.data.keyword.messagehub}} Enterprise plan from {{site.data.keyword.cloud_notm}} Dedicated
{: #migrate_dedicated_enterprise}

The {{site.data.keyword.messagehub}} Enterprise plan provides data isolation, guaranteed performance, increased retention, and exclusive access to a dedicated {{site.data.keyword.messagehub}} cluster.

To migrate applications from {{site.data.keyword.messagehub}} on {{site.data.keyword.cloud_notm}} Dedicated to the Enterprise plan, consider the following information.
{: shortdesc}


## How service instances are provisioned on Enterprise 
{: #instance_provision}

Service instances on Enterprise are provisioned as {{site.data.keyword.cloud_notm}} Services rather than as Cloud Foundry Services on Dedicated. This enables the service to support the latest {{site.data.keyword.cloud_notm}} standards and capabilities, including multi-zone deployments and granular access controls, but has implications for how the service is used. In particular, consider the following aspects:

## Creating, deleting, and listing services
{: #create_services}

As before, you can manage the lifecycle of services using either the {{site.data.keyword.cloud_notm}} console or the {{site.data.keyword.cloud_notm}} CLI command line tool. If you're using the console, services are now listed under **Services** instead of **Cloud Foundry Services**. 

If you're using the CLI, instances are managed using the resource commands. For example,  <code>ibmcloud resource service-instance-create</code>. This is instead of the **cf** commands, for example <code>ibmcloud cf create-service</code>.

## Controlling access
{: #controlling_access}

Authentication and authorization are now managed using the Cloud Identity and Access Management (IAM) service. As well as controlling a user's ability to connect, IAM also enables you to configure granular access to underlying resources, such as topics. Access is controlled by assigning policies to users. For more information, see 
[Managing access to your {{site.data.keyword.messagehub}} resources](/docs/EventStreams?topic=EventStreams-security).

If you are part of a department that previously owned its own instance on a Dedicated cluster and you now want to limit access to your resources on the Enterprise cluster (topics, consumer groups and so on), you can take advantage of the IAM wildcarding facility to set policies for groups of resources. For example, if you give all your topics names like `Dept1_Topic1` and `Dept1_Topic2`, you can set policies for topics called `Dept1_*` and these policies will be applied to all topics with that prefix. For more information, see 
[Assigning access by using wildcard policies ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/iam?topic=iam-wildcard){: new_window}.

## Connecting applications
{: #connecting_apps}

The information that an application needs to connect has not changed, that is, a list of <code>bootstrap.servers</code>, <code>username</code>, and <code>password</code> is required. However, the way these properties are retrieved has changed.

For native applications
:   You must create a Credentials object using the IBM Cloud console or a Service Key object using the CLI. You can then retrieve the required properties. For more information, see [Connecting applications](/docs/EventStreams?topic=EventStreams-connecting#connect_enterprise_external).

For Cloud Foundry applications
:   You must first bind the service to the application's organization and space by creating a service alias. You can then retrieve the required properties from the VCAP_SERVICES environment variable as normal. For more information, see [Connecting to {{site.data.keyword.messagehub}}](/docs/EventStreams?topic=EventStreams-connecting).

Note that clients must support the SNI extension to TLS where the server's hostname is included in the TLS handshake. This feature is commonly available and is supported in all the client versions recommended in [Choosing a Kafka client to use with {{site.data.keyword.messagehub}}](/docs/EventStreams?topic=EventStreams-kafka_using#kafka_clients).

You should also be aware of some other changes as follows:
## Kafka version
{: #kafka_version}

This plan provides access to the latest stable Kafka release 2.3. Applications developed against Kafka 1.1 can run unchanged, but refer to the following information for recommended client versions and tested combinations: [Choosing a Kafka client to use with {{site.data.keyword.messagehub}}](/docs/EventStreams?topic=EventStreams-kafka_using#kafka_clients). 

## Supported regions
{: #supported_regions}

The plan is available in the following multi-zone regions:
* Dallas (us-south)
* Washington (us-east)
* London (eu-gb)
* Sydney (au-syd)
* Frankfurt (eu-de)
* Tokyo (jp-tok)

And in the following single-zone regions:
* Seoul (seo01)
* Chennai (che01)


## Integrations
{: #integrations}

Connection from other services, such as {{site.data.keyword.iot_short_notm}} or {{site.data.keyword.openwhisk_short}}, which bind to the service using a Cloud Foundry organization and space, require a service alias to be created. For more information, see
[Connect Cloud Foundry applications to {{site.data.keyword.messagehub}}](/docs/EventStreams?topic=EventStreams-connecting#connect_enterprise_cf).

## Supported capabilities
{: #capabilities}

There are differences between the capabilities of IBM Cloud Dedicated and the Enterprise plan. To align the product offerings, adopt new technology choices, and remove less-used features, not all capabilities are carried forward. The following table compares the available features.

If you currently use the REST APIs, see [Migrating the REST APIs](/docs/EventStreams?topic=EventStreams-migrate_rest_apis).


|   |  Dedicated Plan |  Enterprise Plan  |
|---|---|---|
| **Tenancy**  |Single tenant   | Single tenant  |
|**Availability zones**   | 1  |3    \n  (1 in single zone locations)   |
| **Availability**  |  99.5% |99.99%   \n  \n  (99.9% in single zone locations) [<sup>1</sup>](/docs/EventStreams?topic=EventStreams-migrate_dedicated_enterprise#footnote_szr)  |
| **Kafka version on cluster**  | Kafka 1.1 | Kafka 2.3  |
| **Fine-grained access control**  | At an instance level only  |  Yes |
|  **Customer-managed encryption** | No  | Yes  |
|  **Cloud Service Endpoint support** | No   | Yes  |
| **Kafka Connect and Kafka Streams supported**  |  Yes | Yes  |
| **Maximum number of partitions**  | 1000  |  3000 [<sup>2</sup>](/docs/EventStreams?topic=EventStreams-migrate_dedicated_enterprise#footnote_partitions) |
|**Maximum retention period** [<sup>3</sup>](/docs/EventStreams?topic=EventStreams-migrate_dedicated_enterprise#footnote_footprint)   | 1 TB  of usable storage per broker   | 2 TB  of usable storage per broker   |
| **Maximum throughput**  | Not specified  |  80 MB per second per cluster (peak throughput of 150 MB per second) [<sup>4</sup>](/docs/EventStreams?topic=EventStreams-migrate_dedicated_enterprise#footnote_throughput) |
| **Maximum message size**  | 1 MB  | 1 MB   |
| **Maximum number of connected clients**  |Not specified   | 10 000  |
|  **Location (region) availability** | Various  |  **Multizone location (MZR)**   \n Dallas (us-south)   \n Washington (us-east)   \n London (eu-gb)   \n Sydney (au-syd)   \n Frankfurt (eu-de)   \n  Tokyo (jp-tok)   \n  \n  **Single zone location (SZR)**   \n Seoul (seo01)   \n Chennai (che01) |
| **APIs supported** |  Kafka API   \n Admin REST API   \n REST API |  Kafka API   \n Admin REST API   \n REST Producer API    |
| **{{site.data.keyword.messagehub}} CLI supported** | No  | Yes  |
| **Deployment timeframe** | Weeks to months  | Expect provisioning to take up to 3 hours. Because Enterprise has its own dedicated resources for each cluster, it requires more time for provisioning  |
| **Compliance** |GDPR   \n  Privacy Shield   \n  ISO 27001, 27017, 27018 |  GDPR   \n Privacy Shield   \n ISO 27001, 27017, 27018   \n  SOC 1 Type 1    \n  SOC 2 Type 1  \n HIPAA ready    \n  PCI |


Small code deltas are shipped daily to production. As a result, you can expect to see many further improvements to our user experience (and other areas).


### Footnotes
{: #footnote_plans notoc}

1. For more information about availability, see [single zone location deployments](/docs/EventStreams?topic=EventStreams-sla#sla_szr). {: #footnote_szr notoc}
2. 3000 is a hard limit for partitions on the Enterprise plan. If you reach this limit, you can no longer create topics. To increase the number of partitions beyond 3000, [contact IBM ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/get-support?topic=get-support-getting-customer-support#using-avatar){: new_window}. {: #footnote_partitions notoc}
3. To approximately calculate the storage footprint of a partition, use the following formula, which is used with a safety margin to avoid filling the storage: 
 ```
retention.bytes + segment.bytes
```
{: codeblock} {: #footnote_footprint notoc}

4. A recommended maximum is 80 MB per second, that is 40 MB per second for producing and 40 MB per second for consuming.  
A recommended peak limit is 150 MB per second, that is 75 MB per second for producing and 75 MB per second for consuming. {: #footnote_throughput notoc}

## Preparing to migrate to the Enterprise plan
{: #enterprise_prep}

### Service instances
{: #service_instances}

A key difference between the Dedicated and Enterprise plans is that Dedicated supports the provisioning of multiple instances of the {{site.data.keyword.messagehub}} service. That is, users in Dedicated can each provision an instance of {{site.data.keyword.messagehub}}, but that instance resides on the Dedicated (4-node Kafka) {{site.data.keyword.messagehub}} cluster. However, to users, it appears like they have their own instance of {{site.data.keyword.messagehub}}.

When moving from a Dedicated {{site.data.keyword.messagehub}} cluster, you have the following two options:

* Provision {{site.data.keyword.messagehub}} instances on the Public multi-tenant [Standard plan](/docs/EventStreams?topic=EventStreams-plan_choose#plan_standard).
* Alternatively, if hosting an instance on a Public multi-tenant plan is not an option, create your {{site.data.keyword.messagehub}} resources on an Enterprise plan. The following example illustrates this option.

The Enterprise plan is provisioned by the Admin in the account, or at a minimum a user with sufficient permissions to provision such an instance. The Admin then grants access rights to users to create topics and partitions on that Enterprise instance.

#### Migration example 
{: #dedicated_prefix notoc}

If you are migrating multiple users from a Dedicated {{site.data.keyword.messagehub}} cluster, who had each provisioned their own {{site.data.keyword.messagehub}} instances on that Dedicated cluster, bear in mind that you should prefix resources like topics with a namespace denominator that differentiates between users.

For example:
* On Dedicated {{site.data.keyword.messagehub}}, there might be two different business lines, each with their own instance. And within their instance each business line created a topic called `Test`.
* If business line 1 then migrated to a new Enterprise instance and simply created a topic called `Test` on the new Enterprise instance, that stops the other business line migrating their topic called `Test`.
* Therefore, you are recommended to prefix new topics with a business line label when you create them on Enterprise. For example `BL1_Test` and `BL2_Test`.
* Similar rules apply to consumer group names. If an instance provisioned by `Dept1` on Dedicated has a consumer group called `group1`, on Enterprise the consumer group should be called `Dept1_group1`.
* When using prefixes, you can take advantage of IAM wildcarding for your business lines. For more information, see [Controlling access](#controlling_access).



### Migrating topics
An application using {{site.data.keyword.messagehub}} produces to and consumes from a number of Kafka topics.

To migrate from a Dedicated cluster to an Enterprise instance, create the topics on the new instance with the same configuration as the Dedicated instance.

#### Obtaining information about topics and their configuration in an existing cluster
{: #existing_topic_config}

If you want to find out information about your topics and their configuration in an existing cluster so that you can recreate them in a new cluster, use the **kafka-topics** tool. Ensure that you use V2.3 of the tool, which does not require Zookeeper access.


For example, some sample output from running the **kafka-topics** tool:

```
~/kafka_2.12-2.3.0 $ bin/kafka-topics.sh --bootstrap-server kafka03-prod01.messagehub.services.us-south.bluemix.net:9093 --command-config vcurr_dal06.properties --describe

Topic:sample-topic	PartitionCount:1	ReplicationFactor:3	Configs:min.insync.replicas=2,unclean.leader.election.enable=true,retention.bytes=1073741824,segment.bytes=536870912,retention.ms=86400000
...
Topic:testtopic	PartitionCount:2	ReplicationFactor:3	Configs:min.insync.replicas=2,unclean.leader.election.enable=true,retention.bytes=1073741824,segment.bytes=536870912,retention.ms=86400000
...
```
{: codeblock}


You can now use this information to create the same named topics in the new cluster. 
For more information about how to create topics, see [Using the administration Kafka Java client API](/docs/EventStreams?topic=EventStreams-kafka_java_api) or the 
[ibmcloud es topic-create command](/docs/EventStreams?topic=EventStreams-cli_reference#ibmcloud_es). 
Alternatively, you can also use the IBM {{site.data.keyword.messagehub}} console.

Prefix the topic name with a name that references the instance in Dedicated as described in the [migration example](/docs/EventStreams?topic=EventStreams-migrate_dedicated_enterprise#dedicated_prefix).
{: important}


### Migrating consumer groups
In Dedicated, consumer groups are scoped to the specific instance (exactly as for topics).
No such scoping exists in the Enterprise plan, so applications should avoid name collisions to avoid unnecessary group rebalances.

When targeting an Enterprise cluster, prefix consumer group names with a name that references the instance in Dedicated.
{: important}

Unlike topics, consumer groups are automatically created, so there is no need to create them in advance. 

### Migration considerations: connecting 
When topics exist on the new plan, your applications will need to switch to using the new plan.

Ensure that your Kafka clients are 0.10.x or later.
{: important}

To update your applications to use the new service see
[Connecting to Event Streams](https://cloud.ibm.com/docs/EventStreams?topic=EventStreams-connecting). 
For Cloud Foundry based applications, see
[Connect Cloud Foundry applications](/docs/EventStreams?topic=EventStreams-connecting#connect_enterprise_cf). 

### Switching from the existing cluster to a new cluster
{: #switch_cluster}

After you have set up your topics, consumers, and producers for the new Enterprise plan and have tested their connectivity, you are ready to start the switchover process. The following procedure is recommended.

Complete the following steps to switch from an existing cluster to a new cluster as part of migration: 

1. Stop any producers producing to the existing cluster or topic.
2. Drain all the messages from the existing cluster or topic. You can confirm this by checking that all consumers for that topic or cluster have zero lag by using the [**kafka-consumer-groups** ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/EventStreams?topic=EventStreams-kafka_console_tools#consumer_groups_tool){: new_window} tool. Ensure that you use V2.3 of the tool because this version makes it easier to check whether a group has lag 0 (that is, if it has reached the log end offset for each of its partitions).

   For example, some sample output from running the **kafka-consumer-groups** tool:

   ```
   ~/kafka_2.12-2.3.0 $ bin/kafka-consumer-groups.sh --bootstrap-server kafka03-prod01.messagehub.services.us-south.bluemix.net:9093 --command-config vcurr_dal06.properties --describe --all-groups

   Consumer group 'testgroup1' has no active members.

   GROUP         TOPIC        PARTITION  CURRENT-OFFSET  LOG-END-OFFSET  LAG             CONSUMER-ID     HOST            CLIENT-ID
   testgroup1    testtopic    0          131             261             130             -               -               -
   testgroup1    testtopic    1          142             268             126             -               -               -

   Consumer group 'testgroup2' has no active members.

   GROUP         TOPIC        PARTITION  CURRENT-OFFSET  LOG-END-OFFSET  LAG             CONSUMER-ID     HOST            CLIENT-ID
   testgroup2    testtopic    0          245             261             0               -               -               -
   testgroup2    testtopic    1          256             268             0               -               -               -

   ```
   {: codeblock}
3. Switch to using the new producers and consumers on the new Enterprise cluster.








