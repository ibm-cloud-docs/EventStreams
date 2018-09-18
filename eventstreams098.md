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

# What's required to use the MQ Light API with {{site.data.keyword.messagehub}}?
{: #mql_reqs}

** The MQ Light API is available as part of the Standard plan only.**
<br/>

The following requirements are needed to use the {{site.data.keyword.mql}} API with {{site.data.keyword.messagehub}}: 

**You must explicitly create a Kafka topic named "MQLight" before you can use the API because all messages go through the "MQLight" topic. This topic must have a single partition. Creating this topic enables the MQ Light API for your service instance. The topics used in the MQ Light API are automatically created as you use them, but all of the messages are actually on the single "MQLight" Kafka topic.** 

The "MQLight" topic is used by the MQ Light API to store its message data and interact with other Kafka clients. Be aware that when this topic is
created, it incurs charges at the standard rate outlined in the services payment plan.

To disable the MQ Light API, delete the "MQLight" topic. Note that all data is destroyed when the topic is deleted.
