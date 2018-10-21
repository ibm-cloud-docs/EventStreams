---

copyright:
  years: 2015, 2018
lastupdated: "2018-10-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Kafka client support and recommendation
{: #client_support}

## General Kafka client support overview

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

## Recommended client

### node-rdkafka - 
A NodeJS client for Apache Kafka that wraps the native librdkafka library. 
We recommend using the [node-rdkafka ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/Blizzard/node-rdkafka/blob/master/README.md){:new_window} client at 0.10.x, or later. This client is well tested with {{site.data.keyword.messagehub}} and demonstrates good performance with large amounts of traffic. 

However, the node-rdkafka client is not well supported on Windows and is not a pure JS client.


## Unsupported clients

### kafka-node
The kafka-node client does not fully support SASL authentication so cannot currently be used with {{site.data.keyword.messagehub}}.


### no-kafka 
The no-kafka client does not fully support SASL authentication so cannot currently be used with {{site.data.keyword.messagehub}}.

### sarama


For information about how to configure your client to connect to {{site.data.keyword.messagehub}}, see [Configuring your client](/docs/services/EventStreams/eventstreams063.html).







