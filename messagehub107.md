---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-05"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# What is Message Hub?

{{site.data.keyword.messagehub_full}} is a high-throughput message bus built with Apache Kafka. It is optimized for event ingestion into {{site.data.keyword.Bluemix_notm}} and event stream distribution between your services and applications.

By being built with Apache Kafka, it directly benefits from all the innovation occurring in the community and Kafka client APIs, Kafka Streams, Kafka Connect, and also KSQL.

{{site.data.keyword.messagehub}} is based on the open-source
Apache Kafka project, a highly scalable, high-performing messaging backbone proven in many
production environments. For more information, see [{{site.data.keyword.messagehub}} and Apache Kafka](/docs/services/MessageHub/messagehub073.html).
Apache Kafka tools usually work directly with {{site.data.keyword.messagehub}}, although you do need to provide additional configuration because connections to {{site.data.keyword.messagehub}} always authenticate using credentials.

{{site.data.keyword.messagehub}} is available as two different plans depending on your requirements: Enterprise and Standard.

* Choose the Enterprise plan if data isolation, predictable performance, and being a single tenant are important considerations. 
* Choose the Standard plan if you want an economical public cloud service where you pay for what you use and share infrastructure with others.

Depending on which plan you're using {{site.data.keyword.messagehub}} offers different APIs. On the Enterprise plan, you can use the Kafka API. On the Standard plan, you can choose from the Kafka API, the Kafka REST API, and the {{site.data.keyword.mql}} API. In most cases, the Kafka API is the best choice. For more information, see [Creating messaging applications](/docs/services/MessageHub/messagehub086.html).



