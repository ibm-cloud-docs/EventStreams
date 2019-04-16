---

copyright:
  years: 2015, 2019
lastupdated: "2018-06-06"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Choosing between the three APIs on the Classic plan 
{: #choose_api_classic}

{{site.data.keyword.messagehub}} supports three APIs on the Classic plan. Here's some information to help you choose which is most appropriate:
{: shortdesc}

## Why use the Kafka API?
{: #why_kafka_classic notoc}

There are a few reasons that you might choose to use the Kafka API over the other interfaces provided by {{site.data.keyword.messagehub}}. These reasons include the following:
{:shortdesc}


* It is easier to integrate your app with existing systems that have Kafka support, for example {{site.data.keyword.IBM}} {{site.data.keyword.streaminganalyticsshort}} and {{site.data.keyword.sparks}}.
* It offers lower latency and higher throughput than the other APIs.
* It offers a richer API than the Kafka REST API.

## Why use the Kafka REST API?
{: #why_rest_classic notoc}

** The Kafka REST API is available as part of the Classic plan only.**
<br/>

The Kafka REST API is a convenient interface that can be used in the following situations:  

* Where a developer wants to get started using {{site.data.keyword.messagehub}}
* In certain low throughput use cases where latency is not a critical factor
* For debugging and fault finding

The Kafka REST API is not intended as a high throughput, low latency interface. ​For these types of requirement, we recommend using the Kafka API to connect to and from {{site.data.keyword.messagehub}}. For more information, see [Using a Kafka client](/docs/services/EventStreams?topic=eventstreams-kafka_using#kafka_using).

## Why use the {{site.data.keyword.mql}} API?
{: #why_mql_classic notoc}

** The MQ Light API is available as part of the Classic plan only.**
<br/>

The {{site.data.keyword.mql}} API provides an AMQP-based messaging interface for Java™, Node.js, Python, and Ruby. The API is provided for backward compatibility with the earlier {{site.data.keyword.mql}} service.











