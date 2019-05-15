---

copyright:
  years: 2015, 2019
lastupdated: "2019-05-15"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}

# Using the Kafka API
{: #kafka_using}

Kafka clients exist in multiple languages and we provide instructions for some of those languages. You can use others but you'll need SASL PLAIN support to provide credentials. Additionally, if you're using the Enterprise plan, you'll also need to use the Server Name Indication (SNI) extension to the TLSv1.2 protocol.

For information about using the Kafka API on the Classic plan, see [Kafka API - Classic](/docs/services/EventStreams?topic=eventstreams-kafka_using_classic).

<table>
    <caption>Table 1. Kafka client support in Standard and Enterprise plans</caption>
      <tr>
	        <th></th>
		    <th>Standard Plan</th>
		    <th>Enterprise Plan</th>
        </tr>
	  		<tr>
			<td>**Kafka version on cluster**</td>
			<td>Kafka 2.2</td>
			<td>Kafka 1.1</td>
		</tr>
	  		<tr>
			<td>**Supported client versions**</td>
			<td>Kafka 0.10.x, or later</td>
			<td>Kafka 0.10.x, or later</td>
		</tr>
		<tr>
			<td>**Kafka Connect, Kafka Streams, and KSQL supported? **</td>
			<td>Yes</td>
			<td>Yes</td>
		</tr>

			<td>**Authentication requirements**</td>
			<td>Client must support authentication using the SASL Plain mechanism and use the Server Name Indication (SNI) extension to the TLSv1.2 protocol</td>
			<td>Client must support authentication using the SASL Plain mechanism and use the Server Name Indication (SNI) extension to the TLSv1.2 protocol</td>
		</tr>

</table>

For information about the V2.2 Producer and Consumer APIs, see 
[Kafka Producer API 2.2 ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://kafka.apache.org/22/javadoc/index.html?org/apache/kafka/clients/producer/KafkaProducer.html){:new_window} and 
[Kafka Consumer API 2.2 ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://kafka.apache.org/22/javadoc/index.html?org/apache/kafka/clients/consumer/KafkaConsumer.html){:new_window}. 


## Choosing a Kafka client to use with {{site.data.keyword.messagehub}}
{: #kafka_clients}

To use the Kafka API with {{site.data.keyword.messagehub}}, choose one of the following types of client:

* The official Java client. It is the best choice because it contains the latest features available for Apache Kafka.
* One of the [recommended third-party clients](/docs/services/EventStreams?topic=eventstreams-kafka_clients#clients_table).

For both types of client, we recommend always choosing the latest client version. 

### Client requirements for connecting to Event Streams

To connect to {{site.data.keyword.messagehub}}, clients must support authentication using the SASL Plain mechanism and use the Server Name Indication (SNI) extension to the TLSv1.2 protocol.

The minimum Kafka protocol that we support is 0.10.

	
### Third-party clients
{: #third_party_clients}

If you can't run the official Java clients, we recommend running one of the [recommended third-party clients](/docs/services/EventStreams?topic=eventstreams-kafka_clients#clients_table), which are all well-tested with {{site.data.keyword.messagehub}}. 
Other third-party clients that support the minimum set of client requirements might work with {{site.data.keyword.messagehub}}. However, we only test with and have experience of the recommended third-party clients.

### Support summary for all recommended clients
{: #client_summary}

<table id="clients_table">
    <caption>Table 2. Client support summary</caption>
      <tr>
		    <th id="client" scope="col">Client</th>
		    <th id="language" scope="col">Language</th>
			<th id="version" scope="col">Recommended version</th>
		    <th id="minimum version" scope="col">Minimum version supported [<sup>1</sup>](/docs/services/EventStreams?topic=eventstreams-kafka_clients#footnote1)</th>
			<th id="sample link" scope="col">Link to sample</th>
        </tr>
			<tr>
			<td colspan="3">**Official client**</td>
			</tr>
	  		<tr>
			<td>[Apache Kafka client ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://kafka.apache.org/downloads)</td>
			<td>Java</td>
			<td>Latest</td>
			<td>0.10.2 </td>
			<td>[Java console sample](/docs/services/EventStreams?topic=eventstreams-kafka_java_using)<br/>
			[Liberty sample ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/event-streams-samples/tree/master/kafka-java-liberty-sample)
			</td>
			</tr>
			<tr>
			<td colspan="3">**Third-party clients**</td>
			</tr>
	  		<tr>
			<td>[node-rdkafka ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/Blizzard/node-rdkafka)</td>
			<td>Node.js</td>
			<td>Latest</td>
			<td>2.2.2</td>
			<td>[Node.js sample ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/event-streams-samples/tree/master/kafka-nodejs-console-sample)</td>
		</tr>
		<tr>
			<td>[confluent-kafka-python ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/confluentinc/confluent-kafka-python)</td>
			<td>Python</td>
			<td>Latest</td>
			<td>0.11.0</td>
			<td>[Kafka Python sample ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/event-streams-samples/tree/master/kafka-python-console-sample)</td>
		</tr>
		<tr>
			<td>[confluent-kafka-go ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/confluentinc/confluent-kafka-go)</td>
			<td>Golang</td>
			<td>Latest</td>
			<td>0.11.0</td>
			<td></td>
		</tr>
		<tr>
			<td>[librdkafka ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/edenhill/librdkafka)</td>
			<td>C or C++</td>
			<td>Latest</td>
			<td>0.11.0</td>
			<td></td>
		</tr>

</table>
### Footnote
1. {: #footnote1}This version is the earliest that we have validated in continual testing. Typically, this is the initial version available within the last 12 months, but it might be newer if significant issues are known to exist


<!--
## Unsupported clients

The following clients are not supported by {{site.data.keyword.messagehub}}:

### kafka-node
The kafka-node client does not fully support SASL authentication with the PLAIN mechanism so cannot currently be used with {{site.data.keyword.messagehub}}.


### no-kafka 
The no-kafka client does not fully support SASL authentication with the PLAIN mechanism so cannot currently be used with {{site.data.keyword.messagehub}}.

-->

<br/>
### Connecting your client to {{site.data.keyword.messagehub}}
{: #connect_client}

For information about how to configure your Java client to connect to {{site.data.keyword.messagehub}}, see [Configuring your client](/docs/services/EventStreams?topic=eventstreams-kafka_connect).

## Configuring your Kafka API client
{: #kafka_api_client}

To establish a connection, clients must be configured to use SASL_SSL PLAIN over TLSv1.2 at a minimum and to require a username, and a list of the bootstrap servers. 

To retrieve the username, password, and list of bootstrap servers, a Service credentials object or service key is required for the service instance. For more information about creating these objects, see <link to Connecting to event Streams>
[Connecting to {{site.data.keyword.messagehub}}](/docs/services/EventStreams?topic=eventstreams-connecting).

From these objects:
* Use the ```kafka_brokers_sasl property``` as the list of bootstrap servers. Format this list as a comma-separated list of host:port entries. For example, ```host1:port1,host2:port2```. We recommend including details for all the hosts listed in the ```kafka_brokers_sasl``` property.
* Use the ```user``` and ```api_key``` properties as the username and password

For service instances on the Classic plan, this information is instead available from your application's VCAP_SERVICES environment variable. For more information, see [Connecting to {{site.data.keyword.messagehub}} - Classic](/docs/services/EventStreams?topic=eventstreams-connecting_classic).

For a Java client, the following example shows the minimum set of properties, where USERNAME, PASSWORD, and KAFKA_BROKERS_SASL should be replaced by the values retrieved previously.

```
bootstrap.servers=KAFKA_BROKERS_SASL
sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="USERNAME" password="PASSWORD";
security.protocol=SASL_SSL
sasl.mechanism=PLAIN
ssl.protocol=TLSv1.2
ssl.enabled.protocols=TLSv1.2
ssl.endpoint.identification.algorithm=HTTPS

# To send or receive messages, the following are also required
key.deserializer=org.apache.kafka.common.serialization.StringDeserializer
value.deserializer=org.apache.kafka.common.serialization.StringDeserializer
```
{: codeblock}

<br/>
Note, if you're using a Kafka client earlier than 0.10.2.1, the ```sasl.jaas.config``` property isn't supported and you must instead provide the client configuration in a JAAS configuration file. 

### Connecting and authenticating in an application other than Java
{: #kafka_notjava }

Any client that supports Kafka 0.10 with SASL PLAIN and TLSv1.2 should work with {{site.data.keyword.messagehub}}.

Note that the client must support the SNI extension to TLS where the server's hostname is included in the TLS handshake. 

Example clients are as follows:
* [librdkafka ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/edenhill/librdkafka/){:new_window} 
* [confluent-kafka-python ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/confluentinc/confluent-kafka-python){:new_window} 




 




