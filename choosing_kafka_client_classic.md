---

copyright:
  years: 2015, 2019, 2021
lastupdated: "2021-06-18"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: EventStreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:deprecated: .deprecated}

# Choosing a Kafka client to use with {{site.data.keyword.messagehub}} Classic plan 
{: #kafka_clients_classic}

The Classic plan is deprecated. From November 1, 2019, you can no longer provision new instances of the Classic Plan. <br/>However, existing instances will continue to be supported.
From June 30, 2020, the Classic Plan will be retired and no longer supported. Any instance of the Classic Plan still provisioned at this date will be deleted. 
{: deprecated}

To use the Kafka API with {{site.data.keyword.messagehub}}, choose one of the following types of client:

* The official Java client. It is the best choice because it contains the latest features available for Apache Kafka.
* One of the [recommended third-party clients](/docs/EventStreams?topic=EventStreams-kafka_clients#clients_table).

For both types of client, we recommend always choosing the latest client version. 
{: shortdesc}

## Client requirements for connecting to Event Streams

To connect to {{site.data.keyword.messagehub}}, clients must support authentication using the SASL Plain mechanism and use the Server Name Indication (SNI) extension to the TLSv1.2 protocol.

The minimum Kafka protocol that we support is 0.10.
	
## Third-party clients
{: #third_party_clients_classic}

If you can't run the official Java clients, we recommend running one of the [recommended third-party clients](/docs/EventStreams?topic=EventStreams-kafka_clients#clients_table), which are all well-tested with {{site.data.keyword.messagehub}}. 

Other third-party clients that support the minimum set of client requirements might work with {{site.data.keyword.messagehub}}. However, we only test with and have experience of the recommended third-party clients.

## Support summary for all recommended clients
{: #client_summary_classic}

| Client  | Language   | Recommended version   |Minimum version supported [<sup>1</sup>](/docs/EventStreams?topic=EventStreams-kafka_clients_classic#footnote_classic) |  Link to sample|
|---|---|---|---|---|
|**Official Apache Kafka client:**         |   |   |   |    |
| [Apache Kafka client ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://kafka.apache.org/downloads)  |  Java   | Latest  | 0.10.2 | [Java console sample](/docs/EventStreams?topic=EventStreams-kafka_java_using)  \n  \n  [Liberty sample ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/event-streams-samples/tree/master/kafka-java-liberty-sample) |
|**Third-party clients:**   |   |   |   |    |
|[node-rdkafka ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/Blizzard/node-rdkafka)   |  Node.js |  Latest|  2.2.2 | [Node.js sample ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/event-streams-samples/tree/master/kafka-nodejs-console-sample)|
|[confluent-kafka-python ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/confluentinc/confluent-kafka-python)|  Python |  Latest|  0.11.0 | [Kafka Python sample ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/event-streams-samples/tree/master/kafka-python-console-sample) |
| [confluent-kafka-go ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/confluentinc/confluent-kafka-go) |  Golang | Latest  |  0.11.0  |   |
| [librdkafka ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/edenhill/librdkafka) |  C or C++ | Latest  |  0.11.0  |   |
{: caption="Table 2. Client support summary" caption-side="top"}

### Footnote
{: #footnote_clients_classic notoc}

1. This version is the earliest that we have validated in continual testing. Typically, this is the initial version available within the last 12 months, but it might be newer if significant issues are known to exist. {: #footnote_classic}

## Backward compatibility (Classic plan only)
{: #compatibility_classic}

For backward compatibility, you can use the Apache Kafka 0.9 Java client with the {{site.data.keyword.messagehub}} Classic plan. However, because of this client's age, we strongly discourage its use. If you choose to use this client version, you need an additional [login module ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/event-streams-samples/blob/master/java/message-hub-liberty-sample/lib-message-hub/messagehub.login-1.0.0.jar).

Client versions earlier than 0.11 might experience degraded performance because of the additional protocol conversions that are required to connect to newer Kafka server versions.


## Connecting your client to {{site.data.keyword.messagehub}}
{: #connect_client_classic}

For information about how to configure your Java client to connect to {{site.data.keyword.messagehub}}, see [Configuring your client](/docs/EventStreams?topic=EventStreams-kafka_connect).








