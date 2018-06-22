---

copyright:
  years: 2015, 2018
lastupdated: "2018-05-04"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Using the Kafka Java client
{: #kafka_using}

<!-- 21/06/18 - removing until some content ready

## To do: instructions for getting started, with links for more information


## To do: simple send source and receive source in-line


## How to use, download, and run the Java Kafka API sample

-->

The Java&trade; Kafka API sample is an example producer and consumer that is written in Java, which directly uses the Kafka API. You can run this sample locally or in {{site.data.keyword.Bluemix_short}}.

The sample code is in the [message-hub-samples GitHub project ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/message-hub-samples/tree/master/kafka-java-console-sample){:new_window}. Although the sample uses
the Kafka API to send and receive messages, the sample uses the {{site.data.keyword.messagehub}} Administration API to create the topic it sends messages to and receives messages from.

For more information about the setup and running of the sample, see the [README.md ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/message-hub-samples/tree/master/kafka-java-console-sample){:new_window}.

For a detailed walkthrough of how to run the sample, see [Getting started with {{site.data.keyword.messagehub}}](/docs/services/MessageHub/index.html#getting_started_steps).

## How to use, download, and run the Liberty for Java sample
{: #liberty_sample notoc}

The Liberty for Java sample implements a simple application that is deployed onto the Liberty runtime. The application uses the Kafka API for {{site.data.keyword.messagehub}} to produce and consume messages.
The application also serves up a web front end that you can use for administration.

You can find the sample code in the [message-hub-samples GitHub project ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/message-hub-samples/tree/master/kafka-java-liberty-sample){:new_window}.

<!--
17/10/17 - Karen: following info duplicated at messagehub063 
-->

## Using the sasl.jaas.config property
{: #sasl_prop notoc}
If you're using a Kafka client at 0.10.2.1 or later, you can use the <code>sasl.jaas.config</code> property for client configuration instead of a JAAS file. To connect to {{site.data.keyword.messagehub}}, set <code>sasl.jaas.config</code> as follows:
<pre>
<code>    sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required \
    username="USERNAME" \
    password="PASSWORD";</code>
</pre>
{:codeblock}

where USERNAME and PASSWORD are the values from your {{site.data.keyword.messagehub}} **Service Credentials** tab in {{site.data.keyword.Bluemix_notm}}.

If you use <code>sasl.jaas.config</code>, clients running in the same JVM can use different credentials. For more information, see
[Configuring Kafka clients ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://kafka.apache.org/documentation/#security_sasl_plain_clientconfig){:new_window}

For an earlier Kafka client, you must use a JAAS configuration file to specify the credentials. This mechanism is less convenient therefore we recommend using the <code>sasl.jaas.config</code> property instead.

<!--
23/04/18 - Karen: following migration info on production in messagehub084 
-->

## Migrating a Kafka client from 0.9.X or 0.10.X to later client versions
{: #kafka_migrate}


If you're using the Java clients, you can use
the publicly available Kafka clients at 0.10 or later. You are strongly encouraged to move from 0.9.X to the
latest version. You can download a Kafka client from 
[https://kafka.apache.org/downloads ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://kafka.apache.org/downloads){:new_window} 



### Migrating a Kafka client to 0.10.2.X or later versions

From 0.10.2, you can configure SASL authentication directly in the client's properties instead of using a JAAS file. This simplicifcation allows you to run multiple clients in the same JVM using different sets of credentials, which is not possible with a JAAS file.

Complete the following steps:

1. Delete the JAAS file. Note that the JVM property java.security.auth.login.config=<PATH TO JAAS> is also no longer required.
2. If you're migrating from 0.9.X, delete the {{site.data.keyword.messagehub}} login jar module.
2. Add the following to the client's properties:
    ```
	sasl.mechanism=PLAIN
    sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="USERNAME" password="PASSWORD";
	```

	where USERNAME and PASSWORD are the values from your {{site.data.keyword.messagehub}} **Service Credentials** tab in {{site.data.keyword.Bluemix_notm}}.
	
	

### Migrating a Kafka client from 0.9.X to 0.10.0.X or 0.10.1.X

Complete the following steps:

1. Delete the {{site.data.keyword.messagehub}} login jar module.
2. Change your <code>jaas.conf</code> file to the following:
    ```
        KafkaClient {
          org.apache.kafka.common.security.plain.PlainLoginModule required
          serviceName="kafka"
            username="USERNAME"
            password="PASSWORD";
        };
    ```
    {: codeblock}

	where USERNAME and PASSWORD are the values from your {{site.data.keyword.messagehub}} **Service Credentials** tab in {{site.data.keyword.Bluemix_notm}}.
	
3. Add this line to your consumer and producer properties: <code>sasl.mechanism=PLAIN</code>

<!-- 
17/10/17 - Karen: following info duplicated at messagehub108
 -->
 
## APIs for topic administration
{: #topic_admin notoc}

If you're using a Kafka client at 0.11 or later, or Kafka Streams at 0.10.2.0 or later, you can use APIs to create and delete topics. We've put some restrictions on the settings allowed when you create topics. Currently, you can modify the following settings only:

<dl>
<dt>cleanup.policy</dt>
<dd>Set to <code>delete</code> (default), <code>compact</code> or <code>delete,compact</code>
<p>**Note:**
If the cleanup policy is <code>compact</code> only, we automatically add <code>delete</code> but disable deletion based on time. Messages in the topic are compacted up to 1 GB before being deleted.</p>
</dd>

<dt>retention.ms</dt>
<dd>The default retention period is 24 hours. The minimum is 1 hour and the maximum is
30 days. Specify this value as multiples of hours.

<p>**Note:**
In premium, this can be set to any value.</p>
</dd>

<dt>retention.bytes</dt>
<dd>The maximum size a partition (which consists of log segments) can grow to before we will discard old log segments to free up space.

<p>**Note:**
Premium only. This can be set to any value larger than 1MB.</p>
</dd>

<dt>segment.bytes</dt>
<dd>The segment file size for the log.

<p>**Note:**
Premium only. This can be set to any value larger than 100kB.</p>
</dd>

<dt>segment.index.bytes</dt>
<dd>The size of the index that maps offsets to file positions. 

<p>**Note:**
Premium only. This can be set to any value between 100kB and 2GB.</p>
</dd>

<dt>segment.ms</dt>
<dd>The period of time after which Kafka will force the log to roll even if the segment file isn't full. 

<p>**Note:**
Premium only. This can be set to any value between 5 minutes and 30 days</p>
</dd>
</dl>
<!--
new topic that includes content from existing topics about samples and migration
-->
