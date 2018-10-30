---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Using the MQ Light API 
{: #mql_using}

** The MQ Light API is available as part of the Standard plan only.**
<br/>

The {{site.data.keyword.mql}} API is provided for backward compatibility with the earlier {{site.data.keyword.mql}} service. The API provides an AMQP-based messaging interface for Java&trade;, Node.js, Python, and Ruby. 
{:shortdesc}


## What is the MQ Light API and how is it different?
{: #mqlight}

<!-- 30/10/18: info was in eventstreams106.md, moved because of doc app changes -->

The {{site.data.keyword.mql}} API provides a higher level of abstraction for messaging compared to Kafka.

The choice between using a Kafka client or the {{site.data.keyword.mql}} API depends on the messaging topology that you
want to build:

* With Kafka, you use a small number of topics and can have multiple partitions for each topic for additional scalability. You can share messages among consumers by using consumer groups, but each consumer must be able to keep up with the rate of messages for the partitions assigned to it.
* With the {{site.data.keyword.mql}} API, you can use a much larger number of topics and the topic names are hierarchical (for example: <code>‘/sports/football’</code> and <code>‘/sports/tiddlywinks’</code>). 

The topics in the {{site.data.keyword.mql}} API are not the same
as Kafka topics. Instead, the {{site.data.keyword.mql}} API uses a
single Kafka topic called "MQLight" and all the messages sent and received using the {{site.data.keyword.mql}} API go through that one Kafka topic.

The {{site.data.keyword.mql}} is available in the following
{{site.data.keyword.Bluemix_notm}} regions only: US South (Dallas), UK South (London), and AP South (Sydney). The MQ Light API not available in the EU Central (Frankfurt) region or in
{{site.data.keyword.Bluemix_notm}} Dedicated.


## What's required to use the MQ Light API with {{site.data.keyword.messagehub}}?
{: #mql_reqs}

<!-- 30/10/18: info was in eventstreams098.md, moved because of doc app changes -->

The following requirements are needed to use the {{site.data.keyword.mql}} API with {{site.data.keyword.messagehub}}: 

**You must explicitly create a Kafka topic named "MQLight" before you can use the API because all messages go through the "MQLight" topic. This topic must have a single partition. Creating this topic enables the MQ Light API for your service instance. The topics used in the MQ Light API are automatically created as you use them, but all of the messages are actually on the single "MQLight" Kafka topic.** 

The "MQLight" topic is used by the MQ Light API to store its message data and interact with other Kafka clients. Be aware that when this topic is
created, it incurs charges at the standard rate outlined in the services payment plan.

To disable the MQ Light API, delete the "MQLight" topic. Note that all data is destroyed when the topic is deleted.
