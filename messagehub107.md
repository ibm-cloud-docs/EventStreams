---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-27"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# What is Message Hub?

{{site.data.keyword.messagehub}} implements publish/subscribe
messaging using topics. Unlike other messaging systems, {{site.data.keyword.messagehub}} provides topics but not queues. {{site.data.keyword.messagehub}} also offers
additional capabilities such as the {{site.data.keyword.mql}} API and bridges to other systems.

{{site.data.keyword.messagehub}} has three APIs: the Kafka API, the {{site.data.keyword.mql}} API and the
Kafka REST API. For more information, see [Creating messaging applications](/docs/services/MessageHub/messagehub086.html).

{{site.data.keyword.messagehub}} also
supports bridges to a selection of other systems. A bridge is a unidirectional link to another
system. A bridge can take messages from the other system and publish them onto a topic, or consume
messages from a topic and send them to the other system. In this way, you can use {{site.data.keyword.messagehub}} to integrate with other systems without writing code. For more information, see [Linking to other services using bridges](/docs/services/MessageHub/messagehub088.html).

{{site.data.keyword.messagehub}} is based on the open-source
Apache Kafka project, a highly scalable, high-performing messaging backbone proven in many
production environments. For more information, see [{{site.data.keyword.messagehub}} and Apache Kafka](/docs/services/MessageHub/messagehub073.html).
