---

copyright:
  years: 2015, 2019
lastupdated: "2019-07-18a"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka, MQ Light

subcollection: EventStreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Migrating {{site.data.keyword.mql}} to Kafka 
{: #migrate_mqlight}

So you're thinking about migrating your applications from the {{site.data.keyword.mql}} API to the Apache Kafka API? Here are some key considerations to bear in mind.

For many use cases, Kafka provides all the capabilities (and more) of the {{site.data.keyword.mql}} API. Kafka offers a richer feature set, higher performance, and scalability than the {{site.data.keyword.mql}} API. If you are porting an application consider whether a slightly higher investment in code change would allow you to access this in the future.

The following information details of the differences between the {{site.data.keyword.mql}} API and Kafka. However, at the highest level one key difference is the topic structure that your application has been built around. Put simply the design and implementation of the {{site.data.keyword.mql}} API prioritizes lightweight topics that have little to no-cost to create, can be used a few times, and then discarded just as trivially. If you have designed your application around this premise or perhaps only using a topic as the destination for a single message, migrating to Kafka requires a different mindset.

The tradeoff for these lightweight topics is that {{site.data.keyword.mql}} topics can offer neither the throughput or scalability that can be achieved by using Apache Kafka.

To learn more about key Kafka concepts and the Kafka API, see 
[Apache Kafka concepts](/docs/EventStreams?topic=EventStreams-apache_kafka) and 
[Apache Kafka documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://kafka.apache.org/documentation/){: new_window}.

## Programming language support
Just because you're migrating between APIs doesn't mean you want to change everything. Your choice of programming language is probably based around the skills of your development team, as well as the other APIs that your application uses. The good news is that Apache Kafka has clients in [many languages ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cwiki.apache.org/confluence/display/KAFKA/Clients){: new_window}, far more than the {{site.data.keyword.mql}} API has been implemented in.

{{site.data.keyword.messagehub}} maintains a [list of clients](/docs/EventStreams?topic=EventStreams-kafka_clients#kafka_clients) that we regularly test and know to work well with the service. If you're using the {{site.data.keyword.mql}} API in Java, Node JS, or Python, {{site.data.keyword.messagehub}} has a recommended Kafka client for these languages. But what about the only other language that the {{site.data.keyword.mql}} API has been ported to, Ruby? {{site.data.keyword.messagehub}} doesn't currently have a recommended client for this language. We do, however, have customers who are using the [Zendesk Ruby client ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/zendesk/ruby-kafka), so if your application is written in Ruby, this might be a good starting point.


## Uses that are straightforward to migrate
First, let's take a look at some uses of the features of the {{site.data.keyword.mql}} API that are straightforward to migrate to Kafka. 

### Publish-subscribe
When an {{site.data.keyword.mql}} application uses non-shared subscriptions, subscribers each receive a copy of each message sent to a topic. This pattern of messaging is often referred to as publish-subscribe, and is straightforward to migrate to Kafka applications.

To implement publish-subscribe messaging using Kafka, use the Kafka producer to publish messages to a topic. Subscribers should use the [Kafka consumer ](/docs/EventStreams?topic=EventStreams-kafka_using) to subscribe to the same topic. You'll also need to ensure that each distinct subscriber specifies a different [consumer group](/docs/EventStreams?topic=EventStreams-consuming_messages#consumer-groups)  ID. By doing this, you'll ensure that each subscriber receives a copy of every message that is sent to the Kafka topic.

### Quality of service specified when sending messages
The {{site.data.keyword.mql}} API allows you to select between "at least once" and "at most once" quality of service when sending messages. The quality of service determines whether error conditions can cause the occasional duplication (at least once) or non-delivery (at most once) of a message sent to the server. Kafka provides a range of qualities of service that include both "at least once", and "at most once" message delivery. In certain circumstances Kafka can exceed the {{site.data.keyword.mql}} API and also offer "exactly once" delivery.

The Kafka producer options that most closely correspond to {{site.data.keyword.mql}}'s "at-least-once" message delivery are:
* acks=all
* retries=2147483647
* max.in.flight.requests.per.connection=1

When configured with these options the Kafka producer responds to network errors by automatically sending messages to {{site.data.keyword.messagehub}} again. Messages are considered sent only when they are reliably stored in {{site.data.keyword.messagehub}}.

To configure a Kafka producer to have similar behavior to the {{site.data.keyword.mql}} API's "at-most-once" message delivery, use the following producer configuration options:
* acks=0
* retries=0

These options instruct the Kafka producer to consider a message as successfully delivered as soon as it has made a single attempt to send the message to {{site.data.keyword.messagehub}}.


### Confirming the delivery of received messages
Consuming a message is a two step operation when using the {{site.data.keyword.mql}} API. First, a subscribing application receives a copy of a message, then it must confirm the delivery of the message. When the delivery of a message is confirmed, the server knows it can safely discard its copy of the message. By using this protocol applications can receive a message int he following two ways:
* _at least once_ by confirming delivery of a message after it has been processed).
* _at most once_ by confirming a message before processing it.<br/>

It is also possible to enable automatic confirmation of messages received using the {{site.data.keyword.mql}} API. This simplifies your application code, but offers less control over when confirmation of message delivery occurs.

Kafka has a similar concept to confirming message delivery: [committing offsets](/docs/EventStreams?topic=EventStreams-consuming_messages#managing-offsets). Each message stored by Kafka is assigned an ever increasing numeric offset. Kafka consumers can tell Kafka (using a commit offset API) at which offset they want to start consuming from if they shut down or are otherwise interrupted. By deciding when to commit an offset value (before or after processing the message) an application can achieve similar "at least once" or "at most once" styles of message receipt. Kafka can also offer "exactly once" delivery of messages, as well as a lot more flexibility in deciding the point at which a consumer should start consuming from.

Kafka consumers also provide the convenience of [automatically committing offsets](/docs/EventStreams?topic=EventStreams-consuming_messages#committing-offsets-automatically). Again, this simplifies your application code but has the drawback that you get "mostly once" message delivery. Infrequently your application might end up processing the same message twice, or perhaps even not processing a message at all if an application failure occurs. The Kafka consumer configuration options that offer similar behavior to {{site.data.keyword.mql}}'s automatic confirmation of messages are as follows:
* enable.auto.commit=true
* auto-commit.interval.ms=10000


enable.auto.commit=true tells the Kafka consumer to automatically commit offsets, and auto-commit.interval.ms=10000 specifies the frequency (in milliseconds) that the consumer automatically commits. This offers more control than the {{site.data.keyword.mql}} API, which does not provide any settings to control how frequently message deliveries are confirmed.

### Encoding data as message properties
Sometimes it's useful to transport additional metadata alongside the main payload of a message. For example, you might require the payload of a message to be in a fixed format to simplify its processing, but also care about the origin of this data when you are initially debugging your application. With the {{site.data.keyword.mql}} API you can associate a set of key-value pairs with each message.

Kafka also supports this use case using message headers, which are also key-value properties associated with a message. There is a slight difference here, in that the {{site.data.keyword.mql}} API allows you to associate structure with the value of a message property (for example, this value is a number, this value is a string, and so on). With Kafka message headers, the value associated with each key can only be an array of bytes. However, it is trivial to use convention (for example, keys ending with a suffix of <code>_str</code> encode their value as a UTF-8 string) or widely supported encodings such as JSON to encode the data type of a value.

### Programmatic administration
With the {{site.data.keyword.mql}} API you can create resources such as topics and subscriptions directly using the API. This has the advantage that it is straightforward and quick to deploy new applications. It does, however, mean that there is no point of control where an administrator can step in and manage the configuration and use of these resources.

Kafka also has an administration API for managing its topic resources. An advantage of using the {{site.data.keyword.messagehub}} deployment of Kafka is that permission to use this API is integrated with IBM Cloud's Identity and Access Management (IAM). This gives you the freedom to deploy applications that can create their own resources at runtime, or to lock down these permissions so that resource creation can be tightly controlled.

It's worth noting that {{site.data.keyword.messagehub}} Apache Kafka far exceeds the {{site.data.keyword.mql}} API both in terms of providing {{site.data.keyword.Bluemix_notm}} console and CLI administration tooling as well as by integrating with IAM to offer fine-grain authorization. To learn more about how {{site.data.keyword.Bluemix_notm}} implements access management, see 
[Enhanced Access Control on Apache Kafka Using {{site.data.keyword.messagehub}} for IBM Cloud ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/blog/enhanced-access-control-on-apache-kafka-using-event-streams-for-ibm-cloud).

### Message expiry
Message expiry allows an {{site.data.keyword.mql}} application to decide the maximum length of time that a message can be stored within the messaging system before it is discarded. Perhaps the data contained in the message is valid only for a short period of time, so there is no point in delivering the message if this duration is exceeded.

Kafka has the concept of log retention, which defines a minimum amount of time messages are stored in a topic. You can specify a retention time when you create a topic using the console, CLI, or administration programming interfaces. What can confuse new users are the rules that Kafka applies to decide when to delete unused log segments. These rules can mean that it is sometimes possible for messages to be stored longer than the retention period you specified. Think of Kafka's retention settings as being designed to bound how much data is stored on a topic, rather than providing an exact control on the lifetime of message data.

Another difference between Kafka's log retention and {{site.data.keyword.mql}} is that the latter allows different expiry times to be associated with each message. If your application really needs very accurate message expiry, or to apply message expiry on a per-message basis, you can achieve this by storing the timestamp of when the message expires as a message header. The receiving application can then compare this to the current time and decide whether to process or discard the message. The downsides to this approach are that it adds complexity to your application, and also requires that your application spends time receiving messages that it then discards.

### Subscriptions with wildcards
When subscribing, the {{site.data.keyword.mql}} API allows a topic pattern to be specified containing wildcard characters. This allows a single subscription to match messages published to a number of different topics. For example a subscription to <code>&apos;a/+/z&apos;</code> can match messages published to <code>&apos;a/b/z&apos;</code>, <code>&apos;a/c/z&apos;</code> and so on.

Kafka also supports the notion of subscribing based on a wildcard. In this case you provide the Kafka subscribe call with a regular expression and Kafka will ensure that it is subscribed to all topics matching this expression. This includes subscribing to any new topics that are created and match the pattern.

### Subscription TTL
When an {{site.data.keyword.mql}} application makes a subscription, {{site.data.keyword.messagehub}} keeps track of which messages have been delivered to the application, and which have not. Storing this information takes up space, so subscription TTL allows the application to provide an indication about how long to store data for a subscriber that is disconnected. If the subscriber does not return and start consuming within the subscription TTL period, the resources used by the subscription are reclaimed.

As previously discussed, Kafka has a similar concept: committing consumer offsets. An {{site.data.keyword.messagehub}} Kafka deployment keeps each committed offset value for 7 days. This means that a consumer can be disconnected (and hence not committing any new offset values) for up to 7 days before it loses track of its position within a topic.

Even though {{site.data.keyword.messagehub}} stores committed offsets for 7 days, it's still possible for a consumer to find that the message corresponding to a committed offset is no longer being stored. This can happen if more data has been appended to a topic partition than it is configured to retain, or if the topic is configured to retain data for less than 7 days. You can choose how a Kafka consumer responds to there being no valid committed offset using the <code>auto.offset.reset</code> configuration property,  which can be set to one of the following values:
* **latest** - start consuming at the most recent offset in the topic partition.
* **earliest** - start consuming at the oldest offset in the topic partition.
* **none** - treat this situation as an error condition.

## Uses that are more difficult to migrate
Now let's take a look at some uses of the {{site.data.keyword.mql}} API that are more difficult to migrate over to Kafka. In many cases this is because {{site.data.keyword.mql}} and Kafka have concepts that don't quite align. You might need to budget more time for migration, and perhaps be prepared to make some compromises that limit the degree that your migrated application scale to.

### Shared subscriptions
The {{site.data.keyword.mql}} concept of shared subscriptions allows a number of applications to all consume from the same queue of messages, albeit with somewhat loose message ordering guarantees. Kafka is based on a publish-subscribe messaging model, but has the concept of _consumer groups_ that allow one group of consumers to share out messages between themselves.

Although consumer groups might seem like a straightforward migration from shared subscriptions, there are some limitations to this approach to be aware of:
* At any given time, each Kafka client in a consumer group has one or more topic partitions uniquely assigned to it. This means that you can't usefully have more Kafka clients in a consumer group than the associated Kafka topic has partitions. If you do, some clients won't receive any messages. Kafka partitions are a finite resource. Although it's certainly possible to create a topic with hundreds or thousands of partitions, it is not practical to scale this approach to hundreds of thousands or millions of partitions. Therefore, using shared subscriptions to implement queued messaging is not practical if you expect to have a large number of consumers.
* When a Kafka consumer joins a consumer group, Kafka attempts to assign it one or more partitions. Because these partitions have to be taken from other consumers in the group (Kafka calls this rebalancing), message delivery to the group is paused briefly. If you have a dynamic set of clients that want to consume from a queue, using Kafka consumer groups is not a good approach because rebalances have an impact on throughput.
* Unlike {{site.data.keyword.mql}}, Kafka does not favor the consumers in a consumer group that can receive messages the fastest. With the {{site.data.keyword.mql}} API, if some consumers were able to receive messages from a shared subscription at a faster rate, those consumers could end up receiving a greater proportion of the overall number of messages sent to the corresponding topic. This is because the {{site.data.keyword.mql}} API selects which message is distributed to which consumer at the point a consumer tries to receive its next message. Kafka favors stronger ordering guarantees than the {{site.data.keyword.mql}} API and implements these by assigning a message to a topic partition at the point the message is produced. By default this assignment distributes messages evenly across all the partitions in a topic. Individual Kafka consumers in a consumer group are assigned one or more topic partitions to consume from in such a way that each partition is only being consumed from by one consumer in the group. Therefore, a consumer capable of receiving messages at a high rate might be limited by the availability of new messages in its set of assigned partitions, even though other consumers might not be able to keep up with the rate of arrival of new messages in their set of assigned partitions.

### Topic hierarchies
With {{site.data.keyword.mql}}, topics can be structured in a multi-level tree-like hierarchy. When a message is published to a particular topic name it is received both by subscribers that have subscribed to this topic, and also by any subscribers that are subscribed to a parent topic in the tree. A frequently cited example that illustrates this is an application that distributes the results of sports matches:
* Individual publishers send their results to a topic that contains the name of the sport. For example: <code>&apos;/sports/soccer&apos;</code> or 
<code>&apos;/sports/cricket&apos;</code>.
* A subscriber that is interested in only cricket results can subscribe to <code>&apos;/sports/cricket&apos;</code>.
* But a subscriber that wants to receive all of the sports results can subscribe to <code>&apos;/sports&apos;</code>.

Kafka uses a simpler "flat" structure for topics, where a subscriber receives only messages that are published to the exact topics that it is subscribed to. So what options are available to you if you need to migrate an {{site.data.keyword.mql}} application that uses topic hierarchies? Let's continue with our sports result distribution example:
* **Producing to multiple topics**<br/>
With this approach Kafka has three topics: <code>&apos;sports&apos;</code>,<code>&apos;soccer&apos;</code>, and <code>&apos;cricket&apos;</code>. Every time a producer wants to send a soccer result, it publishes the result twice: once to the <code>&apos;soccer&apos;</code> topic, and once to the <code>&apos;sports&apos;</code> topic. Likewise for producers that want to send a cricket result. Consumers can decide if they want to receive results for a particular sport or for all sports, depending on which topics they subscribe to.
* **Consuming from multiple topics**<br/>
For our example, this only requires two Kafka topics: <code>&apos;soccer&apos;</code>, and <code>&apos;cricket&apos;</code>. Each producer chooses the topic to use depending on the sport being played. Consumers can choose to subscribe to a particular sport, or they can subscribe to all the sports (potentially using a pattern-based subscription).
* **Using Kafka Streams to join two topics**<br/>
Kafka Streams is a framework that simplifies processing the data stored on Kafka topics. To satisfy our use case we'll require three topics: <code>&apos;sports&apos;</code>,<code>&apos;soccer&apos;</code>, and <code>&apos;cricket&apos;</code>. Our producers send <code>&apos;soccer&apos;</code> results to the <code>&apos;soccer&apos;</code> topic, and <code>&apos;cricket&apos;</code> results to the <code>&apos;cricket&apos;</code> topic. The consumers choose to consume from either the <code>&apos;cricket&apos;</code>, or <code>&apos;soccer&apos;</code> topics if they only care about one particular sport, or the <code>&apos;sports&apos;</code> topic if the want results for all of the sports. Kafka Streams is used to populate the <code>&apos;sports&apos;</code> topic by deploying an application that consumes from both the <code>&apos;cricket&apos;</code> and the <code>&apos;soccer&apos;</code> topic and publishes each result to the <code>&apos;sports&apos;</code> topic.


Well, that's certainly a lot of choice. Which option should you pick? Ultimately, it depends on your particular use case, but here are some guidelines to help you choose:
* Both producing to, and consuming from multiple topics is likely to be quicker to implement than to writing and deploying a Kafka Streams application and runtime. However using Kafka Streams offers greater flexibility.
* For "wide" topic hierarchies (in the sports example, this would be the case where we want to track results for tens or hundreds of different sports) producing to, and consuming from all the individual topics quickly becomes difficult to manage.
* Kafka does not preserve message order between topics, so if you subscribe to multiple topics the order in which a consumer receives messages does not necessarily match the order that the messages were produced in. If message ordering is important, producing to multiple topics, or using Kafka Streams allows the consumer to subscribe to a single topic where message ordering can be preserved.
* In general Kafka Streams offers a lot more flexibility than the other approaches, but has a higher up-front cost in writing and deploying a Streams application. If you are interested in this approach, see 
[Using Kafka Streams with Event Streams](/docs/EventStreams?topic=EventStreams-kafka_streams).

### Large numbers of topics and short-lived topics
The design and implementation of the {{site.data.keyword.mql}} API prioritizes lightweight topics that have little to no cost to create, can be used a few times, and then discarded just as trivially. The tradeoff is that these topics can offer neither the throughput nor scalability that can be achieved by using Apache Kafka.

If you have designed your application around creating large numbers of lightweight topics, or perhaps only using a topic as the destination for a single message, it might be difficult to adapt. Kafka topics, or more accurately the partitions that they are made up from, are not an unlimited resource. Although you can reasonably create hundreds, thousands, or even tens of thousands of partitions - Kafka is not well suited for use cases where you want to create very large numbers of topics. Creating and deleting Kafka topics is also a more expensive operation. For example, the pattern of creating a topic for the sole purpose of receiving a single reply message and deleting the topic after that message is received might be prohibitively expensive with Kafka.

### Client takeover
One of the more niche features of the {{site.data.keyword.mql}} API is client takeover. If a client tries to connect using a client ID that matches an already connected client, the already connected client is disconnected in favor of the newly arriving client. In theory this feature was designed to allow exclusive access to a topic. However, in practice, it often led to two instances of a client fighting for control - each stuck in a loop of interrupting the other instance, then being restarted by the runtime used for deployment.

Kafka doesn't implement this kind of exclusivity (and arguably, that should be considered a good thing). If you are really dependent on having only one producer or consumer at any given time, you can achieve this in a distributed way using a service that supports leadership election. For example: [Apache ZooKeeper ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://zookeeper.apache.org/){: new_window} or [etcd ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://etcd.io/){: new_window}.










