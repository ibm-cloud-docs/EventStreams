---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Using Kafka Connect with {{site.data.keyword.messagehub}}
{: #kafka_connect }

You can use Kafka Connect with {{site.data.keyword.messagehub}} and can run the workers inside or outside {{site.data.keyword.Bluemix_short}}.

Kafka Connect can run in either standalone or distributed mode. Standalone mode is intended for testing and temporary connections between systems. Distributed mode is more appropriate for production use. The configuration required to use {{site.data.keyword.messagehub}} with these two modes is slightly different.
{:shortdesc}

## Standalone worker configuration
{: #standalone_worker notoc}

You must provide the bootstrap servers and SASL credentials information in the worker properties file that you supply when you start a Kafka Connect standalone worker.

The standalone worker does not use any internal topics. Instead, it uses a file for storing offset information.

### Source connector
{: #source_connector notoc }

The following example lists the properties that you must provide in your properties file:

<pre>
<code>
  bootstrap.servers=KAFKA_BROKERS_SASL
  producer.sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="USER" password="PASSWORD";
  producer.security.protocol=SASL_SSL
  producer.sasl.mechanism=PLAIN
  producer.ssl.protocol=TLSv1.2
  producer.ssl.enabled.protocols=TLSv1.2
  producer.ssl.endpoint.identification.algorithm=HTTPS
</code>
</pre>
{:codeblock}

Replace KAFKA_BROKERS_SASL, USER, and PASSWORD with the values from your {{site.data.keyword.messagehub}} **Service Credentials** tab in the 
{{site.data.keyword.Bluemix_notm}} console.

### Sink connector
{: #sink_connector }

The following example lists the properties that you must provide in your properties file:

<pre>
<code>
  bootstrap.servers=KAFKA_BROKERS_SASL
  consumer.sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="USER" password="PASSWORD";
  consumer.security.protocol=SASL_SSL
  consumer.sasl.mechanism=PLAIN
  consumer.ssl.protocol=TLSv1.2
  consumer.ssl.enabled.protocols=TLSv1.2
  consumer.ssl.endpoint.identification.algorithm=HTTPS
</code>
</pre>
{:codeblock}

Replace KAFKA_BROKERS_SASL, USER, and PASSWORD with the values from your {{site.data.keyword.messagehub}} **Service Credentials** tab in the

{{site.data.keyword.Bluemix_notm}} console.

## Distributed worker configuration
{: #distributed_worker notoc}

You must provide the bootstrap servers and SASL credentials information in the properties file that you supply when you start the Kafka Connect distributed workers. The following example lists the properties that you must provide in your properties file:

<pre>
<code>
  bootstrap.servers=KAFKA_BROKERS_SASL
  sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="USER" password="PASSWORD";
  security.protocol=SASL_SSL
  sasl.mechanism=PLAIN
  ssl.protocol=TLSv1.2
  ssl.enabled.protocols=TLSv1.2
  ssl.endpoint.identification.algorithm=HTTPS
</code>
</pre>
{:codeblock}

Replace KAFKA_BROKERS_SASL, USER, and PASSWORD with the values from your {{site.data.keyword.messagehub}} **Service Credentials** tab in the {{site.data.keyword.Bluemix_notm}} console.

If you are want to use a source connector, you must also specify the SSL and SASL configuration for the producer as follows:

<pre>
<code>
  producer.sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="USER" password="PASSWORD";
  producer.security.protocol=SASL_SSL
  producer.sasl.mechanism=PLAIN
  producer.ssl.protocol=TLSv1.2
  producer.ssl.enabled.protocols=TLSv1.2
  producer.ssl.endpoint.identification.algorithm=HTTPS
</code>
</pre>
{:codeblock}

If you want to use a sink connector, you must also specify the SSL and SASL configuration for the consumer as follows:

<pre>
<code>
  consumer.sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="USER" password="PASSWORD";
  consumer.security.protocol=SASL_SSL
  consumer.sasl.mechanism=PLAIN
  consumer.ssl.protocol=TLSv1.2
  consumer.ssl.enabled.protocols=TLSv1.2
  consumer.ssl.endpoint.identification.algorithm=HTTPS
</code>
</pre>
{:codeblock}

In addition, Kafka Connect in distributed mode uses three topics internally. These topics are created automatically when a worker starts up, provided that you use Kafka Connect in Apache Kafka version 0.11 or later. You provide the names of the topics as configuration parameters. Ensure that the values are the same for all workers with the same `group.id` configuration value.

| Configuration               | Description                                                         |
| --------------------------- | ------------------------------------------------------------------- |
| `offset.storage.topic`      | Connector offsets topic                                             |
| `offset.storage.partitions` | Number of partitions for connector offsets topic (default 25) |
| `config.storage.topic`      | Connector configuration topic                                       |
| `status.storage.topic`      | Connector status topic                                              |
| `status.storage.partitions` | Number of partitions for connector status topic (default 5)          |

For example, you can use the following key-value pairs in your properties file:

<pre>
<code>
  offset.storage.topic=connect-offsets
  config.storage.topic=connect-configs
  status.storage.topic=connect-status
</code>
</pre>
{:codeblock}

Consider reducing the number of partitions if you are only making light use of Kafka Connect.



