---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-25"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Message Hub and Apache Kafka
{: #apache_kafka}

Apache Kafka forms the reliable messaging core of {{site.data.keyword.messagehub}}. It is a publish-subscribe messaging system
and is designed to be fault-tolerant providing a high-throughput, low-latency platform for handling
real-time data feeds. These characteristics make it ideal for use in a cloud environment.
{:shortdesc}

![Kafka architecture diagram.](kafka_architecture.png "Diagram showing Kafka architecture. Producers are feeding into a Kafka cluster and the messages are then being subscribed to by consumers.") 

The following list defines some Apache Kafka concepts:

<dl><dt>Topic</dt>
<dd>A feed that messages are published to.</dd>
<dt>Partition</dt>
<dd>Each topic comprises one or more partitions. Each partition is an ordered list of messages. If a
topic has more than one partition, it allows data to be fed through in parallel to increase
throughput.</dd>
<dt>Producer</dt>
<dd>A process that publishes streams of messages to Kafka topics. A producer can publish to one or
more topics and can optionally choose the partition that stores the data.</dd>
<dt>Consumer </dt>
<dd>A process that consumes messages from Kafka topics, and processes the feed of published
messages. A consumer can subscribe to one or more topics or partitions.</dd>
<dt>Consumer group</dt>
<dd>A named group of one or more consumers. Each consumer in the group reads messages from specific
partitions in the topics that the consumer subscribes to. Each message is delivered to one consumer
in the group and all messages with the same key are delivered to the same consumer.

<p>Each partition is assigned to one consumer in the group only.</p> 
<ul>
<li>If there are more partitions than consumers in a group, some consumers have multiple
partitions.</li>
<li>If there are more consumers than partitions, some consumers have no partitions.</li>
</ul>
</dd>
</dl>

To learn more, see [Apache Kafka documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://kafka.apache.org/documentation.html){:new_window} and [Message Hub Kafka Java&trade; API developerWorks&reg; article ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/messaging/2016/03/03/message-hub-kafka-java-api/){:new_window}.


