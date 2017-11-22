---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Consuming messages
{: #consuming_messages }


A consumer is an application that consumes streams of messages from Kafka topics and processes the feed of published messages. A consumer can subscribe to one or more topics or partitions.

Each partition is an ordered sequence of messages. Each of the messages in a partition is assigned a sequential ID number, called the offset, which uniquely identifies each message in the partition. These messages are retained for a configurable period of time, regardless of whether they have been consumed by an application. After that time the messages are discarded to free up space. If a topic has more than one partition, data can be distributed across the partitions to increase throughput. The number of partitions also influences the balancing of workload among consumers.

You can also have consumers in a consumer group, which is a named group of one or more consumers. Each consumer in the group reads messages from specific partitions in the topics that the consumer subscribes to. Each message is delivered to one consumer in the group and all messages with the same key are delivered to the same consumer.

You might find it useful to read this information in conjunction with [producing messages](/docs/services/MessageHub/messagehub112.html) in {{site.data.keyword.messagehub}}.

## Configuring consumer properties 
{: #configuring_consumer_properties }

To start working with consumers, create a configuration of the required properties to pass as parameters to kafkaConsumer. Change the properties in this example to suit your requirements:

<pre class="pre"><code>
props = new Properties();
        props.put("key.serializer","org.apache.kafka.common.serialization.ByteArraySerializer");
        props.put("value.serializer","org.apache.kafka.common.serialization.ByteArraySerializer");
        props.put("bootstrap.servers","kafka05-broker.us-south.bluemix.net:9094");
        props.put("group.id","test");
        props.put("enable.auto.commit","false");
        props.put("auto.offset.reset","earliest");
        props.put("auto.commit.interval.ms","1000");
        props.put("security.protocol","SASL_SSL");
        props.put("ssl.protocol","TLSv1.2");
        props.put("ssl.enabled.protocols","TLSv1.2");
        props.put("ssl.truststore.location","/usr/lib/j2re1.7-ibm/jre/lib/security/cacerts");
        props.put("ssl.truststore.password","password");
        props.put("ssl.truststore.type","JKS");
        props.put("ssl.endpoint.identification.algorithm","HTTPS");
		
</code></pre>
{: codeblock}

There are many configuration settings for the consumer, which control aspects of its behavior. Here are some of the most important ones:

| Name     |Description   | Valid values   | Default   |
|----------|---------|----------|---------|
|key.serializer     | The class used to serialize keys. | Java class that implements Serializer interface, such as org.apache.kafka.common.serialization.StringSerializer  |No default - you must specify a value|
|value.serializer     | The class used to serialize values. | Java class that implements Serializer interface, such as org.apache.kafka.common.serialization.StringSerializer  | No default - you must specify a value |
| | | | |

For more information about each property, see [Apache Kafka documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://kafka.apache.org/documentation.html){:new_window}


## Subscribe and assign methods of message consumption
{: #message_consumption }

You can define two different methods for message consumption: subscribe or assign. You cannot simultaneously subscribe and assign using the same consumer.

Use the subscribe method when you want to automatically consume all messages from a topic, regardless of which partition the messages are in. After subscribing, a rebalancing (a reassignment of partitions to a members of a consumer group) occurs. A consumer coordinates with a group to assign partitions, which happens automatically when data consumption starts.

Use the assign method when you want to manually define the topic and partition that messages are consumed from. 

## Consumer group rebalancing 
{: #consumer_group_rebalancing }

When one of the following changes take place in a consumer group, the group rebalances itself by shifting the assignment of partitions to each consumer to accommodate the change:

* a consumer joins the group
* a consumer leaves the group
* a consumer is considered as no longer functional by the group coordinator. For example, if the consumer has crashed
* new partitions are added to an existing topic

If you have a consumer group that has rebalanced, be aware that any consumer that has left the group will have its commits rejected until it rejoins the group. In this case, the consumer needs to rejoin the group, where it might be assigned a different partition to the one it was previously consuming from.

The assignment of partitions to consumers can change at every group rebalance.


##  Controlling the speed of message consumption 
{: #message_consumption_speed }

If you have problems with message handling caused by message flooding, you can set a consumer option to control the speed of message consumption. Use `fetch.max.bytes` to control how much data a call to `poll()` can return.

## Consumer groups and offsets
{: #consumer_groups }

When you create a consumer group, the group's offset setting is determined by the ```auto.offset.reset``` configuration property. When the consumer starts to process messages, it commits periodic offsets depending on the application's requirements. When the consumer group rebalances, the position is set to the last committed offset for that partition in the group.

If it's the first time you've started your client or the first time with a new group, you can use `auto.offset.reset` to specify where to start from as follows:
- `latest` (the default). Your consumer receives and consumes only messages that arrive after subscribing.
- `earliest`. Your consumer consumes all messages from the beginning.

If there is a problem with the consumer and it crashes before it can commit an offset for messages that have been processed, another consumer duplicates this work. Therefore, if you commit offsets frequently, you'll see fewer duplicates after a crash.

If you use a consumer group and commit, the consumer group automatically restarts where it left off. 


## Applications committing messages 
{: #apps_committing_messages }

If an application fails to commit a message and auto commit is set to false, messages are retrieved again from the last saved commit when the application restarts or when the group rebalances. If you commit an offset larger than the one you missed, the consumers continue as normal. 

If an application crashes after its consume but before the commit, you don't lose messages. In a consumer group each consumer fetches from a different partition. Therefore, if one of the consumers crashes, one of the other consumers takes over and restarts consuming from the partition that was formerly assigned to the crashed instance, starting from its last succesful commit.


## Code snippets - TBD
{: #consumer_code_snippets notoc}





