---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-18"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Choosing between the three APIs
{: #choose_api}

{{site.data.keyword.messagehub}} supports three APIs. Here's some information to help you choose which is most appropriate:

## Why use the Kafka API?
{: #why_kafka notoc}

There are a few reasons that you might choose to use the Kafka API over the other interfaces provided by {{site.data.keyword.messagehub}}. These reasons include the following:
{:shortdesc}


* It is easier to integrate your app with existing systems that have Kafka support, for example {{site.data.keyword.IBM}} {{site.data.keyword.streaminganalyticsshort}} and {{site.data.keyword.sparks}}.
* It offers lower latency and higher throughput than the other APIs.
* It offers a richer API than the Kafka REST API.


## Why use the {{site.data.keyword.mql}} API?
{: #why_mql notoc}

The {{site.data.keyword.mql}} API provides a higher
level of abstraction than the Kafka API. {{site.data.keyword.mql}} enables apps to be written quickly and portably in a unified messaging model that supports both queue and publish/subscribe messaging patterns. 
{:shortdesc}

Apps exchange messages using dynamically created
destinations, which you can hierarchically structure (for example, <code>‘/sports/football’</code>), group using wildcards (for example,
<code>‘/sports/#’<code>) and have simple controls for delivery assurance and message expiry.
This enables you to implement scenarios such as worker offload, event notification, and batch processing straightforwardly.

As well as sending messages between other apps using the {{site.data.keyword.mql}} API, you can also exchange messages with apps that use the Kafka REST or Kafka APIs. Alternatively, you can also use apps on premises with {{site.data.keyword.IBM_notm}} MQ.


## Why use the Kafka REST API?
{: #why_rest notoc}

The Kafka REST API is a convenient interface that can be used in the following situations:  

* Where a developer wants to quickly get started using {{site.data.keyword.messagehub}}
* In certain low throughput use cases where latency is not a critical factor
* For debugging and fault finding

The Kafka REST API is not intended as a high throughput, low latency interface. ​For these types of requirement, we recommend using the Kafka API to connect to and from {{site.data.keyword.messagehub}}. For more information, see [Using a Kafka client](/docs/services/MessageHub/messagehub050.html#kafka_client).








