---

copyright:
  years: 2015, 2018
lastupdated: "2017-03-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# MQ bridge
{: #mq_bridge}

The MQ bridge allows you to transfer message data from an {{site.data.keyword.IBM_notm}}
 MQ queue to a {{site.data.keyword.messagehub}} Kafka topic. The MQ bridge enables you to efficiently perform cloud-style workloads (for example, data analytics) against {{site.data.keyword.IBM_notm}} MQ message data generated within your enterprise.
 {:shortdesc}

The MQ bridge connects to an {{site.data.keyword.IBM_notm}} MQ queue manager as an MQ client and consumes MQ message data from an MQ queue. The bridge converts each MQ message into a Kafka record and sends the message to a {{site.data.keyword.messagehub}} Kafka topic.

## Supported versions of {{site.data.keyword.IBM_notm}} MQ
{: #mq_support}

The versions of {{site.data.keyword.IBM_notm}} MQ that the bridge works with are as follows:

* {{site.data.keyword.IBM_notm}} MQ version 8.0, and later

## Securing the MQ bridge
{: #mq_bridge_security}

You can configure the MQ bridge to authenticate with {{site.data.keyword.IBM_notm}} MQ using a user identifier and password. We recommend that you grant the following permissions only to the identity associated with an instance of the MQ bridge:

* CONNECT authority. The MQ bridge must be able to connect to the MQ queue manager.
* GET authority for the queue that the MQ bridge is configured to consume from.

## Message reliability and ordering
{: #mq_bridge_reliability}

The MQ bridge implements an at-least-once level of reliability for the message data that it
transfers. This means that the bridge does not lose message data, but might occasionally generate
duplicate sequences of Kafka records for a given sequence of MQ messages. Typically, duplication
occurs when an event interrupts the bridge's processing of message data. For example:

* Restart of the MQ queue manager
* Interruption of the network between the MQ queue manager and the bridge
* Rebalancing of Kafka topic partition assignment
* Interruption of the network between the bridge and Kafka

To ensure that the MQ bridge can reliably transfer messages from MQ, the bridge requests
exclusive access to the MQ queue that it reads messages from. This access prevents other
applications from receiving messages from the MQ queue while the bridge is using it. If other
applications are already receiving messages from the queue, the MQ bridge might be unable to start
until these applications end.

Generally the MQ bridge forwards MQ messages to Kafka in the order that they are received from {{site.data.keyword.IBM_notm}} MQ. However, occasionally MQ message data is duplicated within a Kafka topic (for the reasons described previously). This possible duplication can result in differences between the order of MQ messages and the order that the corresponding records are stored in Kafka.

## Kafka partition assignment
{: #mq_bridge_partition}

The MQ bridge supports options to control the assignment of {{site.data.keyword.IBM_notm}} MQ message data to Kafka topic partitions. Message ordering within a particular partition depends on the option selected for message data ordering (see [Message reliability and ordering](#mq_bridge_reliability)). The supported values are as follows:
<dl><dt>Default</dt>
<dd>Kafka's default partition assignment is used which means that data from MQ messages is
distributed evenly across the partitions in the Kafka topic.</dd>
<dt>CorrelationId</dt>
<dd>MQ messages with the same Correlation ID are assigned to the same Kafka partition.</dd>
<dt>GroupId</dt>
<dd>MQ messages with the same Group ID are assigned to the same Kafka partition.
</dd>
</dl>

## Message size restrictions
{: #mq_message}

You can configure {{site.data.keyword.IBM_notm}} MQ to store messages that are too large to fit into a {{site.data.keyword.messagehub}} Kafka record. The maximum Kafka record size
is 1 000 000 bytes, although some of this capacity is used when the bridge is configured to perform
Kafka partition assignment based on MQ Correlation identifier, or MQ Group identifier. We recommend
sending messages that are no larger than 950 kilobytes using the MQ bridge.

If the MQ bridge encounters a message that is too large to forward to Kafka, the bridge discards
the message and writes a log entry to your Kibana dashboard. Consider setting the MAXMSGL attribute
of the MQ queue that the bridge receives messages from to prevent MQ applications from sending
messages to the queue that cannot be transferred using the MQ bridge.
