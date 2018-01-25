---

copyright:
  years: 2015, 2018
lastupdated: "2017-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Using Kafka console tools with {{site.data.keyword.messagehub}}
{: #kafka_console_tools }

Apache Kafka comes with a variety of console tools for simple administration and messaging operations. You can use many of them with {{site.data.keyword.messagehub}}, although {{site.data.keyword.messagehub}} does not permit connection to its ZooKeeper cluster. As Kafka has developed, many of the tools that previously required connection to ZooKeeper no longer have that requirement.

To provide the SASL credentials to these tools, create a properties file based on the following example:

<pre>
<code>
  sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="USER" password="PASSWORD";
  security.protocol=SASL_SSL
  sasl.mechanism=PLAIN
  ssl.protocol=TLSv1.2
  ssl.enabled.protocols=TLSv1.2
  ssl.endpoint.identification.algorithm=HTTPS
</code>
</pre>
{:codeblock}

Replace USER and PASSWORD with the values from your {{site.data.keyword.messagehub}} **Service Credentials** tab in the {{site.data.keyword.Bluemix_notm}} console.


## Console producer
{: #console_producer }

You can use the Kafka console producer tool with {{site.data.keyword.messagehub}}. You must provide a list of brokers and SASL credentials.

After you've created the properties file as described previously, you can run the console producer in a terminal as follows:

<pre>
<code>
  $ kafka-console-producer.sh --broker-list KAFKA_BROKERS_SASL --producer.config CONFIG_FILE --topic TOPIC_NAME
</code>
</pre>
{:codeblock}

Replace the following variables in the example with your own values:
* KAFKA_BROKERS_SASL with the value from your {{site.data.keyword.messagehub}} **Service Credentials** tab in the {{site.data.keyword.Bluemix_notm}} console, as a list of host:port pairs separated with commas (for example, `host1:port1,host2:port2`). 
* CONFIG_FILE with the path of the configuration file. 

You can use many of the other options of this tool, with the exception of those that require access to ZooKeeper.


## Console consumer
{: #console_consumer }

You can use the Kafka console consumer tool with {{site.data.keyword.messagehub}}. You must provide a bootstrap server and SASL credentials.

After you've created the properties file as described previously, you can run the console consumer in a terminal as follows:

<pre>
<code>
  $ kafka-console-consumer.sh --bootstrap-server KAFKA_BROKERS_SASL --consumer.config CONFIG_FILE --topic TOPIC_NAME 
</code>
</pre>
{:codeblock}

Replace the following variables in the example with your own values:
* KAFKA_BROKERS_SASL with the value from your {{site.data.keyword.messagehub}} **Service Credentials** tab in the {{site.data.keyword.Bluemix_notm}} console, as a list of host:port pairs separated with commas (for example, `host1:port1,host2:port2`). 
* CONFIG_FILE with the path of the configuration file. 

You can use many of the other options of this tool, with the exception of those that require access to ZooKeeper.


## Consumer groups
{: #consumer_groups_tool }

You can use the Kafka consumer groups tool with {{site.data.keyword.messagehub}}. Because {{site.data.keyword.messagehub}} does not permit connection to its ZooKeeper cluster, some of the options are not available.

After you've created the properties file as described previously, you can run the consumer groups tools in a terminal. For example, you can list the consumer groups as follows:

<pre>
<code>
  $ kafka-consumer-groups.sh --bootstrap-server KAFKA_BROKERS_SASL --command-config CONFIG_FILE --list --describe
</code>
</pre>
{:codeblock}

Replace the following variables in the example with your own values:
* KAFKA_BROKERS_SASL with the value from your {{site.data.keyword.messagehub}} **Service Credentials** tab in the {{site.data.keyword.Bluemix_notm}} console, as a list of host:port pairs separated with commas (for example, `host1:port1,host2:port2`). 
* CONFIG_FILE with the path of the configuration file.

Using this tool, you can also display details like the current positions of the consumers, their lag, and client-id for each partition for a group. For example:

<pre>
<code>
  $ kafka-consumer-groups.sh --bootstrap-server KAFKA_BROKERS_SASL --command-config CONFIG_FILE --describe --group GROUP
</code>
</pre>
{:codeblock}

Replace GROUP in the example with the group name that you want to retrieve details for. 


## Topics
{: #topics_tool }

You cannot use the Kafka topics tool `kafka-topics` with {{site.data.keyword.messagehub}} because the tool requires access to ZooKeeper.

However, you can administer topics using the {{site.data.keyword.messagehub}} dashboard in the {{site.data.keyword.Bluemix_notm}} console or using the REST API.


## Kafka Streams reset
{: #kafka_streams_reset }

You can use this tool with {{site.data.keyword.messagehub}} to reset the processing state of a Kafka Streams application, so you can reprocess its input from scratch. Before you run this tool, ensure that your Streams application is fully stopped.

For example:

<pre>
<code>
  $ kafka-streams-application-reset.sh --bootstrap-servers KAFKA_BROKERS_SASL --config-file CONFIG_FILE --application-id APP_ID
</code>
</pre>
{:codeblock}

Replace the following variables in the example with your own values:
* KAFKA_BROKERS_SASL with the value from your {{site.data.keyword.messagehub}} **Service Credentials** tab in the {{site.data.keyword.Bluemix_notm}} console, as a list of host:port pairs separated with commas (like `host1:port1,host2:port2`). 
* CONFIG_FILE with the path of the configuration file. 
* APP_ID with your Streams application ID.

