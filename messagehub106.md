---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-28"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# What is the MQ Light API and how is it different?
{: #mqlight}

The {{site.data.keyword.mql}} API provides a higher level of
abstraction for messaging compared to Kafka, which makes it easier to learn and easier to use in
your applications.
{:shortdesc}

The choice between using a Kafka client or the {{site.data.keyword.mql}} API depends on the messaging topology that you
want to build:

* With Kafka, you use a small number of topics and can have multiple partitions for each topic for additional scalability. You can share messages among consumers by using consumer groups, but each consumer must be able to keep up with the rate of messages for the partitions assigned to it.
* With the {{site.data.keyword.mql}} API, you can use a much larger number of topics and the topic names are hierarchical (for example: ```‘/sports/football’``` and ```‘/sports/tiddlywinks’```). Sharing messages among consumers is much simpler.

The topics in the {{site.data.keyword.mql}} API are not the same
as Kafka topics. Instead, the {{site.data.keyword.mql}} API uses a
single Kafka topic called "MQLight" and all the messages sent and received using the {{site.data.keyword.mql}} API go through that one Kafka topic.

The {{site.data.keyword.mql}} is available in the following
{{site.data.keyword.Bluemix_notm}} regions only: US South, United Kingdom, and Sydney. The MQ Light API not available in the Germany region or in
{{site.data.keyword.Bluemix_notm}} Dedicated.

<!-- begin STAGING ONLY -->
For more information about choosing between the APIs, see [Choosing between the three APIs](/docs/services/MessageHub/messagehub087.html).
<!-- end STAGING ONLY -->

