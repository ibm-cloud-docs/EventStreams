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

Each partition is an ordered sequence of messages, whose state cannot be altered after they have been created. Each of the messages in a partition is assigned a sequential ID number, called the offset, which uniquely identifies each message in the partition. These messages are all retained for a configurable period of time, regardless of whether they have been consumed by another application, after which the messages are discarded to free up space. (IIB)

You can also have consumers in a consumer group, which is a named group of one or more consumers. Each consumer in the group reads messages from specific partitions in the topics that the consumer subscribes to. Each message is delivered to one consumer in the group and all messages with the same key are delivered to the same consumer.

You might find it useful to read this information about consuming messages in conjunction with [producing messages in {{site.data.keyword.messagehub}}](/docs/services/MessageHub/messagehub112.html).

## Configuring consumer properties (Hugo https://developer.ibm.com/messaging/2016/03/03/message-hub-kafka-java-api/)
{: #configuring_consumer_properties }

To start working with consumers, create a configuration of the required properties to pass as parameters to kafkaConsumer. Change these properties according to your requirements:

```
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
		
```

There are many configuration settings for the consumer. You can control aspects of the producer including batching, retries, and message acknowledgement. Here are the most important ones:

| Name     |Description   | Valid values   | Default   |
|----------|---------|----------|---------|
|key.serializer     | The class used to serialize keys. | Java class that implements Serializer interface, such as org.apache.kafka.common.serialization.StringSerializer  |No default - you must specify a value|
|value.serializer     | The class used to serialize values. | Java class that implements Serializer interface, such as org.apache.kafka.common.serialization.StringSerializer  | No default - you must specify a value |
| | | | |

For more information about each property, see [Apache Kafka documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://kafka.apache.org/documentation.html){:new_window}


## Subscribe and assign methods of message consumption
{: #message_consumption }

You can define two different methods to use for message consumption: subscribe or assign. Below is a summary about the remarkable points of each one of them and when to use it:

Use the subscribe method when you want to consume all messages from a topic
This is automatically consumed from a topic, no matter in which partition(s) the messages are.
After subscribing, a re-balancing (re-assigning partition to a member) occurs. A consumer coordinates with a group to assign partitions, this happens automatically when consuming the data starts.
Define a List of strings of topics and then KafkaConsumer will subscribe to that list.

Use the assign method when you want to define the topic and partition where messages are consumed from.
This could be considered as a manual consumption as partition is programmatically defined for topic desired.
Define a List of TopicPartition and then KafkaConsumer will assign to that list.
It is not possible to subscribe and assign at the same time using the same consumer instance.

=============================
## Consumer group rebalancing (DE)
{: #consumer_group_rebalancing }

When one of the following changes happen to a consumer group, the group rebalances itself by shifting the assignment of partitions to each consumer to adapt to the change:

* a consumer joins the group
* a consumer leaves the group
* a consumer is considered no longer functioning by the group coordinator. For example, if the consumer has crashed
* new partitions are added to an existing topic

If you have a consumer group that has rebalanced, be aware that any consumer that has left the group will have its commits rejected until it rejoins the group. In this case, the consumer needs to rejoin the group, where it might be assigned a completely different partition(s) to the one it was previously consuming from

==============================

## Consumer groups and offsets
{: #consumer_groups }


When you create a consumer group, the group's offset setting is determined by the ```auto.offset.reset``` configuration property. When the consumer starts to process messages, it commits periodic offsets depending on the application's requirements. When the consumer group rebalances, the position is set to the last committed offset for that partition in the group.

If there is a problem with the consumer and it crashes before it can commit an offset for messages that have been processed, another consumer duplicates this work. Therefore, if you commit offsets frequently, you'll see fewer duplicates after a crash.

====================================


## Reading messages from consumer groups (MM)
{: #reading_consumer_groups }

If you use a consumer group and commit, the consumer group automatically restarts where it left off. 

If it's the first time you've started your client (or with a new group), you can use `auto.offset.reset` to specify where to start from as follows:
- `latest` (the default). Your consumer receives only messages that arrive after subscribing
- `earliest`, you consumer consumes all messages from the beginning


=============================================================

##  Controlling the speed of message consumption (MM)
{: #message_consumption_speed }

If you want to set consumer options to control the speed of message consumption to prevent flooding of messages, which causes problems with message handling, you can use `fetch.max.bytes` to control how much data a call to `poll()` can return.

=======================================================

## Application committing messages (EC)
{: #apps_committing_messages }

If an app fails to commit a message and auto commit is set to false, at restart of the app or when the group rebalances, messages are retrieved again from the last saved commit. If you happen to commit an offset larger than the one you missed, the consumers continue as normal. 

If an app instance crashes after its consume but before the commit, you don't lose messages. In a consumer group each consumer instance fetches from a different partition. Therefore, if one of the consumer instances crashes, one of the other instances takes over and restarts consuming from the partition that was formerly assigned to the crashed instance, starting from its last succesful commit.


======================================================
Producing messages topic



In the programming interfaces, a message is actually called a record. For example, the Java class org.apache.kafka.clients.producer.ProducerRecord is used to represent a message from the point of view of the producer API. The terms _record_ and _message_ can be used interchangeably, but essentially a record is used to represent a message.

Each topic comprises one or more partitions. Each partition is an ordered list of messages. If a topic has more than one partition, data can be distributed across the partitions to increase throughput. The number of partitions also influences the balancing of workload among consumers.

The Kafka cluster comprises several servers. The load is balanced across the cluster by distributing the work amongst the servers. Each partition has one server that acts as the partition's leader and other servers that act as the followers. All produce and consume requests for the partition are handled by the leader. The followers replicate the partition data from the leader with the aim of keeping up with the leader. If a follower is keeping up with the leader of a partition, the follower's replica is in sync. When the leader for a partition fails, one of the followers with an in-sync replica automatically takes over as the partition's leader. In practice, a server is the leader for some partitions and the follower for others. The leadership of partitions is dynamic and changes as servers come and go.

A producer does not need to take specific actions to handle the change in the leadership of a partition. The producer automatically reconnects to the new leader, although you will see increased latency while the cluster settles.
 
When a producer connects to Kafka, it makes an initial bootstrap connection, which can be to any of the servers in the cluster. The producer requests the partition and leadership information about the topic that it wants to publish to. Then the producer establishes another connection to the partition leader and can begin to publish messages. These actions happen automatically behind the scenes when your producer connects to the Kafka cluster.
 
When a message is sent to the partition leader, that message is not immediately available to consumers. The leader appends the record for the message to the partition, assigning it the next offset number for that partition. After all the followers for the in-sync replicas have replicated the record and acknowledged that they've written the record to their replicas, the record is now committed. The message is available for consumers.

Each message is represented as a record which comprises two parts: key and value. The key is commonly used for data about the message, while the value is the body of the message. Because many tools in the Kafka ecosystem such as connectors to other systems use only the value and ignore the key, it's best to put all of the message data in the value and just use the key for partitioning or log compaction. You should not rely on everything that reads from Kafka to make use of the key.

Many other messaging systems also have a way of carrying other information along with the messages. Kafka 0.11 introduces record headers for this purpose. {{site.data.keyword.messagehub}} is currently based on Kafka 0.10.2.1, so it does not yet support record headers.


## Message ordering
{: #message_ordering notoc}

Kafka generally writes messages in the order that they are sent by the producer. However, there are situations where retries can cause messages to be duplicated or reordered.
 
If you want a sequence of messages to be sent in order, it's very important to ensure that they are all written to the same partition. The typical way to do this is use the same key for all the messages.
 
The producer is also able to retry sending messages automatically. It's often a good idea to enable this retry feature because the alternative is that your application code has to perform any retries itself. The combination of batching in Kafka and automatic retries can have the effect of duplicating messages and reordering them.
 
For example, if you publish a sequence of three messages <M1, M2, M3> on a topic. The records might all fit within the same batch, so they're actually all sent to the partition leader together. The leader then writes them to the partition and replicates them as separate records. In the case of a failure, it's possible that M1 and M2 are added to the partition, but M3 is not. The producer doesn't receive an acknowledgement, so it retries sending <M1, M2, M3>. The new leader simply writes M1, M2 and M3 onto the partition, which now contains <M1, M2, M1, M2, M3>, where the duplicated M1 actually follows the original M2. if you restrict the number of requests inflight to each broker to just one, you can prevent this reordering. You might still find a single record is duplicated such as <M1, M2, M2, M3>, but you'll never get out of order sequences. In Kafka 0.11 (not yet available in {{site.data.keyword.messagehub}}), you can use the idempotent producer feature to prevent the duplication of M1 also.
 
It's normal practice with Kafka to write the applications to handle occasional message duplicates because the performance impact of only having a single request in flight is significant.


## Code snippets
{: #code_snippets notoc}

To connect to {{site.data.keyword.messagehub}}, you first need to build the set of configuration properties. All connections to {{site.data.keyword.messagehub}} are secured using TLS and user/password authentication, so you need at least these properties. Replace KAFKA_BROKERS_SASL, USER, and PASSWORD with your own service credentials:

```
Properties props = new Properties();
 props.put("bootstrap.servers", KAFKA_BROKERS_SASL);
 props.put("sasl.jaas.config", "org.apache.kafka.common.security.plain.PlainLoginModule required username=\"USER\" password=\"PASSWORD\";");
 props.put("security.protocol", "SASL_SSL");
 props.put("sasl.mechanism", "PLAIN");
 props.put("ssl.protocol", "TLSv1.2");
 props.put("ssl.enabled.protocols", "TLSv1.2");
 props.put("ssl.endpoint.identification.algorithm", "HTTPS");
```

To send a message, you'll also need to specify serializers for the keys and values:

```
 props.put("key.serializer", "org.apache.kafka.common.serialization.StringSerializer");
 props.put("value.serializer", "org.apache.kafka.common.serialization.StringSerializer");
```

Then use a KafkaProducer to send messages, where each message is represented by a ProducerRecord. Don't forget to close the KafkaProducer when you're finished. This code just sends the message but it doesn't wait to see whether the send succeeded.

```
 Producer<String, String> producer = new KafkaProducer<>(props);
 producer.send(new ProducerRecord<String, String>("T1", "key", "value"));
 producer.close();
 ```
 
The send() method is asynchronous and returns a Future that you can use to check its completion:

```
 Future<RecordMetadata> f = producer.send(new ProducerRecord<String, String>("T1", "key", "value"));
// Do some other stuff
// Now wait for the result of the send
 RecordMetadata rm = f.get();
 long offset = rm.offset; 
```

Alternatively, you can supply a callback when sending the message:

```
producer.send(new ProducerRecord<String,String>("T1","key","value", new Callback() {
          public void onCompletion(RecordMetadata metadata, Exception exception) {
                     // This is called when the send completes, either successfully or with an exception
          }
});
```

For more information, see the [Javadoc for the Kafka client ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://kafka.apache.org/0102/javadoc/index.html){:new_window}, which is very comprehensive. 



