---

copyright:
  years: 2015, 2019
lastupdated: "2019-10-01"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}

# Using the Kafka API on the Classic plan
{: #kafka_using_classic}

The Classic plan is deprecated. From November 1, 2019, you will no longer be able to provision new instances of the Classic Plan. <br/>However existing instances will continue to be supported.
From June 30, 2020, the Classic Plan will be retired and no longer supported. Any instance of the Classic Plan still provisioned at this date will be deleted. 
{:deprecated}

Kafka clients exist in multiple languages and we provide instructions for some of those languages. You can use others but you'll need SASL PLAIN support to provide credentials. Additionally, if you're using the Enterprise plan, you'll also need to use the Server Name Indication (SNI) extension to the TLSv1.2 protocol.

<table>
    <caption>Table 1. Kafka client support on Classic plan</caption>
      <tr>
	        <th></th>
		    <th>Classic Plan</th>
		    
        </tr>
	  		<tr>
			<td>**Kafka version on cluster**</td>
			<td>Kafka 1.1</td>
					</tr>
	  		<tr>
			<td>**Supported client versions**</td>
			<td>Kafka 0.10.x, or later</td>
		</tr>
		<tr>
			<td>**Kafka Connect, Kafka Streams, and KSQL supported? **</td>
			<td>Yes</td>
		</tr>

			<td>**Authentication requirements**</td>
			<td>Client must support authentication using the SASL Plain mechanism and use the Server Name Indication (SNI) extension to the TLSv1.2 protocol</td>
				</tr>

</table>

For information about the V1.1 Producer and Consumer APIs, see 
[Kafka Producer API 1.1 ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://kafka.apache.org/11/javadoc/index.html?org/apache/kafka/clients/producer/KafkaProducer.html){:new_window} and 
[Kafka Consumer API 1.1 ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://kafka.apache.org/11/javadoc/index.html?org/apache/kafka/clients/consumer/KafkaConsumer.html){:new_window}. 








