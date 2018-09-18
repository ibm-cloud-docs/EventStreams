---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-29"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Apache Kafka concepts
{: #apache_kafka}

![Kafka architecture diagram.](kafka_overview.png "Diagram that shows a Kafka architecture. A producer is feeding into a Kafka topic over 3 partitions and the messages are then being subscribed to by consumers.")


The following list defines some Apache Kafka concepts:

<dl>
<dt>Server</dt>
<dd>A Kafka installation is made up of one or more individual server machines. These servers can be located in geographically disparate data centers. 
</dd>
<br/>
<dt>Cluster</dt>
<dd>Kafka runs as a cluster of one or more servers. The load is balanced across the cluster by distributing it amongst the servers.</dd>
<br/>
<dt>Message</dt>
<dd>The unit of data in Kafka. Each message is represented as a record, which comprises two parts: key and value. The key is commonly used for data about the message and the value is the body of the message. Kafka uses the terms record and message interchangeably. 

<p>Many other messaging systems also have a way of carrying other information along with the messages. Kafka 0.11 introduces record headers for this purpose, which are supported by the {{site.data.keyword.messagehub}} Enterprise plan. The {{site.data.keyword.messagehub}} Standard plan is currently based on Kafka 0.10.2.1, so it does not yet support record headers. </p> 

<p>Because many tools in the Kafka ecosystem (such as connectors to other systems) use only the value and ignore the key, it's best to put all of the message data in the value and just use the key for partitioning or log compaction. You should not rely on everything that reads from Kafka to make use of the key.</p>   </dd>
<dt>Topic</dt>
<dd>A named stream of messages.</dd>
<br/>
<dt>Partition</dt>
<dd>Each topic comprises one or more partitions. Each partition is an ordered list of messages. The messages on a partition are each given a monotonically increasing number called the offset. 
<p>Each partition has one server in the cluster that acts as the partition's leader and other servers that act as the followers.<p>
<p>If a topic has more than one partition, it allows data to be fed through in parallel to increase throughput by distributing the partitions across the cluster. The number of partitions also influences the balancing of workload among consumers.</p>
<p>For more information, see [Partition leadership](/docs/services/EventStreams/eventstreams118.html).</dd>
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
- [Producing messages](/docs/services/EventStreams/eventstreams112.html)
- [Consuming messages](/docs/services/EventStreams/eventstreams114.html) 
- [Partition leadership](/docs/services/EventStreams/eventstreams118.html) 
- [Apache Kafka documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://kafka.apache.org/documentation.html){:new_window} 


<!-- 27/06/18 Karen: removing - suggestion from James

## {{site.data.keyword.messagehub}} plans
{{site.data.keyword.messagehub}} is available as two different plans depending on your requirements: Standard and Enterprise.

* Choose the Standard plan if you want event ingest and distribution capabilities, where you pay for what you use and share infrastructure with others.
* Choose the Enterprise plan if data isolation, guaranteed performance, and increased retention are important considerations. 

For more information, see [Choosing your plan](/docs/services/EventStreams/eventstreams085.html).
-->



