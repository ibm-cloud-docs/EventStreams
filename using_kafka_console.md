---

copyright:
  years: 2015, 2022
lastupdated: "2022-04-29"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: EventStreams

---

{:external: target="_blank" .external}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}


# Using Kafka console tools with {{site.data.keyword.messagehub}}
{: #kafka_console_tools}

Apache Kafka comes with a variety of console tools for simple administration and messaging operations. You can use many of them with {{site.data.keyword.messagehub}}, although {{site.data.keyword.messagehub}} does not permit connection to its ZooKeeper cluster. As Kafka has developed, many of the tools that previously required connection to ZooKeeper no longer have that requirement.
{: shortdesc}

You can find these console tools in the `bin` directory of your Kafka download. You can download a client from [Apache Kafka downloads](http://kafka.apache.org/downloads){: external}.

To provide the SASL credentials to these tools, create a properties file based on the following example:

```config
    sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="USER" password="PASSWORD";
    security.protocol=SASL_SSL
    sasl.mechanism=PLAIN
    ssl.protocol=TLSv1.2
    ssl.enabled.protocols=TLSv1.2
    ssl.endpoint.identification.algorithm=HTTPS
```
{: codeblock}

Replace USER and PASSWORD with the values from your {{site.data.keyword.messagehub}} **Service Credentials** tab in the {{site.data.keyword.Bluemix_notm}} console.


## Console producer
{: #console_producer}

You can use the Kafka console producer tool with {{site.data.keyword.messagehub}}. You must provide a list of brokers and SASL credentials.

After you've created the properties file as described previously, you can run the console producer in a terminal as follows:

```bash
   kafka-console-producer.sh --broker-list KAFKA_BROKERS_SASL --producer.config CONFIG_FILE --topic TOPIC_NAME
```
{: codeblock}

Replace the following variables in the example with your own values:

- KAFKA_BROKERS_SASL with the value from your {{site.data.keyword.messagehub}} **Service Credentials** tab in the {{site.data.keyword.Bluemix_notm}} console, as a list of host:port pairs separated with commas (for example, `host1:port1,host2:port2`). 
- CONFIG_FILE with the path of the configuration file. 

You can use many of the other options of this tool, with the exception of those that require access to ZooKeeper.

## Console consumer
{: #console_consumer}

You can use the Kafka console consumer tool with {{site.data.keyword.messagehub}}. You must provide a bootstrap server and SASL credentials.

After you created the properties file as described previously, run the console consumer in a terminal as follows:

```bash
   kafka-console-consumer.sh --bootstrap-server KAFKA_BROKERS_SASL --consumer.config CONFIG_FILE --topic TOPIC_NAME 
```
{: codeblock}

Replace the following variables in the example with your own values:

- KAFKA_BROKERS_SASL with the value from your {{site.data.keyword.messagehub}} **Service Credentials** tab in the {{site.data.keyword.Bluemix_notm}} console, as a list of host:port pairs separated with commas (for example, `host1:port1,host2:port2`). 
- CONFIG_FILE with the path of the configuration file. 

You can use many of the other options of this tool, with the exception of those that require access to ZooKeeper.

## Consumer groups
{: #consumer_groups_tool}

You can use the Kafka consumer groups tool with {{site.data.keyword.messagehub}}. Because {{site.data.keyword.messagehub}} does not permit connection to its ZooKeeper cluster, some of the options are not available.

After you created the properties file as described previously, run the consumer groups tools in a terminal. For example, you can list the consumer groups as follows:

```bash
   kafka-consumer-groups.sh --bootstrap-server KAFKA_BROKERS_SASL --command-config CONFIG_FILE --list --timeout 60000
```
{: codeblock}

Replace the following variables in the example with your own values:

- KAFKA_BROKERS_SASL with the value from your {{site.data.keyword.messagehub}} **Service Credentials** tab in the {{site.data.keyword.Bluemix_notm}} console, as a list of host:port pairs separated with commas (for example, `host1:port1,host2:port2`). 
- CONFIG_FILE with the path of the configuration file.

Using this tool, you can also display details like the current positions of the consumers, their lag, and client-id for each partition for a group. For example:

```bash
   kafka-consumer-groups.sh --bootstrap-server KAFKA_BROKERS_SASL --command-config CONFIG_FILE --describe --group GROUP --timeout 60000
```
{: codeblock}

Replace GROUP in the example with the group name that you want to retrieve details for. 

Here is some sample output from running the **kafka-consumer-groups** tool:

```bash
GROUP              TOPIC    PARTITION  CURRENT-OFFSET  LOG-END-OFFSET  LAG         CONSUMER-ID      HOST          CLIENT-ID
consumer-group-1   foo        0          264             267            3          client-1-abc    example.com    client-1
consumer-group-1   foo        1          124             124            0          client-1-abc    example.com    client-1
consumer-group-1   foo        2          212             212            0          client-2-def    example.com    client-2
```
{: codeblock}

From the example above, you can see consumer group `consumer-group-1` has 2 consumer members consuming messages from topic `foo` with 3 partitions. It also shows that the consumer `client-1-abc` that is consuming from partition `0` is 3 messages behind, because the current offset of the consumer is `264` but the offset of the last message on partition `0` is `267`. 

## Topics
{: #topics_tool}

You can use the **kafka-topics** tool with {{site.data.keyword.messagehub}}. Ensure that you use V2.8 of the tool, because it does not require Zookeeper access.

A scenario where you might want to use **kafka-topics** is to find out information about your topics and their configuration in an existing cluster, so that you can recreate them in a new cluster. You can use the information that is output from **kafka-topics** to create the same named topics in the new cluster. For more information about how to create topics, see [Using the administration Kafka Java client API](/docs/EventStreams?topic=EventStreams-kafka_java_api) or the 
[ibmcloud es topic-create command](/docs/EventStreams?topic=EventStreams-cli_reference#ibmcloud_es). Alternatively, you can also use the IBM {{site.data.keyword.messagehub}} console.

Here is some sample output from running the **kafka-topics** tool:

```bash
   bin/kafka-topics.sh --bootstrap-server kafka03-prod01.messagehub.services.us-south.bluemix.net:9093 --command-config vcurr_dal06.properties --describe

Topic:sample-topic	PartitionCount:3	ReplicationFactor:3	 Configs:min.insync.replicas=2,unclean.leader.election.enable=true,retention.bytes=1073741824,segment.bytes=536870912,retention.ms=86400000
    Topic: sample-topic    Partition: 0    Leader: 0    Replicas: 0,2,1    Isr: 0,2,1
    Topic: sample-topic    Partition: 1    Leader: 1    Replicas: 1,2,0	   Isr: 0,2,1
    Topic: sample-topic    Partition: 2    Leader: 2    Replicas: 2,1,0	   Isr: 0,2,1
Topic:testtopic	 PartitionCount:1	 ReplicationFactor:3	Configs:min.insync.replicas=2,unclean.leader.election.enable=true,retention.bytes=1073741824,segment.bytes=536870912,retention.ms=86400000
    Topic: testtopic    Partition: 0    Leader: 0    Replicas: 0,2,1   Isr: 0,2
```
{: codeblock}

From the sample above, you can see that topic `sample-topic` has 3 partitions and a replication factor of 3. The example also shows which broker the leader of each partitions is on and which replicas are in sync (`Isr`). For example, the leader of partition `0`  is on broker `0`, the followers are on brokers `2` and `1` and all 3 replicas are in sync. If you look at the second topic `testtopic`, it has only 1 partition, replicated on brokers `0`, `2` and `1` but the in-sync replica list only shows `0` and `2`. This means the follower on broker `1` is falling behind and is therefore not in the `Isr` list. 


## Kafka Streams reset
{: #kafka_streams_reset}

You can use this tool with {{site.data.keyword.messagehub}} to reset the processing state of a Kafka Streams application, so you can reprocess its input from scratch. Before you run this tool, ensure that your Streams application is fully stopped.

For example:

```bash
   kafka-streams-application-reset.sh --bootstrap-servers KAFKA_BROKERS_SASL --config-file CONFIG_FILE --application-id APP_ID
```
{: codeblock}

Replace the following variables in the example with your own values:

- KAFKA_BROKERS_SASL with the value from your {{site.data.keyword.messagehub}} **Service Credentials** tab in the {{site.data.keyword.Bluemix_notm}} console, as a list of host:port pairs separated with commas (like `host1:port1,host2:port2`). 
- CONFIG_FILE with the path of the configuration file. 
- APP_ID with your Streams application ID.
