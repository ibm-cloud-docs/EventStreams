---

copyright:
  years: 2015, 2017
lastupdated: "2016-11-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Enabling the {{site.data.keyword.mql}} API in {{site.data.keyword.messagehub}}
{: #mql_enable}


**You must explicitly create a Kafka topic named "MQLight" before you can use the API because all messages go through the "MQLight" topic. This topic must have a single partition. Creating this topic enables the MQ Light API for your service instance. **  For more information about how to create topics in {{site.data.keyword.messagehub}}, see [Managing topics](/docs/services/MessageHub/messagehub070.html).

The "MQLight" topic is used by the MQ Light API to store its message data and interact with other Kafka clients. Be aware that when this topic is
created, it incurs charges at the standard rate outlined in the services payment plan.

To disable the MQ Light API, delete the "MQLight" topic. Note that all data is destroyed when the topic is deleted.
