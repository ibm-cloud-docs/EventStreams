---

copyright:
  years: 2015, 2018
lastupdated: "2018-01-23"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Watson IoT Platform bridge
{: #consuming_messages }

{{site.data.keyword.iot_full}} provides a managed bridge for creating a unidirectional link to {{site.data.keyword.messagehub}}.

Connecting {{site.data.keyword.messagehub_full}} to {{site.data.keyword.iot_short_notm}} allows you to use {{site.data.keyword.messagehub}} as an event pipeline to consume your device events from the {{site.data.keyword.iot_short_notm}} and to make them available in real time to the rest of the platform. 

A common pattern is to use the {{site.data.keyword.iot_short_notm}} bridge, {{site.data.keyword.messagehub}}, and the Cloud Object Storage bridge to create an end-to-end pipeline, which facilitates real-time and batch interactions.

For information about to how to create this bridge, see: [Connecting and configuring a historian service by using {{site.data.keyword.messagehub}}] (/docs/services/IoT/message_hub.html)



