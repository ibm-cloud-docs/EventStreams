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

# Why use the {{site.data.keyword.mql}} API?
{: #why_mql}

The {{site.data.keyword.mql}} API provides a higher
level of abstraction than the Kafka API. {{site.data.keyword.mql}} enables apps to be written quickly and portably in a unified messaging model that supports both queue and publish/subscribe messaging patterns. 
{:shortdesc}

Apps exchange messages using dynamically created
destinations, which you can hierarchically structure (for example, <code>‘/sports/football’</code>), group using wildcards (for example,
<code>‘/sports/#’</code>) and have simple controls for delivery assurance and message expiry.
This enables you to implement scenarios such as worker offload, event notification, and batch
processing straightforwardly.

As well as sending messages between other apps using the {{site.data.keyword.mql}} API, you can also exchange messages with apps that use the Kafka REST or Kafka APIs. Alternatively, you can also use apps on premises with {{site.data.keyword.IBM}} MQ.

