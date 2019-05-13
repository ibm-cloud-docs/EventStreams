---

copyright:
  years: 2015, 2019
lastupdated: "2019-05-13"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Kafka client support and recommendations
{: #client_support}

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
			<td>Kafka 1.1</td>
			<td>Kafka 2.2</td>
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

## Recommended third-party clients

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

For information about how to configure your client to connect to {{site.data.keyword.messagehub}}, see [Configuring your client](/docs/services/EventStreams?topic=eventstreams-kafka_connect).







