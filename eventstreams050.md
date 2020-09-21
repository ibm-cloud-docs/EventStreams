---

copyright:
  years: 2015, 2020
lastupdated: "2020-09-21"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: EventStreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}

# Using the Kafka API
{: #kafka_using}

Kafka provides a rich set of APIs and clients across a broad range of languages. For example:

* **Kafka's core API (Consumer, Producer, and Admin API)**<br/>
    Use to send and receive messages directly from one or more Kafka topics. 
	
	The Kafka Admin client provides a simple interface through the Kafka API for managing Kafka resources. It allows you to create, delete, and manage topics. You can also use the Admin client to manage consumer groups and configurations.
* **Streams API**<br/>
    A higher level stream processing API to easily consume, transform, and produce events between topics.
* **Connect API**<br/>
    A framework allowing re-usable or standard integrations to stream events into and out of external systems, such as databases.

The following table summarizes what you can use with {{site.data.keyword.messagehub}}:

<table>
    <caption>Table 1. Kafka client support in Standard, Enterprise, and Lite plans</caption>
      <tr>
	        <th></th>
		    <th>Enterprise Plan</th>
		    <th>Standard Plan</th>
		    <th>Lite Plan</th>
        </tr>
	  		<tr>
			<td>**Kafka version on cluster**</td>
			<td>Kafka 2.3</td>
			<td>Kafka 2.3</td>
			<td>Kafka 2.3</td>
		</tr>
	  		<tr>
			<td>**Supported client versions**</td>
			<td>Kafka 0.10.x, or later</td>
			<td>Kafka 0.10.x, or later</td>
			<td>Kafka 0.10.x, or later</td>
		</tr>
		<tr>
			<td>**Kafka Connect supported**</td>
			<td>Yes</td>
			<td>Yes</td>
			<td>No</td>
		</tr>
		<tr>
			<td>**Kafka Streams supported**</td>
			<td>Yes</td>
			<td>Yes</td>
			<td>No</td>
		</tr>
		<tr>
			<td>**ksqlDB supported**</td>
			<td>Yes</td>
			<td>No</td>
			<td>No</td>
		</tr>
		<tr>
			<td>**Authentication requirements**</td>
			<td>Client must support authentication using the SASL Plain mechanism and use the Server Name Indication (SNI) extension to the TLSv1.2 protocol</td>
			<td>Client must support authentication using the SASL Plain mechanism and use the Server Name Indication (SNI) extension to the TLSv1.2 protocol</td>
			<td>Client must support authentication using the SASL Plain mechanism and use the Server Name Indication (SNI) extension to the TLSv1.2 protocol</td>
		</tr>

</table>
<br/>

## Choosing a Kafka client to use with {{site.data.keyword.messagehub}}
{: #kafka_clients}

The official client for the Kafka API is written in Java, and as such contains the latest features and bug fixes. For more information about this API, see [Kafka Producer API 2.3 ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://kafka.apache.org/23/javadoc/index.html?org/apache/kafka/clients/producer/KafkaProducer.html){:new_window} and 
[Kafka Consumer API 2.3 ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://kafka.apache.org/23/javadoc/index.html?org/apache/kafka/clients/consumer/KafkaConsumer.html){:new_window}. 

For other languages, we recommend running one of the following clients, all of which are well-tested with {{site.data.keyword.messagehub}}.

### Support summary for all recommended clients
{: #client_summary}

<table id="clients_table">
    <caption>Table 2. Client support summary</caption>
      <tr>
		    <th id="client" scope="col">Client</th>
		    <th id="language" scope="col">Language</th>
			<th id="version" scope="col">Recommended version</th>
		    <th id="minimum version" scope="col">Minimum version supported [<sup>1</sup>](/docs/EventStreams?topic=EventStreams-kafka_clients#footnote1)</th>
			<th id="sample link" scope="col">Link to sample</th>
        </tr>
			<tr>
			<td colspan="3">**Official Apache Kafka client**</td>
			</tr>
	  		<tr>
			<td>[Apache Kafka client ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://kafka.apache.org/downloads)</td>
			<td>Java</td>
			<td>Latest</td>
			<td>0.10.2 </td>
			<td>[Java console sample](/docs/EventStreams?topic=EventStreams-kafka_java_using)<br/>
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
{: #footnote_clients notoc}

1. {: #footnote1 notoc}This version is the earliest that we have validated in continual testing. Typically, this is the initial version available within the last 12 months, but it might be newer if significant issues are known to exist

<br/>
If you can't run any of the clients listed, you can use other third-party clients that meet the following minimum requirements (for example, [librdkafka ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/edenhill/librdkafka/){:new_window}).
* Supports Kafka 0.10, or later
* Can connect and authenticate using SASL PLAIN with TLSv1.2
* Supports the SNI extensions for TLS where the server's hostname is includes in the TLS handshake
* Supports elliptic curve cryptography

However, we only test and have experience of the recommended third-party clients.

In all cases, the latest version of the client is recommended.
<br/>
### Connecting your client to {{site.data.keyword.messagehub}}
{: #connect_client}

For information about how to configure your Java client to connect to {{site.data.keyword.messagehub}}, see [Configuring your client](/docs/EventStreams?topic=EventStreams-kafka_using#kafka_api_client).

## Configuring your Kafka API client
{: #kafka_api_client}

To establish a connection, clients must be configured to use SASL PLAIN over TLSv1.2 at a minimum and to require a username, and a list of the bootstrap servers. TLSv1.2 ensures connections are encrypted and validates the authenticity of the brokers (to prevent man-in-the-middle attacks). SASL enforces authentication on all connections.

To retrieve the username, password, and list of bootstrap servers, a Service credentials object or service key is required for the service instance. For more information about creating these objects, see <link to Connecting to event Streams>
[Connecting to {{site.data.keyword.messagehub}}](/docs/EventStreams?topic=EventStreams-connecting).

From these objects:
* Use the <code>kafka_brokers_sasl property</code> as the list of bootstrap servers. Format this list as a comma-separated list of host:port entries. For example, <code>host1:port1,host2:port2</code>. We recommend including details for all the hosts listed in the <code>kafka_brokers_sasl</code> property.
* Use the <code>user</code> and <code>api_key</code> properties as the username and password

For service instances on the Classic plan, this information is available from your application's VCAP_SERVICES environment variable instead. For more information, see [Connecting to {{site.data.keyword.messagehub}} - Classic](/docs/EventStreams?topic=EventStreams-connecting_classic).

For a Java client, the following example shows the minimum set of properties, where USERNAME, PASSWORD, and KAFKA_BROKERS_SASL should be replaced by the values that you retrieved previously.

```
bootstrap.servers=KAFKA_BROKERS_SASL
sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="USERNAME" password="PASSWORD";
security.protocol=SASL_SSL
sasl.mechanism=PLAIN
ssl.protocol=TLSv1.2
ssl.enabled.protocols=TLSv1.2
ssl.endpoint.identification.algorithm=HTTPS
```
{: codeblock}

<br/>
Note, if you're using a Kafka client earlier than 0.10.2.1, the <code>sasl.jaas.config</code> property isn't supported and you must instead provide the client configuration in a JAAS configuration file. 
