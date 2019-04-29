---

copyright:
  years: 2015, 2019
lastupdated: "2019-01-30"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}

# Configuring your Kafka API client
{: #kafka_api_client}

To connect to {{site.data.keyword.messagehub}}, the Kafka API uses one of the following sets of credential information: 
* the <code>kafka_brokers_sasl</code> credentials, and the <code>user</code> and <code>password</code> from
the [VCAP_SERVICES environment variable](/docs/services/EventStreams?topic=eventstreams-connecting#connect_standard_cf).
* the service key. For more information, see [Connecting to your cluster](/docs/services/EventStreams?topic=eventstreams-connecting).
{: shortdesc}



where USERNAME and PASSWORD are the values from your {{site.data.keyword.messagehub}} **Service Credentials** tab in {{site.data.keyword.Bluemix_notm}}.

If you use <code>sasl.jaas.config</code>, clients running in the same JVM can use different credentials. For more information, see
[Configuring Kafka clients ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://kafka.apache.org/documentation/#security_sasl_plain_clientconfig){:new_window}

The following example is a sample configuration file named <code>consumer.properties</code>:

```
key.deserializer=org.apache.kafka.common.serialization.StringDeserializer
value.deserializer=org.apache.kafka.common.serialization.StringDeserializer
#
client.id=kafka-java-console-sample-consumer
group.id=kafka-java-console-sample-group
#
security.protocol=SASL_SSL
sasl.mechanism=PLAIN
sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="USERNAME" password="PASSWORD";
ssl.protocol=TLSv1.2
ssl.enabled.protocols=TLSv1.2
ssl.endpoint.identification.algorithm=HTTPS
#
# please read the Kafka docs about this setting
auto.offset.reset=latest
```
{: codeblock}

<!--17/10/17 - Karen: following info duplicated at messagehub104 -->
## Using the sasl.jaas.config property (connecting and authenticating in a Java application)
{: #kafka_java notoc}
If you're using a Kafka client at 0.10.2.1 or later, you can use the <code>sasl.jaas.config</code> property for client configuration instead of a JAAS file. To connect to {{site.data.keyword.messagehub}}, set <code>sasl.jaas.config</code> as follows:
<pre>
<code>    sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required \
    username="USERNAME" \
    password="PASSWORD";</code>
</pre>
{:codeblock}

For an earlier Kafka client, you must use a JAAS configuration file to specify the credentials. This mechanism is less convenient therefore we recommend using the <code>sasl.jaas.config</code> property instead.
## Connecting and authenticating in an application other than Java
{: #kafka_notjava notoc}

The {{site.data.keyword.messagehub}} service currently
authenticates clients by using SASL PLAIN over TLS. Credentials are carried over an encrypted connection.
This is a new feature added in Kafka 0.10.0.X. 

Any client that supports Kafka 0.10 with SASL PLAIN
should work with {{site.data.keyword.messagehub}}. Example clients are as follows:

* [librdkafka ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/edenhill/librdkafka/){:new_window} 
* [confluent-kafka-python ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/confluentinc/confluent-kafka-python){:new_window} 




