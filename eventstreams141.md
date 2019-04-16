---

copyright:
  years: 2015, 2019
lastupdated: "2019-01-14"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Choosing a Kafka client to use with {{site.data.keyword.messagehub}} Classic plan 
{: #kafka_clients_classic}

To use the Kafka API with {{site.data.keyword.messagehub}}, choose one of the following types of client:

* The official Java client. It is the best choice because it contains the latest features available for Apache Kafka.
* One of the [recommended third-party clients](/docs/services/EventStreams?topic=eventstreams-kafka_clients#clients_table).

For both types of client, we recommend always choosing the latest client version. 
{: shortdesc}

## Client requirements for connecting to Event Streams

To connect to {{site.data.keyword.messagehub}}, clients must support authentication using the SASL Plain mechanism and use the Server Name Indication (SNI) extension to the TLSv1.2 protocol.

The minimum Kafka protocol that we support is 0.10.
	
## Third-party clients
{: #third_party_clients_classic}

If you can't run the official Java clients, we recommend running one of the [recommended third-party clients](/docs/services/EventStreams?topic=eventstreams-kafka_clients#clients_table), which are all well-tested with {{site.data.keyword.messagehub}}. 

Other third-party clients that support the minimum set of client requirements might work with {{site.data.keyword.messagehub}}. However, we only test with and have experience of the recommended third-party clients.

## Support summary for all recommended clients
{: #client_summary_classic}

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
			<td>0.10.2 <p> For information about older clients, see [backward compatibility](/docs/services/EventStreams?topic=eventstreams-kafka_clients#compatibility).</p></td>
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

## Backward compatibility (Classic plan only)
{: #compatibility_classic}

For backward compatibility, you can use the Apache Kafka 0.9 Java client with the {{site.data.keyword.messagehub}} Classic plan. However, because of this client's age, we strongly discourage its use. If you choose to use this client version, you need an additional [login module ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/event-streams-samples/tree/master/kafka-0.9/message-hub-login-library).

Client versions earlier than 0.11 might experience degraded performance because of the additional protocol conversions that are required to connect to newer Kafka server versions.

<!--
## Unsupported clients

The following clients are not supported by {{site.data.keyword.messagehub}}:

### kafka-node
The kafka-node client does not fully support SASL authentication with the PLAIN mechanism so cannot currently be used with {{site.data.keyword.messagehub}}.


### no-kafka 
The no-kafka client does not fully support SASL authentication with the PLAIN mechanism so cannot currently be used with {{site.data.keyword.messagehub}}.

-->

## Connecting your client to {{site.data.keyword.messagehub}}
{: #connect_client_classic}

For information about how to configure your Java client to connect to {{site.data.keyword.messagehub}}, see [Configuring your client](/docs/services/EventStreams?topic=eventstreams-kafka_connect).








