---

copyright:
  years: 2015, 2019
lastupdated: "2019-07-03"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}

# Service Level Agreement (SLA) for {{site.data.keyword.messagehub}} availability 
{: #sla}

## Standard plan
{: #sla_standard}

The {{site.data.keyword.messagehub}} service is provided with an availability of 99.95% on the Standard plan.
For more information about the SLA for high availability services in {{site.data.keyword.Bluemix}}, see
[{{site.data.keyword.Bluemix_notm}} service description ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www-03.ibm.com/software/sla/sladb.nsf/pdf/6605-18/$file/i126-6605-18_08-2019_en_US.pdf){:new_window}.


## Enterprise plan
{: #sla_enterprise}

The {{site.data.keyword.messagehub}} service is provided with an availability of 99.95% on the Enterprise plan as a high availability Public environment. When the {{site.data.keyword.messagehub}} service is run in non-HA environments, such as [single zone locations](#sla_szr), the availability is 99.5%. 
For more information about the SLA for high availability services in {{site.data.keyword.Bluemix_notm}}, see
[{{site.data.keyword.Bluemix_notm}} service description ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www-03.ibm.com/software/sla/sladb.nsf/pdf/6605-18/$file/i126-6605-18_08-2019_en_US.pdf){:new_window}.

## Classic plan
{: #sla_classic}

The Classic plan is deprecated. From November 1, 2019, you will no longer be able to provision new instances of the Classic Plan. <br/>However existing instances will continue to be supported.
From June 30, 2020, the Classic Plan will be retired and no longer supported. Any instance of the Classic Plan still provisioned at this date will be deleted. 
{:deprecated}

The {{site.data.keyword.messagehub}} service is provided with an availability of 99.5% on the Classic plan. 
For more information about the SLA for {{site.data.keyword.Bluemix_notm}}, see
[{{site.data.keyword.Bluemix_notm}} service description ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www-03.ibm.com/software/sla/sladb.nsf/pdf/6605-18/$file/i126-6605-18_08-2019_en_US.pdf){:new_window}.

<!--
## What does 99.95% availability mean?
Availability refers to the ability of applications to produce and consume messages from Kafka topics.
-->


## How do we measure it?
Service instances are continuously monitored for performance, error rates, and their response to synthetic operations. Outages are recorded. For more information, see [Service status for Event Streams ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/status?component=messagehub&selected=status){:new_window}.

Availability refers to the ability of applications to produce and consume messages from Kafka topics.

## What do you need to consider to achieve this availability?
To achieve high levels of availability from the application perspective, you should consider [connectivity](/docs/services/EventStreams?topic=eventstreams-sla#connectivity), [throughput](/docs/services/EventStreams?topic=eventstreams-sla#throughput), and [consistency and durability of messages](/docs/services/EventStreams?topic=eventstreams-sla#message_consistency). Users are responsible for designing their applications to optimize these three elements for their business.

### Connectivity
{: #connectivity}

Because of the dynamic nature of the cloud, applications must expect connection breakages. A connection breakage is not considered a failure of service.

**Retries**<br/>
Kafka clients provide reconnect logic, but you must explicitly enable reconnects for producers. For more information, see the [ <code>retries</code> property ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://kafka.apache.org/11/documentation.html#producerconfigs){:new_window}. Connections are remade within 60 seconds.   
 
**Duplicates**<br/>
Enabling retries might result in duplicate messages. Depending on when a connection is lost, the producer might not be able to determine if a message was successfully processed by the server and therefore must send the message again when reconnected. You are recommended to design applications to expect duplicate messages. 

If duplicates cannot be tolerated, you can use the <code>idempotent</code> producer feature (from Kafka 1.1) to prevent duplicates during retries. For more information, see the [ <code>enable.idempotence</code> property ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://kafka.apache.org/11/documentation.html#producerconfigs){:new_window}.

### Throughput
{: #throughput}

Throughput is expressed as the number of bytes per second that can be both sent and received in a cluster. 

**Specific guidance for the Standard plan**<br/>
For throughput guidance information, see [Limits and quotas- Standard](/docs/services/EventStreams?topic=eventstreams-kafka_quotas#standard_throughput). 

**Specific guidance for the Enterprise plan**<br/>

For throughput guidance information, see [Limits and quotas - Enterprise](/docs/services/EventStreams?topic=eventstreams-kafka_quotas#enterprise_throughput). 

**Measurement**<br/>
You are recommended to instrument applications to be aware of how they are performing. For example, the number of messages sent and received, message sizes, and return codes. Understanding an application's usage helps you configure its resources appropriately, such as the retention time for messages on topics.

**Saturation**<br/>
As the limit of the traffic that can be produced in to the cluster is approached, producers start to be throttled, latency increases, and ultimately errors such as timeout errors occur. Depending on the configuration, message consistency and durability might also be impacted. For more information, see [Consistency and durability of messages](/docs/services/EventStreams?topic=eventstreams-sla#message_consistency).

### Consistency and durability of messages
{: #message_consistency}

Kafka achieves its availability and durability by replicating the messages it receives across other nodes in the cluster, which can then be used in case of failure. {{site.data.keyword.messagehub}} uses three replicas (default.replication.factor = 3) meaning that each message received by a node is replicated to two other nodes in different availability zones. In this way, the loss of a node or availability zone can be tolerated without loss of data or function.

**Producer <code>acks</code> mode**<br/>
Although all message are replicated, applications can control how robustly the messages they produce are transferred to the service by using the producer's <code>acks</code> mode property. This property provides a choice between speed and the risk of message loss. The default setting is <code>acks=1</code>, which means that the producer returns success as soon as the node it's connected to acknowledges receiving the message, but before replication has completed. The recommended and most assured setting is <code>acks=all</code> where the producer only returns success after the message has been copied to all replicas. This ensures the replicas are kept in step, which prevents message loss if a failure causes a switch to a replica.

## Single zone location deployments
{: #sla_szr}

For the highest availability we recommend our high availability Public environments, which are built in our multizone locations. In a multizone location, our Kafka clusters are distributed across 3 availability zones, which means that the cluster is resilient to the failure of a single zone or any component within that zone.
Some customers require geographic locality and therefore want to provision an {{site.data.keyword.messagehub}} cluster in a geographically local but single zone location. {{site.data.keyword.messagehub}} supports this deployment model, however be aware of the following availability trade-offs:
* In a single zone location, there are categories of single failures that might lead to the cluster going offline for a period of time. For example, the failure of an entire data center or the update or failure of a shared component such as the underlying hypervisor, SAN, or network. These failures are reflected in the reduced SLA for single zone locations.
* An advantage of spreading Kafka across many zones is to minimize the chance of a failure that could bring down an entire cluster. In contrast, there is the small possibility that a single failure could bring down the entire cluster within one zone. In extreme cases there is also the potential of data loss. For example, even if <code>acks=all</code> is used by the producers, if all Kafka nodes went down simultaneously, there might be some messages that the brokers had acknowledged receipt for, but the underlying file system had not completed the flush to disk. Potentially, those un-flushed messages could be lost. 

    For more information, see [Message acknowledgments](/docs/services/EventStreams?topic=eventstreams-producing_messages#message_acknowledgments). In many use cases this is not necessarily an issue. However, if message loss is unacceptable under any circumstance, consider other strategies such as using a multi-availability zone cluster, cross region replication, or producer side message checkpointing.

For more information, see [single zone clusters](/docs/containers?topic=containers-regions-and-zones#regions_single_zone) and [multizone clusters](/docs/containers?topic=containers-regions-and-zones#regions_multizone).




