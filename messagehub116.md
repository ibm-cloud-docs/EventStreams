---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Using Kafka console tools with {{site.data.keyword.messagehub}}
{: #kafka_console_tools }

Apache Kafka comes with a variety of console tools for simple administration and messaging operations. Many of them can be used with {{site.data.keyword.messagehub}}, although {{site.data.keyword.messagehub}} does not permit connection to its ZooKeeper cluster. As Kafka has matured, many of the tools that previously required connection to ZooKeeper no longer have that requirement.

You provide the SASL credentials to these tools using a properties file. Create a properties file based on the following example:

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

You can use the Kafka console producer with {{site.data.keyword.messagehub}}. You must provide a list of brokers and SASL credentials.

After you've created the properties file described previously, you can run the console producer in a terminal as follows:

<pre>
<code>
  $ kafka-console-producer.sh --broker-list KAFKA_BROKERS_SASL --producer.config CONFIG_FILE --topic TOPIC_NAME
</code>
</pre>
{:codeblock}

Replace KAFKA_BROKERS_SASL with the value from your {{site.data.keyword.messagehub}} **Service Credentials** tab in the {{site.data.keyword.Bluemix_notm}} console as a list of host:port pairs separated with commas (like `host1:port1,host2:port2`). Replace CONFIG_FILE with the path of the configuration file. You can use many of the other options of this tool, with the exception of those that require access to ZooKeeper.


## Console consumer

You can use the Kafka console consumer with {{site.data.keyword.messagehub}}. You must provide a bootstrap server and SASL credentials.

After you've created the properties file described above, you can run the console consumer in a terminal as follows:

<pre>
<code>
  $ kafka-console-consumer.sh --bootstrap-server KAFKA_BROKERS_SASL --consumer.config CONFIG_FILE --topic TOPIC_NAME
</code>
</pre>
{:codeblock}

Replace KAFKA_BROKERS_SASL with the value from your {{site.data.keyword.messagehub}} **Service Credentials** tab in the {{site.data.keyword.Bluemix_notm}} console as a list of host:port pairs separated with commas (like `host1:port1,host2:port2`). Replace CONFIG_FILE with the path of the configuration file. You can use many of the other options of this tool, with the exception of those that require access to ZooKeeper.


## Consumer groups tool

You can use the Kafka consumer groups tool with {{site.data.keyword.messagehub}}. Because {{site.data.keyword.messagehub}} does not permit connection to its ZooKeeper cluster, some of the options are not available.

After you've created the properties file described above, you can run the consumer groups tools in a terminal. For example, you can list the consumer groups as follows:

<pre>
<code>
  $ kafka-consumer-groups.sh --bootstrap-server KAFKA_BROKERS_SASL --command-config CONFIG_FILE --list
</code>
</pre>
{:codeblock}

Replace KAFKA_BROKERS_SASL with the value from your {{site.data.keyword.messagehub}} **Service Credentials** tab in the {{site.data.keyword.Bluemix_notm}} console as a list of host:port pairs separated with commas (like `host1:port1,host2:port2`). Replace CONFIG_FILE with the path of the configuration file.


## Topics tool

You cannot use the Kafka topics tool `kafka-topics` with {{site.data.keyboard.messagehub}} because the tool requires access to ZooKeeper.
