---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-27"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Managing topics
{: #managing}

You can manage topics in {{site.data.keyword.messagehub}} using
the following three methods:

* You are recommended to use the [Kafka Admin API ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://kafka.apache.org/11/javadoc/index.html?org/apache/kafka/clients/admin/AdminClient.html){:new_window}. This API requires a Kafka Java client at version 0.11 or later
* {{site.data.keyword.messagehub}} dashboard in the {{site.data.keyword.Bluemix_notm}} console
* [{{site.data.keyword.messagehub}} Administration API](/docs/services/MessageHub/messagehub037.html)
{:shortdesc}


## __consumer_offsets topic in the Enterprise plan

The internal __consumer_offsets topic is visible if you're using the Enterprise plan. You are strongly recommended not to attempt to delete or manage the topic in any way. 


<!-- 07/06/18 - Karen: removing until a newer version available
For a video that demonstrates how you can use the {{site.data.keyword.messagehub}} dashboard in the {{site.data.keyword.Bluemix_notm}} console, see [{{site.data.keyword.IBM_notm}} {{site.data.keyword.messagehub}} - User Interface ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.youtube.com/watch?v=lZulxqv_rHc){:new_window}.
-->
<!--
Examples and walkthrough needed for both - create, delete, secure topic
-->
