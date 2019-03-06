---

copyright:
  years: 2015, 2019
lastupdated: "2019-02-06"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Service Level Agreement (SLA) for {{site.data.keyword.messagehub}} availability (Enterprise plan)
{: #sla}

The {{site.data.keyword.messagehub}} service is provided with an availability of 99.95% on the Enterprise plan. 
For more information about the SLA for {{site.data.keyword.Bluemix}}, see
[{{site.data.keyword.Bluemix_notm}} service description ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www-03.ibm.com/software/sla/sladb.nsf/pdf/6605-14/$file/i126-6605-14_08-2018_en_US.pdf){:new_window}.

## What does 99.95% availability mean?
Availability refers to the ability of applications to produce and consume messages from Kafka topics.

## How do we measure it?
Service instances are continuously monitored for performance, error rates, and their response to synthetic operations. Outages are recorded.

## What do you need to consider to achieve this availability?
To achieve high levels of availability from the application perspective, you should consider [connectivity](/docs/services/EventStreams?topic=eventstreams-sla#connectivity), [throughput](/docs/services/EventStreams?topic=eventstreams-sla#throughput), and [consistency and durability of messages](/docs/services/EventStreams?topic=eventstreams-sla#message_consistency). Users are responsible for designing their applications to optimize these three elements for their business.

### Connectivity
{: #connectivity}

Because of the dynamic nature of the cloud, applications must expect connection breakages. A connection breakage is not considered a failure of service.

**Retries**<br/>
Kafka clients provide reconnect logic, but you must explicitly enable reconnects for producers. For more information, see the [ ```retries``` property ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://kafka.apache.org/11/documentation.html#producerconfigs){:new_window}. Connections are remade within 60 seconds.   
 
**Duplicates**<br/>
Enabling retries might result in duplicate messages. Depending on when a connection is lost, the producer might not be able to determine if a message was successfully processed by the server and therefore must send the message again when reconnected. You are recommended to architect applications to expect duplicate messages. 

If duplicates cannot be tolerated, you can use the ```idempotent``` producer feature (from Kafka 1.1) to prevent duplicates during retries. For more information, see the [ ```enable.idempotence``` property ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://kafka.apache.org/11/documentation.html#producerconfigs){:new_window}.

### Throughput
{: #throughput}

Throughput is expressed as the number of bytes per second that can be both sent and received in a cluster. 

**Recommendation**<br/>
40 MB per second with a maximum peak limit of 90 MB per second. <br/>
The recommended figure is based on a typical workload and takes into account the possible impact of operational actions such as internal updates or failure modes like the loss of an availability zone.  For example, messages with a small payload (less than 10 K). If the average throughput exceeds this figure, you might experience a loss in performance during these conditions.

**Measurement**<br/>
You are recommended to instrument applications to be aware of how they are performing. For example, the number of messages sent and received, message sizes, and return codes. Understanding an application's usage helps you configure its resources appropriately, such as the retention time for messages on topics.

**Saturation**<br/>
As the limit of the traffic that can be produced in to the cluster is approached, producers start to be throttled, latency increases, and ultimately errors such as timeout errors occur. Depending on the configuration, message consistency and durability might also be impacted. For more information, see [Consistency and durability of messages](/docs/services/EventStreams?topic=eventstreams-sla#message_consistency).

### Consistency and durability of messages
{: #message_consistency}

Kafka achieves its availability and durability by replicating the messages it receives across other nodes in the cluster, which can then be used in case of failure. {{site.data.keyword.messagehub}} uses three replicas (default.replication.factor = 3) meaning that each message received by a node is replicated to two other nodes in different availability zones. In this way, the loss of a node or availability zone can be tolerated without loss of data or function.

**Producer ```acks``` mode**<br/>
Although all message are replicated, applications can control how robustly the messages they produce are transferred to the service by using the producer's ```acks``` mode property. This property provides a choice between speed and the risk of message loss. The default setting is ```acks=1```, which means that the producer returns success as soon as the node it's connected to acknowledges receiving the message, but before replication has completed. The recommended and most assured setting is ```acks=all``` where the producer only returns success after the message has been copied to all replicas. This ensures the replicas are kept in step, which prevents message loss if a failure causes a switch to a replica.


