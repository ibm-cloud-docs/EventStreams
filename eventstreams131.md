---

copyright:
  years: 2015, 2018
lastupdated: "2018-10-17"

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

### node-rdkafka - a NodeJS client for Apache Kafka that wraps the native librdkafka library. 
We recommend using the [node-rdkafka ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/Blizzard/node-rdkafka/blob/master/README.md){:new_window} client at 0.10.x, or later. This client is well tested with {{site.data.keyword.messagehub}} and demonstrates good performance. 

However, the node-rdkafka client is not well supported on Windows.

 but that's not pure JS.

I think node-rdkafka would remain the customer-recommended option for deployment of node.js production applications that are pushing significant amounts of traffic, because it naturally receives more battle testing within Confluent (benefiting from all the other clients that share the common librdkafka) and Blizzard. 

You do need a client that fully supports SASL authentication and node-rdkafka is the only reliable one of those for nodejs

## Unsupported clients

### kafka-node
The kafka-node client does not support SASL authentication so cannot currently be used with {{site.data.keyword.messagehub}}.



### no-kafka 
The no-kafka client does not support SASL authentication so cannot currently be used with {{site.data.keyword.messagehub}}.

no-kafka is not a supported Kafka client in {{site.data.keyword.messagehub}} because it does not support SASL authentication.


To understand more about how {{site.data.keyword.messagehub}} works, see [About {{site.data.keyword.messagehub}}](/docs/services/EventStreams/eventstreams010.html).

To access other {{site.data.keyword.messagehub}} samples, including samples for Java and Python, see [{{site.data.keyword.messagehub}} samples ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/event-streams-samples){:new_window}.






