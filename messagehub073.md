---

copyright:
  years: 2015, 2018
lastupdated: "2018-01-16"

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

![Kafka architecture diagram.](kafka_architecture.png "Diagram that shows a Kafka architecture. Producers are feeding into a Kafka cluster and the messages are then being subscribed to by consumers.") 

The following list defines some Apache Kafka concepts:

<dl><dt>Cluster</dt>
<dd>Kafka runs as a cluster of one or more servers. The load is balanced across the cluster by distributing it amongst the servers.</dd>
<br/>
<dt>Topic</dt>
<dd>A named stream of messages.</dd>
<br/>
<dt>Partition</dt>
<dd>Each topic comprises one or more partitions. Each partition is an ordered list of messages. The messages on a partition are each given a monotonically increasing number called the offset. 

<p>If a topic has more than one partition, it allows data to be fed through in parallel to increase throughput by distributing the partitions across the cluster. The number of partitions also influences the balancing of workload among consumers.</p></dd>
<dt>Message</dt>
<dd>The unit of data in Kafka. Each message is represented as a record, which comprises two parts: key and value. The key is commonly used for data about the message and the value is the body of the message. Kafka uses the terms record and message interchangeably. 

<p>Many other messaging systems also have a way of carrying other information along with the messages. Kafka 0.11 introduces record headers for this purpose. {{site.data.keyword.messagehub}} is currently based on Kafka 0.10.2.1, so it does not yet support record headers.</p> 

<p>Because many tools in the Kafka ecosystem (such as connectors to other systems) use only the value and ignore the key, it's best to put all of the message data in the value and just use the key for partitioning or log compaction. You should not rely on everything that reads from Kafka to make use of the key.</p>   </dd>
<dt>Producer</dt>
<dd>A process that publishes streams of messages to Kafka topics. A producer can publish to one or
more topics and can optionally choose the partition that stores the data.<br/></dd>
<br/>
<dt>Consumer </dt>
<dd>A process that consumes messages from Kafka topics and processes the feed of messages. A consumer can consume from one or more topics or partitions.</dd>
<br/>
<dt>Consumer group</dt>
<dd>A named group of one or more consumers that together consume the messages from a set of topics. Each consumer in the group reads messages from specific partitions that it is assigned to. Each partition is assigned to one consumer in the group only.
<ul>
<li>If there are more partitions than consumers in a group, some consumers have multiple
partitions.</li>
<li>If there are more consumers than partitions, some consumers have no partitions.</li>
</ul>
</dd>
</dl>

To learn more, see the following information:
- [Producing messages](/docs/services/MessageHub/messagehub112.html)
- [Consuming messages](/docs/services/MessageHub/messagehub114.html) 
- [Partition leadership](/docs/services/MessageHub/messagehub118.html) 
- [Apache Kafka documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://kafka.apache.org/documentation.html){:new_window} 
- [Message Hub Kafka Java&trade; API developerWorks&reg; article ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/messaging/2016/03/03/message-hub-kafka-java-api/){:new_window}.


