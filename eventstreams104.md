---

copyright:
  years: 2015, 2019
lastupdated: "2019-04-15"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: EventStreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Using the Kafka Java client
{: #kafka_java_using}

<!-- 21/06/18 - removing until some content ready

## To do: instructions for getting started, with links for more information


## To do: simple send source and receive source in-line


## How to use, download, and run the Java Kafka API sample

-->

The Java&trade; Kafka API sample is an example producer and consumer that is written in Java, which directly uses the Kafka API. You can run this sample locally or in {{site.data.keyword.Bluemix_short}}.
{: shortdesc}

The sample code is in the [event-streams-samples GitHub project ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/event-streams-samples/tree/master/kafka-java-console-sample){:new_window}. Although the sample uses
the Kafka API to send and receive messages, the sample uses the {{site.data.keyword.messagehub}} Administration API to create the topic it sends messages to and receives messages from.

For more information about the setup and running of the sample, see the [README.md ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/event-streams-samples/tree/master/kafka-java-console-sample){:new_window}.

For a detailed walkthrough of how to run the sample, see [Getting started with {{site.data.keyword.messagehub}}](/docs/EventStreams?topic=EventStreams-getting_started#getting_started_steps).

## How to use, download, and run the Liberty for Java sample
{: #liberty_sample notoc}

The Liberty for Java sample implements a simple application that is deployed onto the Liberty runtime. The application uses the Kafka API for {{site.data.keyword.messagehub}} to produce and consume messages.
The application also serves up a web front end that you can use for administration.

You can find the sample code in the [event-streams-samples GitHub project ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/event-streams-samples/tree/master/kafka-java-liberty-sample){:new_window}.

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
[Configuring Kafka clients ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://kafka.apache.org/documentation/#security_sasl_plain_clientconfig){:new_window}.

For an earlier Kafka client, you must use a JAAS configuration file to specify the credentials. This mechanism is less convenient therefore we recommend using the <code>sasl.jaas.config</code> property instead.

<!--
23/04/18 - Karen: following migration info on production in messagehub084 
-->

## Migrating a Kafka client from 0.9.X or 0.10.X to later client versions
{: #kafka_migrate}


If you're using the Java clients, you can use
the publicly available Kafka clients at 0.10 or later. 

You are strongly encouraged to move from 0.9.X to the
latest version. You can download a Kafka client from 
[https://kafka.apache.org/downloads ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://kafka.apache.org/downloads){:new_window}.

<!--
For information about the implications of using a 0.9.X client, see 
[Backward compatibility](/docs/EventStreams?topic=EventStreams-kafka_clients#compatibility).
-->



### Migrating a Kafka client to 0.10.2.X or later versions

From 0.10.2, you can configure SASL authentication directly in the client's properties instead of using a JAAS file. This simplification allows you to run multiple clients in the same JVM using different sets of credentials, which is not possible with a JAAS file.

Complete the following steps:

1. Delete the JAAS file. Note that the JVM property java.security.auth.login.config=<PATH TO JAAS> is also no longer required.
2. Add the following to the client's properties:
    ```
	sasl.mechanism=PLAIN
    sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="USERNAME" password="PASSWORD";
	```

	where USERNAME and PASSWORD are the values from your {{site.data.keyword.messagehub}} **Service Credentials** tab in {{site.data.keyword.Bluemix_notm}}.



