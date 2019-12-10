---

copyright:
  years: 2015, 2019
lastupdated: "2019-12-10p"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka, migration. Dedicated, upgrade

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}
{:deprecated: .deprecated}

# Upgrading to the {{site.data.keyword.messagehub}} Enterprise plan from {{site.data.keyword.cloud_notm}} Dedicated
{: #migrate_dedicated_enterprise}

The {{site.data.keyword.messagehub}} Enterprise plan provides data isolation, guaranteed performance, increased retention and exclusive access to a dedicated {{site.data.keyword.messagehub}} cluster.

To migrate applications from {{site.data.keyword.messagehub}} on {{site.data.keyword.cloud_notm}} Dedicated to the Enterprise plan, consider the following information.
{: shortdesc}


Service instances are now provisioned as {{site.data.keyword.cloud_notm}} Services rather than as Cloud Foundry Services. This enables the service to support the latest {{site.data.keyword.cloud_notm}} standards and capabilities, including multi-zone deployments and granular access controls, but has implications for how the service is used. In particular, consider the following aspects:

## Creating, deleting, and listing services
{: #create_services}

As before, you can manage the lifecycle of services using either the {{site.data.keyword.cloud_notm}} console or the {{site.data.keyword.cloud_notm}} CLI command line tool. If you're using the console, services are now listed under **Services** instead of **Cloud Foundry Services**. 

If you're using the CLI, instances are managed using the resource commands. For example,  <code>ibmcloud resource service-instance-create</code>. This is instead of the **cf** commands, for example <code>ibmcloud cf create-service</code>.

## Controlling access
{: #controlling_access}

Authentication and authorization are now managed using the Cloud Identity and Access Management (IAM) service. As well as controlling a user's ability to connect, IAM also enables you to configure granular access to underlying resources, such as topics. Access is controlled by assigning policies to users. For more information, see 
[Managing access to your {{site.data.keyword.messagehub}} resources](/docs/services/EventStreams?topic=eventstreams-security).

## Connecting applications
{: #connecting_apps}

The information that an application needs to connect has not changed, that is, a list of <code>bootstrap.servers</code>, <code>username</code>, and <code>password</code> is required. However, the way these properties are retrieved has changed.

<ul>
<li>
      <strong>For native applications</strong>
        <br/>
        You must create a Credentials object using the IBM Cloud console or a Service Key object using the CLI. You can then retrieve the required properties. For more information, see 
        [Connecting applications](/docs/services/EventStreams?topic=eventstreams-connecting#connect_enterprise_external).
</li>
<br/>
<li><strong>For Cloud Foundry applications</strong>
        <br/>
        You must first bind the service to the application's organization and space by creating a service alias. You can then retrieve the required properties from the VCAP_SERVICES environment variable as normal. For more information, see 
        [Connecting to {{site.data.keyword.messagehub}}](/docs/services/EventStreams?topic=eventstreams-connecting).
</li>
</ul>
<br/>
Note that clients must support the SNI extension to TLS where the server's hostname is included in the TLS handshake. This feature is commonly available and is supported in all the client versions recommended in [Choosing a Kafka client to use with {{site.data.keyword.messagehub}}](/docs/services/EventStreams?topic=eventstreams-kafka_using#kafka_clients).
</li>
</ul>

<br>
You should also be aware of some other changes as follows:
## Kafka version
{: #kafka_version}

This plan provides access to the latest stable Kafka release 2.2. Applications developed against Kafka 1.1 can run unchanged, but refer to the following information for recommended client versions and tested combinations: [Choosing a Kafka client to use with {{site.data.keyword.messagehub}}](/docs/services/EventStreams?topic=eventstreams-kafka_using#kafka_clients). 

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


## Tenancy
{: #tenancy}



## Integrations
{: #integrations}

Connection from other services, such as {{site.data.keyword.iot_short_notm}} or {{site.data.keyword.openwhisk_short}}, which bind to the service using a Cloud Foundry organization and space, require a service alias to be created. For more information, see
[Connect Cloud Foundry applications to {{site.data.keyword.messagehub}}](/docs/services/EventStreams?topic=eventstreams-connecting#connect_enterprise_cf).

## Supported capabilities
{: #capabilities}

There are differences between the capabilities of IBM Cloud Dedicated and the Enterprise plan. To align the product offerings, adopt new technology choices, and remove less-used features, not all capabilities are carried forward. The following table compares the available features.

If you currently use the REST APIs, see [Migrating the REST APIs](/docs/services/EventStreams?topic=eventstreams-migrate_rest_apis).

<table>
    <caption>Table 1. Support in Dedicated and Enterprise plans</caption>
      <tr>
	        <th></th>
		    <th>Dedicated Plan</th>
	      	    <th>Enterprise Plan</th>
        </tr>
		<tr>
			<td>**Tenancy**</td>
			<td>Single tenant </td>
			<td>Single tenant</td>			
		</tr>
        <tr>
			<td>**Availability zones**</td>
			<td>0</td>
			<td>3<br/>(1 in single zone locations)
			</td>
		</tr>
        <tr>
			<td>**Availability**</td>
			<td>99.5%</td>
			<td>99.99%<br/>(99.9% in single zone locations) [<sup>1</sup>](/docs/services/EventStreams?topic=eventstreams-migrate_dedicated_enterprise#footnote_szr)</td>
		</tr>
	  		<tr>
			<td>**Kafka version on cluster**</td>
			<td>Kafka 1.1</td>
			<td>Kafka 2.2</td>
		</tr>
		<tr>
			<td>**Fine-grained access control**</td>
			<td>At an instance level only</td>
			<td>Yes</td>
		</tr>
		<tr>
			<td>**Customer-managed encryption**</td>
			<td>No</td>
			<td>Yes</td>
		</tr>
				<tr>
			<td>**Cloud Service Endpoint support**</td>
			<td>No</td>
			<td>Yes</td>
		</tr>
		<tr>
			<td>**Kafka Connect and Kafka Streams supported **</td>
			<td>Yes</td>
			<td>Yes</td>
		</tr>
		<tr>
			<td>**Maximum number of partitions**</td>
			<td>1000</td>
			<td>3000</td>
		</tr>
		<tr>
			<td>**Maximum retention period**</td>
			<td>1 TB  of usable storage per broker </td>
			<td>2 TB of usable storage per broker<!--Unlimited up to the storage limit of your plan --></td>
		</tr>
		<tr>
			<td>**Maximum throughput**</td>
			<td>Not specified</td>
			<td>80 MB per second per cluster (peak throughput of 150 MB per second) [<sup>2</sup>](/docs/services/EventStreams?topic=eventstreams-migrate_dedicated_enterprise#footnote_throughput)</td>
		</tr>
		<tr>
			<td>**Maximum message size**</td>
			<td>1 MB</td>
			<td>1 MB</td>
		</tr>
		<tr>
			<td>**Maximum number of connected clients**</td>
			<td>Not specified</td>
			<td>10 000</td>
		</tr>
		<tr>
			<td>**Location (region) availability**</td>
			<td>
			Dallas (us-south)</br>
			London (eu-gb)<br/>
			Sydney (au-syd)</br>
			Frankfurt (eu-de)<br/>
			<br/>
			</td>
			<td>**Multizone location (MZR)**</br>
			Dallas (us-south)</br>
			Washington (us-east)<br/>
			London (eu-gb)<br/>
			Sydney (au-syd)</br>
			Frankfurt (eu-de)<br/>
			Tokyo (jp-tok)<br/>
			<br/>
			**Single zone location (SZR)**</br>
			Seoul (seo01)<br/>
			Chennai (che01)<br/>
			<br/>
			</td>
		</tr>
		<tr>
     	    <td>**APIs supported**</td>

			<td>Kafka API<br/>
			Admin REST API</br>
			REST API</br>
			</td>
			<td>Kafka API</br>
			Admin REST API<br/>
			REST Producer API</br>
		    </td>
		</tr>
		</tr>
			<td>**{{site.data.keyword.messagehub}} CLI supported**</td>

			<td>No</td>
			<td>Yes</td>
		</tr>
		</tr>
		<tr>
			<td>**Deployment timeframe**</td>
			<td>Weeks to months</td>
			<td>Expect provisioning to take up to 3 hours. Because Enterprise has its own dedicated resources for each cluster, it requires more time for provisioning</td>
		</tr>
		<tr>
			<td>**Compliance**</td>
			<td>GDPR<br/>
Privacy Shield<br/>
ISO 27001, 27017, 27018<br/></td>
			<td>GDPR<br/>
Privacy Shield<br/>
ISO 27001, 27017, 27018<br/>
SOC 1 Type 1<br/>
SOC 2 Type 1<br/>
HIPPA ready<br/>
PCI<br/>
</td>
		</tr>

</table>

### Footnotes
{: #footnote_plans notoc}

1. {: #footnote_szr notoc} For more information about availability, see [single zone location deployments](/docs/services/EventStreams?topic=eventstreams-sla#sla_szr).
2. {: #footnote_throughput notoc}A recommended maximum is 80 MB per second, that is 40 MB per second for producing and 40 MB per second for consuming. <br/>
A recommended peak limit is 150 MB per second, that is 75 MB per second for producing and 75 MB per second for consuming.

<br/>
Small code deltas are shipped daily to production. As a result, you can expect to see many further improvements to our user experience (and other areas). Coming soon:

* **Customer metrics**<br/>
    The ability to monitor activity in a service instance.

<br/>


## Preparing to migrate to the Enterprise plan
{: #enterprise_prep}

<br/>
### Discovering topics and configuration in an existing cluster
{: #existing_topic_config}

If you want to find out information about your topics and configuration in an existing cluster so you can recreate them in a new cluster, use the [*kafka-topics* tool ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/services/EventStreams?topic=eventstreams-kafka_console_tools#topics_tool){:new_window}. Ensure you use V2.3 of the tool, which does not require Zookeeper access.


For example, some sample output from running the *kafka-topics* tool:

```
~/kafka_2.12-2.3.0 $ bin/kafka-topics.sh --bootstrap-server kafka03-prod01.messagehub.services.us-south.bluemix.net:9093 --command-config vcurr_dal06.properties --describe

Topic:kafka-nodejs-console-sample-topic	PartitionCount:1	ReplicationFactor:3	Configs:min.insync.replicas=2,unclean.leader.election.enable=true,retention.bytes=1073741824,segment.bytes=536870912,retention.ms=86400000
	Topic: kafka-nodejs-console-sample-topic	Partition: 0	Leader: 5	Replicas: 5,8,2	Isr: 8,5,2
Topic:edotesttopic	PartitionCount:2	ReplicationFactor:3	Configs:min.insync.replicas=2,unclean.leader.election.enable=true,retention.bytes=1073741824,segment.bytes=536870912,retention.ms=86400000
	Topic: edotesttopic	Partition: 0	Leader: 3	Replicas: 3,0,8	Isr: 3,0,8
	Topic: edotesttopic	Partition: 1	Leader: 6	Replicas: 6,8,2	Isr: 6,8,2
```
{: codeblock}

<br/>

### Switching from the existing cluster to a new cluster
{: #switch_cluster}

Complete the following steps to switch from an existing cluster to a new cluster as part of migration: 

1. Stop producing to the old cluster.
2. Drain all the messages from the old cluster. Use the [*kafka-consumer-groups* tool ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/services/EventStreams?topic=eventstreams-kafka_console_tools#consumer_groups_tool){:new_window} to complete this task. Ensure you use V2.3 of the tool because this version makes it easier to check whether a group has lag 0 (that is, if it has reached the log end offset for each of its partitions).

For example, some sample output from running the *kafka-consumer-groups* tool:

```
~/kafka_2.12-2.3.0 $ bin/kafka-consumer-groups.sh --bootstrap-server kafka03-prod01.messagehub.services.us-south.bluemix.net:9093 --command-config vcurr_dal06.properties --describe --all-groups

Consumer group 'edo-hyperion-groupid1575992638473' has no active members.

GROUP                             TOPIC           PARTITION  CURRENT-OFFSET  LOG-END-OFFSET  LAG             CONSUMER-ID     HOST            CLIENT-ID
edo-hyperion-groupid1575992638473 edotesttopic    0          131             261             130             -               -               -
edo-hyperion-groupid1575992638473 edotesttopic    1          142             268             126             -               -               -

Consumer group 'edo-hyperion-groupid1575992703846' has no active members.

GROUP                             TOPIC           PARTITION  CURRENT-OFFSET  LOG-END-OFFSET  LAG             CONSUMER-ID     HOST            CLIENT-ID
edo-hyperion-groupid1575992703846 edotesttopic    0          245             261             16              -               -               -
edo-hyperion-groupid1575992703846 edotesttopic    1          256             268             12              -               -               -

```
{: codeblock}

3. Switch the consumer to the new cluster.

<br/>

### Calculate storage footprint of a partition
{: #calculate_footprint}

To calculate the storage footprint of a partition approximately, use the following formula: 
```
retention.bytes + segment.bytes + a safety margin
```






