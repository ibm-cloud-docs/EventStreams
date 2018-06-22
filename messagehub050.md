---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Using a Kafka client
{: #kafka_using}

If you're using the Java clients, you can use the publicly available Kafka clients at 0.10.x or later. 

Kafka clients exist in multiple languages and we provide instructions for some of those languages. You can use others but you'll need SASL PLAIN support to provide credentials. Additionally, if you're using the Enterprise plan, you'll also need to use the Service Name Identifaction (SNI) extension to the TLSv1.2 protocol.

## {{site.data.keyword.messagehub}} Standard plan

The Standard plan supports Apache Kafka version 0.10.2 with Kafka client version 0.10.x, or later, including the option to use Kafka Streams, Kafka Connect, and KSQL. 

The Kafka client must support authentication using the SASL Plain mechanism


## {{site.data.keyword.messagehub}} Enterprise plan

The Enterprise plan supports Apache Kafka version 1.1 with Kafka client version 0.10.x, or later, including the option to use Kafka Streams, Kafka Connect, and KSQL. 

The Kafka client must support authentication using the SASL Plain mechanism and use the Service Name Identifaction (SNI) extension to the TLSv1.2 protocol.


