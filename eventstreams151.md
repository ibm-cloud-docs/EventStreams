---

copyright:
  years: 2015, 2019
lastupdated: "2019-07-11e"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Migrating {{site.data.keyword.messagehub}} bridges to Kafka Connect
{: #migrate_bridges}
 
The {{site.data.keyword.messagehub}} Classic plan offers two bridges, one that takes data from Kafka and stores it in {{site.data.keyword.cos_full}} and one that takes data from IBM MQ and puts it into Kafka. These bridges allow you to connect systems by supplying just the configuration and do not require you to write any code. 
 
The bridges connect systems to and from Kafka. To those familiar with Kafka this sounds very similar to the Kafka Connect framework and the associated Connectors. {{site.data.keyword.messagehub}} is at its core Kafka so we wanted to align closely with Kafka and therefore are moving to Kafka Connect as a way to offer connections between systems. Consequently, we will not be supporting the older style bridges in the Enterprise and Standard plans.

To help our current users move to the more strategic Kafka Connect based Connectors, we have written an IBM COS Sink Connector and an IBM MQ Source Connector as replacements for the bridges.

Kafka Connect allows for far greater scaling than the bridges offered previously. Looking more closely at the COS Sink Connector, it offers the majority of bridge functionality and more. You can still configure how frequently it sinks to COS. The bridge allowed you to set an upload size threshold in kB; the analogous function in the Connector is to set "cos.object.records", which instructs the Connector to upload after receiving a set number of records. The COS Sink Connector also allows you to set a "cos.object.deadline.seconds" which is the same as the "uploadDurationThresholdSeconds" for the bridge. 

The only functionality that is missing is partitioning by ISO 8601 date. The date partitioning was used only if your messages were JSON and contained a timestamp field of a specific format, resulting in records being stored in COS as a file each day. This was rather restrictive and we've opted to make all the partitioning by offset for the COS Sink Connector. What this means is that files uploaded to the object store have the following naming scheme: 
 
<code>
&lt;topic_name&gt;/&lt;partition&gt;/&lt;beginning_offset&gt;-&lt;end_offset&gt;
</code>
{: codeblock} 

Although the COS Sink Connector does not include this feature, instead it offers far greater scaling and the ability to do exactly once delivery. For full details for the COS Sink Connector, see 
[Kafka Connect Sink Connector for IBM Cloud Object Storage. ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/kafka-connect-ibmcos-sink){:new_window}.

The MQ Source Connector offers all the functionality of the MQ bridge and more with improved security. For a full list of MQ Source Connector features, see [Kafka Connect source Connector for IBM MQ ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/kafka-connect-mq-source){:new_window}.
 
To run the Connectors you will need to run the Kafka Connect framework. We provide examples of how to do this in [Using Kafka Connect with {{site.data.keyword.messagehub}}](/docs/services/EventStreams?topic=eventstreams-kafka_connect). By running the Kafka Connect framework you have full control over how Connectors are scaled, how you monitor your Connectors, and access to a much richer set of metrics. For more information, see 
[Connect monitoring ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://kafka.apache.org/documentation.html#connect_monitoring){:new_window}.
