---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-05"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Using the administration Kafka Java client API
{: #kafka_java_api}


<!-- 
17/10/17 - Karen: following info duplicated at messagehub108
 -->

If you're using a Kafka client at 0.11 or later, or Kafka Streams at 0.10.2.0 or later, you can use APIs to create and delete topics. We've put some restrictions on the settings allowed when you create topics. Currently, you can modify the following settings only:

<dl>
<dt>cleanup.policy</dt>
<dd>Set to <code>delete</code> (default), <code>compact</code> or <code>delete,compact</code>
<p>**Note:**
If the cleanup policy is <code>compact</code> only, we automatically add <code>delete</code>, but disable deletion based on time. Messages in the topic are compacted up to 1 GB before being deleted.</p>
</dd>

<dt>retention.ms</dt>
<dd>The default retention period is 24 hours. The minimum is 1 hour and the maximum is
30 days. Specify this value as multiples of hours.

<p>**Note:**
In the Enterprise plan, you can set this to any value.</p>
</dd>

<dt>retention.bytes</dt>
<dd>The maximum size a partition (which consists of log segments) can grow to before we discard old log segments to free up space.

<p>**Note:**
Enterprise plan only. Set to any value larger than 1 MB.</p>
</dd>

<dt>segment.bytes</dt>
<dd>The segment file size for the log.

<p>**Note:**
Enterprise plan only. Set to any value larger than 100 kB.</p>
</dd>

<dt>segment.index.bytes</dt>
<dd>The size of the index that maps offsets to file positions. 

<p>**Note:**
Enterprise plan only. Set to any value between 100 kB and 2 GB.</p>
</dd>

<dt>segment.ms</dt>
<dd>The period of time after which Kafka will force the log to roll even if the segment file isn't full. 

<p>**Note:**
Enterprise plan only. Set to any value between 5 minutes and 30 days</p>
</dd>
</dl>

