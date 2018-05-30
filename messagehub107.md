---

copyright:
  years: 2015, 2018
lastupdated: "2018-05-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# What is Message Hub?

{{site.data.keyword.messagehub}} implements publish/subscribe
messaging using topics. Unlike other messaging systems, {{site.data.keyword.messagehub}} provides topics but not queues. {{site.data.keyword.messagehub}} also offers
additional capabilities such as bridges to other systems.

{{site.data.keyword.messagehub}} is based on the open-source
Apache Kafka project, a highly scalable, high-performing messaging backbone proven in many
production environments. For more information, see [{{site.data.keyword.messagehub}} and Apache Kafka](/docs/services/MessageHub/messagehub073.html).
Apache Kafka tools usually work directly with {{site.data.keyword.messagehub}}, although you do need to provide additional configuration because connections to {{site.data.keyword.messagehub}} always authenticate using credentials.

{{site.data.keyword.messagehub}} is available in two different plans depending on your requirements: Standard and Enterprise.

* Choose the Enterrpise plan if data isolation and performance are important considerations. 

* Choose the Standard plan if you want an economical public cloud service where you pay for what you use and share infrastructure with others.

Depending on which plan you're using {{site.data.keyword.messagehub}} offers different APIs. On the Enterprise plan, you can use the Kafka API. On the Standard plan, you can choose from the Kafka API, the Kafka REST API, and the {{site.data.keyword.mql}} API. In most cases, the Kafka API is the best choice. For more information, see [Creating messaging applications](/docs/services/MessageHub/messagehub086.html).

## {{site.data.keyword.messagehub}} Standard plan
The {{site.data.keyword.messagehub}} Standard plan also
supports bridges to a selection of other systems. A bridge is a unidirectional link to another
system. A bridge can take messages from the other system and publish them onto a topic, or consume
messages from a topic and send them to the other system. In this way, you can use {{site.data.keyword.messagehub}} to integrate with other systems without writing code. For more information, see [Linking to other services using bridges](/docs/services/MessageHub/messagehub088.html).

