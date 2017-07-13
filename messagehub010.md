---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# About Message Hub
{: #about}

{{site.data.keyword.messagehub_full}} is a scalable,
distributed, high throughput messaging service that enables applications and services to communicate
easily and reliably.
{:shortdesc}

In {{site.data.keyword.messagehub}}, applications send data by
creating a message and sending it to a topic. To receive messages, applications subscribe to a topic
and choose to either receive all the topic's messages or to share the messages between them.
{{site.data.keyword.messagehub}} hosts and maintains the messages
in an ordered sequence. In contrast to traditional messaging systems, {{site.data.keyword.messagehub}} provides topics but not queues. However,
{{site.data.keyword.messagehub}} offers ways to share messages
between receiving applications, which results in behavior similar to queues.

You can use {{site.data.keyword.messagehub}} to complete the
following tasks:

* Wire microservices together.
* Offload work to back-end worker processes.
* Connect stream data to analytics to realize powerful insights.
* Publish event data to multiple applications to react in real time.
* Transfer data into another service. For example, to long-term storage.
