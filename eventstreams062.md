---

copyright:
  years: 2015, 2018
lastupdated: "2018-10-29"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Choosing a Kafka client to use with {{site.data.keyword.messagehub}}
{: #kafka_reqs}

## Support for the official Apache Kafka client (Java) 

<table>
    <caption>Table 1. Kafka client support in Standard and Enterprise plans</caption>
      <tr>
	        <th></th>
		    <th>Standard Plan</th>
		    <th>Enterprise Plan</th>
        </tr>
	  		<tr>
			<td>**Kafka version on cluster**</td>
			<td>Kafka 0.10.2</td>
			<td>Kafka 1.1</td>
		</tr>
	  		<tr>
			<td>**Supported client versions**</td>
			<td>Kafka 0.10.x, or later</td>
			<td>Kafka 0.10.x, or later</td>
		</tr>
			<td>**Authentication requirements**</td>
			<td>Client must support authentication using the SASL Plain mechanism</td>
			<td>Client must support authentication using the SASL Plain mechanism and use the Server Name Indication (SNI) extension to the TLSv1.2 protocol</td>
		</tr>

</table>

To use the Kafka API with {{site.data.keyword.messagehub}} either choose one of official Java clients or a one of the [recommended third-party clients](/docs/services/EventStreams/eventstreams062.html#third_party_clients).

* Supported official Apache Kafka clients:
	* [Apache Kafka 1.1 client ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.apache.org/dyn/closer.cgi?path=/kafka/1.1.0/kafka_2.11-1.1.0.tgz){:new_window}
	* [Apache Kafka 0.11.0.X client ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.apache.org/dyn/closer.cgi?path=/kafka/0.11.0.1/kafka_2.11-0.11.0.1.tgz){:new_window}
	* [Apache Kafka 0.10.2.X client ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.apache.org/dyn/closer.cgi?path=/kafka/0.10.2.1/kafka_2.11-0.10.2.1.tgz){:new_window} 
	

<!--
* [Javadoc for the API ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://kafka.apache.org/0102/javadoc/index.html){:new_window} 
-->

## Recommended third-party clients
{: #third_party_clients}

If you can't run the official Java clients, we recommend running one of the following third-party clients, which are well-tested with {{site.data.keyword.messagehub}}:

* [node-rdkafka (Node.js) ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/Blizzard/node-rdkafka){:new_window} - tested up to V2.3.3. 

* [confluent-kafka-python (Python) ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/confluentinc/confluent-kafka-python){:new_window}

* [sarama (Go) ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/Shopify/sarama){:new_window}  

Other third-party clients might work with {{site.data.keyword.messagehub}} but we can't make any guarantees.

## Unsupported clients

### kafka-node
The kafka-node client does not fully support SASL authentication so cannot currently be used with {{site.data.keyword.messagehub}}.


### no-kafka 
The no-kafka client does not fully support SASL authentication so cannot currently be used with {{site.data.keyword.messagehub}}.

For information about how to configure your client to connect to {{site.data.keyword.messagehub}}, see [Configuring your client](/docs/services/EventStreams/eventstreams063.html).







