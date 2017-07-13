---

copyright:
  years: 2015, 2017
lastupdated: "2017-07-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Using the Kafka Java client
{: #kafka_using}

## To do: instructions for getting started, with links for more information
{: notoc}

## To do: simple send source and receive source in-line
{: notoc}

## How to use, download, and run the Java Kafka API sample
{: notoc}

The Java&trade; Kafka API sample is an example producer and consumer that is written in Java, which directly uses the Kafka API. You can run this sample locally or in {{site.data.keyword.Bluemix_short}}.

The sample code is in the [message-hub-samples GitHub project ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/message-hub-samples/tree/master/kafka-java-console-sample){:new_window}. Although the sample uses
the Kafka API to send and receive messages, the sample uses the {{site.data.keyword.messagehub}} Administration API to create the topic it sends messages to and receives messages from.

For more information about the setup and running of the sample, see the [README.md ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/message-hub-samples/tree/master/kafka-java-console-sample){:new_window}.

For a detailed walkthrough of how to run the sample, see [Getting started with {{site.data.keyword.messagehub}}](/docs/services/MessageHub/messagehub.html#getting_started_steps).

## How to use, download, and run the Liberty for Java sample
{: #liberty_sample notoc}

The Liberty for Java sample implements a simple application that is deployed onto the Liberty runtime. The application uses the Kafka API for {{site.data.keyword.messagehub}} to produce and consume messages.
The application also serves up a web front end that you can use for administration.

You can find the sample code in the [message-hub-samples GitHub project ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/message-hub-samples/tree/master/kafka-java-liberty-sample){:new_window}.

## How to migrate the Kafka client from 0.9.x to 0.10.x
{: #kafka_migrate notoc}


If you're using the Java clients, you can now use
the publicly available 0.10.x Kafka clients. You are strongly encouraged to move from 0.9.x to the
latest 0.10.x version (currently 0.10.2.1). Complete the following steps:

1. Delete the {{site.data.keyword.messagehub}} login jar module.
2. Change your ```jaas.conf``` file to the following: 
    ```
        KafkaClient {
          org.apache.kafka.common.security.plain.PlainLoginModule required
          serviceName="kafka"
            username="<your username>"
            password="<your password>";
        };
    ```
    {: codeblock}

3. Add this line to your consumer and producer properties: ```sasl.mechanism=PLAIN```

## Topic Admin APIs
{: #topic_admin notoc}

If you're using 0.10.2.1 or later, you can use APIs to create and delete topics. We've put some restrictions on the settings allowed when creating topics. Currently the only settings allowed are:
– cleanup.policy: Can be set to delete (default), compact or delete,compact
– retention.ms: Default is 24 hours. Minimum is 1 hour. Maximum is 30 days. It must be in muliples of hours.
Note:
If the cleanup policy is only compact, we automatically add delete but disable deletion based on time. Messages in the topic will be compacted up to 1GB before being deleted.


## Kafka Streams support

The updated Streams library takes advantage of the topic APIs and now works out of the box with Message Hub. All you need to do is specify your SASL credentials via sasl.jaas.config or a JAAS file and set replication.factor to 3.

For example:

    ```
    props.put(StreamsConfig.REPLICATION_FACTOR_CONFIG, "3");
    props.put(StreamsConfig.BOOTSTRAP_SERVERS_CONFIG, BOOTSTRAP_SERVERS);
    props.put("security.protocol","SASL_SSL");
    props.put("sasl.mechanism","PLAIN");
    props.put("ssl.protocol","TLSv1.2");
    props.put("ssl.enabled.protocols","TLSv1.2");
    props.put("sasl.jaas.config","org.apache.kafka.common.security.plain.PlainLoginModule required username=\"USERNAME\" password=\"PASSWORD\";");
    ```
    {: codeblock}

where BOOTSTRAP_SERVERS, USERNAME and PASSWORD are the values from your Message Hub service Credentials page in Bluemix.

<!-- 
new topic that includes content from existing topics about samples and migration
-->
