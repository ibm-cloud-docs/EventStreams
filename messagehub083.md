---

copyright:
  years: 2015, 2017
lastupdated: "2016-22-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Maximum limits
{: #max_limits}

The following limits are enforced for the {{site.data.keyword.mql}} API:
{:shortdesc}

* The maximum amount of data that can be stored is consistent with a single Kafka partition for your payment plan (typically 1 GB). If this data limit is exceeded, the oldest messages in the partition are removed as new messages are sent.
* The maximum time a message is stored is consistent with a single Kafka partition for your payment plan (typically 24 hours). You cannot retrieve messages that are older than this time period.
* The maximum size of a message (excluding headers) is 1 MB.
* The maximum number of clients that can be connected at a single time is 25.
* The maximum number of destinations that can be active at a single time is 25. An active destination is defined as follows:
  - A destination with a TimeToLive > 0 both with or without a client currently connected.
  - A destination with a TimeToLive = 0 (the default) where a client is connected. 
  <p>A destination that is shared between clients counts as a single destination.</p>
