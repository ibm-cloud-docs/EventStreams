---

copyright:
  years: 2015, 2019
lastupdated: "2019-02-03"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# What is {{site.data.keyword.messagehub}}?
{: #about}

{{site.data.keyword.messagehub_full}} is a high-throughput message bus built with Apache Kafka. It is optimized for event ingestion into {{site.data.keyword.Bluemix_notm}} and event stream distribution between your services and applications. {{site.data.keyword.messagehub}} was previously known as Message Hub.
{: shortdesc}

You can use {{site.data.keyword.messagehub}} to complete the following tasks:

* Offload work to back-end worker applications.
* Connect event streams to streaming analytics to realize powerful insights.
* Publish event data to multiple applications to react in real time.

By being built with Apache Kafka, it directly benefits from all the innovation occurring in the community and supports Kafka client APIs, Kafka Streams, and Kafka Connect.

Apache Kafka tools usually work directly with {{site.data.keyword.messagehub}}, although you do need to provide additional configuration because connections to {{site.data.keyword.messagehub}} always authenticate using credentials.

In {{site.data.keyword.messagehub}}, applications send data by creating a message and sending it to a topic. To receive messages, applications subscribe to a topic
and choose to either receive all the topic's messages or to share the messages between them.
{{site.data.keyword.messagehub}} hosts and maintains the messages in an ordered sequence. 




