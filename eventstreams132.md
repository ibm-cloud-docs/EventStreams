---

copyright:
  years: 2015, 2018
lastupdated: "2018-11-29"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Service Level Agreement (SLA) for availability
{: #sla}

The {{site.data.keyword.messagehub}} service is provided with an availability of 99.95%. 
For further information about the SLA for {{site.data.keyword.Bluemix}}, see 
[{{site.data.keyword.Bluemix_notm}} service description ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www-03.ibm.com/software/sla/sladb.nsf/pdf/6605-14/$file/i126-6605-14_08-2018_en_US.pdf){:new_window}

## What does 99.95% availability mean?

Availability refers to the ability of applications to produce and consume messages from Kafka topics.

## How do we measure it?

Service instances are continuously monitored for performance, error rates, and response to synthetic operations. Outages are recorded.

## What do you need to consider to achieve this?

To achieve high levels of availability from the application perspective, consider the following three aspects:


### Connectivity

Because of the dynamic nature of the cloud, applications must expect connection breakages. A connection breakage is not considered a failure of service.
* **Retries**: Kafka clients provide re-connect logic, but for producers this must be explicitly enabled (See the producers 'retries' property). Connections are remade within 60 seconds.    
* **Duplicates**: Enabling retries might result in duplicate messages, because depending on when a connection is lost, the producer might not be able to determine if a message was successfully processed by the server and hence must re-send it when reconnected. It is recommended to architect applications to expect duplicate messages. If duplicates cannot be tolerated, the idempotent producer feature (from Kafka 1.1) can be used to prevent duplicates during retries (See the producers 'enable.idempotency' property).

### Throughput

Expressed as the number of bytes per second which can be both sent and received in a cluster. 
* **Recommended**: 40 MB/sec, max peak limit: 90MB/sec
The recommended figure is based on a typical workload, for example messages with a small (<10 K) payload taking in to account the possible impact of operational actions such as internal updates or failure modes such as the loss of an availability zone. If the average throughput exceeds this figure a loss in performance could be experienced during these conditions.

* **Measurement**: It's recommended to instrument applications to be aware of how they are performing, for example the number of messages sent/received, message sizes, return codes etc. Understanding an application's usage will help you configure its resources appropriately e.g. such as the retention time for messages on topics.

* **Saturation**: As the limit of the traffic which can be produced in to the cluster is approached, producers will start to be throttled, latency will increase and ultimately errors, such as timeout errors, will be seen. Depending on the configuration, message consistency and durability might also be impacted, see the following additional information.

### Consistency and durability of messages

Kafka achieves its availability and durability by replicating the messages it receives across other nodes in the cluster, which can then be used in case of failure. {{site.data.keyword.messagehub}} uses three replicas (default.replication.factor = 3) meaning that each message received by a node will be replicated to two other nodes in different availability zones. In this way, the loss of a node or availability zone can be tolerated without loss of data or function.
* **Producer Acks Mode**: Although replication is performed for all messages, applications can control how robustly the messages they produce are transferred to the service by using the producer's acks mode property. This property provides a choice between speed versus risk of message loss. The default setting is acks=1 meaning that the producer returns success as soon as the node its connected to acknowledges receiving the message, but before replication has completed. The recommended and most assured setting is acks=all where the producer only returns success after the message has been copied to all replicas. This ensures the replicas are kept in step which prevents message loss if a failure causes a switch to a replica. See xx and 'unclean.leader.election' for more details. 


{{site.data.keyword.messagehub}}, see [Configuring your client](/docs/services/EventStreams/eventstreams063.html).







