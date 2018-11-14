---

copyright:
  years: 2015, 2018
lastupdated: "2018-11-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Choosing a Kafka client to use with {{site.data.keyword.messagehub}}
{: #kafka_reqs}

To use the Kafka API with {{site.data.keyword.messagehub}}, choose one of the following types of client:

* an official Java client at 1.1 or later, for example, [Apache Kafka 1.1 client ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.apache.org/dyn/closer.cgi?path=/kafka/1.1.0/kafka_2.11-1.1.0.tgz){:new_window}.
	The official Java client offers the most because it contains the latest features available for Apache Kafka.

* one of the [recommended third-party clients](/docs/services/EventStreams/eventstreams062.html#clients_table).

For both types of client, we recommend choosing the latest client version. 

## Support summary for the official Apache Kafka client (Java)

<table>
    <caption>Table 1. Kafka client support in Standard and Enterprise plans</caption>
      <tr>
	        <th></th>
		    <th>Standard and Enterprise Plans</th>
		    <th></th>
        </tr>
	  		<tr>
			<td>**Kafka version on cluster**</td>
			<td>Kafka 1.1</td>
		</tr>
	  		<tr>
			<td>**Supported client versions**</td>
			<td>Kafka 1.1, or later</td>
		</tr>
			<td>**Authentication requirements**</td>
			<td>Client must support authentication using the SASL Plain mechanism and use the Server Name Indication (SNI) extension to the TLSv1.2 protocol</td>
		</tr>

</table>


<!--
* [Apache Kafka 0.11.0.X client ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.apache.org/dyn/closer.cgi?path=/kafka/0.11.0.1/kafka_2.11-0.11.0.1.tgz){:new_window}
* [Apache Kafka 0.10.2.X client ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.apache.org/dyn/closer.cgi?path=/kafka/0.10.2.1/kafka_2.11-0.10.2.1.tgz){:new_window} 
-->
	

	
## Third-party clients
{: #third_party_clients}

If you can't run the official Java clients, we recommend running one of the [recommended third-party clients](/docs/services/EventStreams/eventstreams062.html#clients_table), which are all well-tested with {{site.data.keyword.messagehub}}. The minimum Kafka protocol that we support is 0.10.

<!--
* [sarama (Go) ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/Shopify/sarama){:new_window}
-->  

Other third-party clients might work with {{site.data.keyword.messagehub}} but we can't make any guarantees.

## Support summary all supported clients
{: #client_summary}

<table id="clients_table">
    <caption>Table 2. Client support summary</caption>
      <tr>
		    <th>Client</th>
		    <th>Language</th>
			<th>Recommended version</th>
		    <th>Minimum version supported</th>
			<th>Link to sample</th>
        </tr>
			<tr>
			<td colspan="3">**Official client**</td>
			</tr>
	  		<tr>
			<td>[Apache Kafka 1.1 client ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.apache.org/dyn/closer.cgi?path=/kafka/1.1.0/kafka_2.11-1.1.0.tgz)</td>
			<td>Java</td>
			<td>Latest</td>
			<td>0.10.2</td>
			<td>[Java console sample ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/event-streams-samples/tree/master/kafka-java-console-sample)<br/>
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
			<td>2.3.3</td>
			<td>[Node.js sample ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/event-streams-samples/tree/master/kafka-nodejs-console-sample)</td>
		</tr>
		<tr>
			<td>[confluent-kafka-python ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/confluentinc/confluent-kafka-python)</td>
			<td>Python</td>
			<td>Latest</td>
			<td>0.11.6</td>
			<td>[Kafka Python sample ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/event-streams-samples/tree/master/kafka-python-console-sample)</td>
		</tr>
		<tr>
			<td>[confluent-kafka-go ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/confluentinc/confluent-kafka-go)</td>
			<td>Golang</td>
			<td>Latest</td>
			<td>0.11.6</td>
			<td></td>
		</tr>
		<tr>
			<td>[librdkafka ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/edenhill/librdkafka)</td>
			<td>C or C++</td>
			<td>Latest</td>
			<td>0.11.6</td>
			<td></td>
		</tr>

</table>

<!--
## Unsupported clients

The following clients are not supported by {{site.data.keyword.messagehub}}:

### kafka-node
The kafka-node client does not fully support SASL authentication with the PLAIN mechanism so cannot currently be used with {{site.data.keyword.messagehub}}.


### no-kafka 
The no-kafka client does not fully support SASL authentication with the PLAIN mechanism so cannot currently be used with {{site.data.keyword.messagehub}}.

-->

## Connecting your client to {{site.data.keyword.messagehub}}
{: #connect_client}

For information about how to configure your client to connect to {{site.data.keyword.messagehub}}, see [Configuring your client](/docs/services/EventStreams/eventstreams063.html).








