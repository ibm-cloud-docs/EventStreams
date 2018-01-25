---

copyright:
  years: 2015, 2018
lastupdated: "2017-05-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Using a Kafka client
{: #kafka_using}

{{site.data.keyword.messagehub}}  is currently based on
Kafka 0.10.2.1. The earliest version of Kafka client that can connect to {{site.data.keyword.messagehub}}  is 0.9.0.0. and the latest version is
0.10.2.1. You cannot connect a Kafka client to {{site.data.keyword.messagehub}} if the version number of the Kafka client
exceeds the version number of Kafka we have deployed.

Kafka clients exist in multiple languages and we provide instructions for some of those languages. You can use others but you'll need SASL PLAIN support to provide credentials.
