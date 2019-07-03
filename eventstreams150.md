---

copyright:
  years: 2015, 2019
lastupdated: "2019-07-03"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka, MQ Light

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Migrating {{site.data.keyword.mql}} to Kafka on {{site.data.keyword.messagehub}} 
{: #migrate_mqlight}

Here are some key considerations for migrating applications from the {{site.data.keyword.mql}} API to the Apache Kafka API.

For many use cases, Kafka provides all the capabilities (and more) of the {{site.data.keyword.mql}} API. Kafka offers a richer feature set, higher performance, and scalability than the {{site.data.keyword.mql}} API. If you are porting an application consider whether a slightly higher investment in code change would allow you to access this in the future.

The following information details of the differences between the {{site.data.keyword.mql}} API and Kafka. However, at the highest level one key difference is the topic structure your application has been built around. 

Put simply the design and implementation of the {{site.data.keyword.mql}} API prioritizes light-weight topics that have little to no-cost to create, can be used a few times, and then discarded just as trivially. If you have designed your application around this premise or perhaps only using a topic as the destination for a single message, migrating to Kafka will require a different mindset.

The tradeoff for these lightweight topics is that {{site.data.keyword.mql}} topics can offer neither the throughput or scalability that can be achieved by using Apache Kafka.

To learn more about key Kafka concepts and the Kafka API, see 
[Apache Kafka concepts](/docs/services/EventStreams?topic=eventstreams-apache_kafka) and 
[Apache Kafka documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://kafka.apache.org/documentation/){:new_window}.

## Programming language support
Just because you're migrating between APIs doesn't mean you want to change everything. Your choice of programming language is likely based around the skills of your development team, as well as the other APIs that your application uses. The good news is that Apache Kafka has clients in [many languages ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cwiki.apache.org/confluence/display/KAFKA/Clients){:new_window}, far more than the {{site.data.keyword.mql}} API has been implemented in.

{{site.data.keyword.messagehub}} maintains a [list of clients](/docs/services/EventStreams?topic=eventstreams-kafka_clients#kafka_clients) that we regularly test and know to work well with the service. If you're using the {{site.data.keyword.mql}} API in Java, Node JS, or Python, {{site.data.keyword.messagehub}} has a recommended Kafka client for these programming languages. But what about the only other language that the {{site.data.keyword.mql}} API has been ported to? Ruby. {{site.data.keyword.messagehub}} doesn't currently have a recommended client for this language. We do, however, have customers who are using the [Zendesk Ruby client ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/zendesk/ruby-kafka), so if your application is written in Ruby, this might be a good starting point.


## Uses that are straightforward to migrate
First, let's take a look at some uses of the features of the {{site.data.keyword.mql}} API that are straightforward to migrate to Kafka. Hopefully you'll need to read no further than the use cases described in this section.

### Publish-subscribe
When an {{site.data.keyword.mql}} application uses non-shared subscriptions, subscribers each receive a copy of each message sent to a topic. This pattern of messaging is often referred to as publish-subscribe, and is straightforward to migrate to Kafka applications.

To implement publish-subscribe messaging using Kafka, use the Kafka producer to publish messages to a topic. Subscribers should use the [Kafka consumer to subscribe to the same topic](/docs/services/EventStreams?topic=eventstreams-kafka_using). You'll also need to ensure that each distinct subscriber specifies a different [consumer group](/docs/services/EventStreams?topic=eventstreams-consuming_messages#consumer-groups)  ID. By doing this, you'll ensure that each subscriber receives a copy of every message that is sent to the Kafka topic.

### Quality of service specified when sending messages
The {{site.data.keyword.mql}} API allows you to select between "at least once" and "at most once" quality of service when sending messages. Te quality of service determines whether error conditions can give rise to the occasional duplication (at least once) or non-delivery (at most once) of a message sent to the server. Kafka provides a range of qualities of service that include both "at least once", and "at most once" message delivery. In certain circumstances Kafka can exceed the {{site.data.keyword.mql}} API and also offer "exactly once" delivery.

The Kafka producer options that most closely correspond to {{site.data.keyword.mql}}'s "at-least-once" message delivery are:
* acks=all
* retries=2147483647
* max.in.flight.requests.per.connection=1

When configured with these options the Kafka producer responds to network errors by automatically sending messages to {{site.data.keyword.messagehub}} again. Messages are only considered sent when they are reliably stored in {{site.data.keyword.messagehub}}.

* To configure a Kafka producer to have similar behavior to the {{site.data.keyword.mql}} API's "at-most-once" message delivery, use the following producer configuration options:
* acks=0
* retries=0

The options instruct the Kafka producer to consider a message as having being successfully delivered as soon as it has made a single attempt to send the message to {{site.data.keyword.messagehub}}.


### Confirming the delivery of received messages
Consuming a message is a two step operation when using the {{site.data.keyword.mql}} API. First a subscribing application receives a copy of a message, then it must confirm the delivery of the message. When the delivery of a message is confirmed, the server knows it can safely discard its copy of the message. By using this protocol applications can receive a message:
* * at least once* *, by confirming delivery of a message after it has been processed) and also
* *at most once* *, by confirming a message before processing it.
It is also possible to enable automatic confirmation of messages received using the {{site.data.keyword.mql}} API. This simplifies your application code, but offers less control over when confirmation of message delivery occurs.

Kafka has a similar concept to confirming message delivery: [committing offsets](/docs/services/EventStreams?topic=eventstreams-consuming_messages#managing-offsets). Each message stored by Kafka is assigned a ever increasing numeric offset. Kafka consumers can tell Kafka (via a commit offset API) at what offset they want to start consuming from should they shut down or otherwise be interrupted. By deciding when to commit an offset value (before or after processing the message) an application can achieve similar "at least once" or "at most once" styles of message receipt. Kafka can also offer "exactly once" delivery of messages, as well as a lot more flexibility in deciding the point at which a consumer should start consuming from.


Kafka consumers also provide the convenience of [automatically committing offsets](/docs/services/EventStreams?topic=eventstreams-consuming_messages#committing-offsets-automatically). Again, this simplifies your application code but has the drawback that you get "mostly once" message delivery. Or to put it another way: infrequently your application might end up processing the same message twice, or perhaps even not processing a message at all if an application failure occurs. The Kafka consumer configuration options offer similar behaviour to {{site.data.keyword.mql}}'s automatic confirmation of messages are:
enable.auto.commit=true
auto-commit.interval.ms=10000


The first of these options tells the Kafka consumer to automatically commit offsets, and the second specifies the frequency (in milliseconds) with which the consumer will automatically commit. This offers more control than the {{site.data.keyword.mql}} API, which does not provide any settings to control how frequently message deliveries are confirmed.

### Encoding data as message properties
Sometimes it is useful to transport additional meta-data alongside the main payload of a message. For example, you might require the payload of a message to be in a fixed format to simplify its processing, but also care about the origin of this data when you are initially debugging your application. With the {{site.data.keyword.mql}} API you can associate a set of key/value pairs with each message.

Kafka also supports this use case using message headers, which are also key/value properties associated with a message. There is a slight difference here, in that the {{site.data.keyword.mql}} API allows you to associate structure with the value of a message property (e.g. this value is a number, this value is a string, etc). With Kafka message headers, the value associated with each key can only be an array of bytes. However it is trivial to use convention (e.g. keys ending with a suffix of "_str" encode their value as a UTF-8 string) or widely supported encodings such as JSON to encode the data type of a value.


### Programmatic administration
With the {{site.data.keyword.mql}} API you can create resources such as topics and subscriptions directly via the API. This has the advantage that it is straight forward and quick to deploy new applications. It does, however, mean that there is no point of control where an administrator can step in and manage the configuration and use of these resources.

Kafka also has an administration API for managing its topic resources. However, an advantage of using the {{site.data.keyword.messagehub}} deployment of Kafka is that permission to use this API is integrated with IBM Cloud's Identity and Access Management (IAM). This gives you the freedom to deploy applications that can create their own resources at run time, or to lock down these permissions so that resource creation can be tightly controlled.

It's worth noting that {{site.data.keyword.messagehub}} Apache Kafka far exceeds the {{site.data.keyword.mql}} API both in terms of providing UI and CLI administration tooling as well as by integrating with IAM to offer fine-grain authorization. Providing details of how IBM Cloud implements access management are a little outside the scope of this post, and also completely unnecessary since Paul has written an excellent blog post that tackles this exact subject.

### Message expiry
As the name suggestions, message expiry allows an {{site.data.keyword.mql}} application to decide the maximum length of time a message can be stored within the messaging system before it is discarded. Perhaps the data contained in the message is only valid for a short period of time, so there is no point in delivering the message if this duration is exceeded.


Kafka has the concept of log retention which defines a minimum amount of time messages are stored in a topic. You can specify a retention time when you create a topic using the {{site.data.keyword.messagehub}} UI, CLI, or administration programming interfaces. Something that can confuse new users is the rules that Kafka applies to decide when to delete unused log segments means that it is sometimes possible for messages to be stored longer than the retention period you specified. Think of Kafka's retention settings as being designed to bound how much data is stored on a topic, rather than providing an exact control on the lifetime of message data.


Another difference between Kafka's log retention and {{site.data.keyword.mql}} is that the latter allows different expiry times to be associated with each message. If your application really needs very accurate message expiry, or to apply message expiry on a per-message basis, then this can be achieved by storing the time-stamp when the message will expire as a message header. The receiving application can then compare this to the current time and decide whether it will process or discard the message. The down sides to this approach is that it adds complexity to your application, and also requires that your application spends time receiving messages that it will then discard.


### Subscriptions with wildcards
When subscribing, the {{site.data.keyword.mql}} API allows a topic pattern to be specified containing wildcard characters. This allows a single subscription to match messages published to a number of different topics. For example a subscription to 'a/+/z' can match messages published to 'a/b/z', 'a/c/z', etc..

Kafka also supports the notion of subscribing based on a wildcard. In this case you provide the Kafka subscribe call with a regular expression and Kafka will ensure that it is subscribed to all topics matching this expression. This includes subscribing to any new topics that are created and match the pattern.

### Subscription TTL
When an {{site.data.keyword.mql}} application makes a subscription, {{site.data.keyword.messagehub}} keeps track of which messages have been delivered to the application, and which have not. Storing this information takes up space, so subscription TTL allows the application to provide a hint about how long to store data for a subscriber that is disconnected. If the subscriber does not return and start consuming within the subscription TTL period, then the resources used by the subscription are reclaimed.

As we've already discussed, Kafka has a similar concept: committing consumer offsets. An {{site.data.keyword.messagehub}} Kafka deployment keeps each committed offset value for 7 days. This means that a consumer can be disconnected (and hence not committing any new offset values) for up to 7 days before it loses track of its position within a topic.

Even though {{site.data.keyword.messagehub}} stores committed offsets for 7 days, it is still possible for a consumer to find that the message corresponding to a committed offset is no longer being stored. This can happen if more data has been appended to a topic partition that it is configured to retain, or if the topic is configured to retain data for less than 7 days. You can choose how a Kafka consumer responds to their being no valid committed offset using the auto.offset.reset configuration property which can be set to one of the following values:
* latest - start consuming at the most recent offset in the topic partition.
* earliest - start consuming at the oldest offset in the topic partition.
* none - treat this situation as an error condition.









You can connect {{site.data.keyword.messagehub}} to {{site.data.keyword.cos_full}} to read data from an {{site.data.keyword.messagehub}} Kafka topic
and place the data into [{{site.data.keyword.IBM_notm}} Cloud Object Storage ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/services/cloud-object-storage?topic=cloud-object-storage-about#about){:new_window}.
{: shortdesc}

The connector allows you to archive data from the Kafka topics in {{site.data.keyword.messagehub}} to an instance of the [Cloud Object Storage service ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/services/cloud-object-storage?topic=cloud-object-storage-about#about){:new_window}. The connector consumes
batches of messages from Kafka and uploads the message data as objects to a bucket in the Cloud Object Storage service.
Complete the following steps to walk through the setup:

## Step 1. Install the pre-requisites
{: #step1_install_prereqs}
Ensure you have the following software and services installed:

* An {{site.data.keyword.messagehub}} instance - Standard or Enterprise plan. You will need to create credentials.
* An instance of the Cloud Object Storage service with at least one bucket
* An {{site.data.keyword.containerfull}} cluster. You can provision a free one for testing purposes. 

    You will also need CLI access to your cluster. For more information, see
 [Setting up the CLI and API](/docs/containers?topic=containers-cs_cli_install)
* A recent version of Kubectl (for example 1.14)
* [git ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://git-scm.com/downloads){:new_window}
* [Gradle 4.0, or later ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://gradle.org/install/){:new_window}
* Java 8 or later

## Step 2. Clone the kafka-connect repositories
{: #step3_clone project}

Clone the following two repositories that contain the required files:

* https://github.com/ibm-messaging/kafka-connect-ibmcos-sink

* https://github.com/ibm-messaging/kafka-connect


## Step 3. Create your Kafka Connect configuration
{: #step3_create_config}

1.You only have to set up this configuation once. {{site.data.keyword.messagehub}} stores it for future use.

    From the kafka-connect project, edit the <code>connect-distributed.properties</code> file and replace &lt;BOOTSTRAP_SERVERS&gt; in one place and &lt;APIKEY&gt; in three places with your {{site.data.keyword.messagehub}} credentials.

    Provide &lt;BOOTSTRAP_SERVERS&gt; as a comma-separated list. If they are not valid, you will get an error.

    Your &lt;APIKEY&gt; will appear in clear text on your machine but will be secret when pushed to IKS.

    If you have more than one replica (that is you're using a paid cluster), edit the <code>kafka-connect.yaml</code> file and edit the entry <code>replicas: 1</code>

    

2. Then run the following commands:
<br/>
    To create a secret: 
    ```
    kubectl create secret generic connect-distributed-config --from-file=connect-distributed.properties
   ```
    {: codeblock}
    <br/>
    To create a ConfigMap:
    ```
    kubectl create configmap connect-log4j-config --from-file=connect-log4j.properties
    ```
    {: codeblock}


