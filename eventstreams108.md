---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# FAQs
{: #faqs}

Answers to common questions about the {{site.data.keyword.IBM}} {{site.data.keyword.messagehub}} service.
{: shortdesc}

<!--17/10/17 - Karen: same info duplicated at messagehub104 -->
## How do I use Kafka APIs to create and delete topics?
{: #topic_admin}

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


## How long does {{site.data.keyword.messagehub}} set the log retention window for the consumer offsets topic?
{: #offsets }
{{site.data.keyword.messagehub}} retains consumer offsets for 7 days. This corresponds to the Kafka configuration offsets.retention.minutes. 

Offset retention is system-wide so you cannot set it at an individual topic level. All consumer groups get only 7 days of stored offsets even if using a topic with a log retention that has been increased to the maximum of 30 days. 

## What is {{site.data.keyword.messagehub}}'s availability behavior?
{: #availability}

If you write {{site.data.keyword.messagehub}} apps, use this information to understand what normal {{site.data.keyword.messagehub}} availability behavior is and what your apps are expected to handle.

### APIs
{: #api_availability }

As part of the regular operation of {{site.data.keyword.messagehub}}, the nodes of the Kafka clusters are occasionally restarted.
In some cases, your apps will be aware as the cluster reassigns resources. Write your apps to be resilient
to these changes and to be able to reconnect and retry operations.

### {{site.data.keyword.messagehub}} bridges (Standard plan only)
{: #bridge_availability }

Write your apps to handle the possibility that bridges might restart from time to time.

## What is {{site.data.keyword.messagehub}}'s maximum message size? 
{: #max_message_size }

{{site.data.keyword.messagehub}}'s maximum message size is 1 MB, which is the Kafka default. 

## What are {{site.data.keyword.messagehub}}'s replication settings? 
{: #replication }

{{site.data.keyword.messagehub}} is configured to provide strong availability and durability.
The following configuration settings apply to all topics and cannot be changed:
* replication.factor = 3
* min.insync.replicas = 2

## How does {{site.data.keyword.messagehub}}'s billing work on the Standard plan? 
{: #billing }

{{site.data.keyword.messagehub}} on the Standard plan regularly samples a user's topic count and {{site.data.keyword.Bluemix_notm}} records the maximum sample value each day. {{site.data.keyword.messagehub}} bills for the maximum number of concurrent partitions seen and for the sum of messages that are sent and received daily.

For example, if you create and delete 1 topic 10 times in a day, you are charged for a maximum of 1 topic. However, if you create 10 topics and delete them, you might be charged for either 0 or 10 topics depending when the sampling takes place.

{{site.data.keyword.messagehub}} bills either for each message or for each 64 k. A message up to 64 k counts as 1 billable message. Messages larger than 64 k count as the following number of billable messages: <code><var class="keyword varname">message_size</var> &divide; 64 k</code>.

<!--12/04/18 - Karen: same info duplicated at messagehub057 -->
## How often does the Kafka REST API restart? 
{: #REST_restart }

The Kafka REST API restarts once a day for a short period of
time. 

During this period, the Kafka REST API might become
unavailable. If this happens, you are recommended to retry your
request. After the REST API has restarted, you will have to
recreate your Kafka consumer instances. If this is the case, the
REST API returns the following JSON:

```'{"error_code":40403,"message":"Consumer instance not found."}'
```
{:screen}

## What are the differences between the {{site.data.keyword.messagehub}} Standard and {{site.data.keyword.messagehub}} Enterprise plans?
{: #plan_compare }

To find out more information about the two different {{site.data.keyword.messagehub}} plans, see [Choosing your plan](/docs/services/EventStreams/eventstreams085.html).

## How do I handle disaster recovery?
{: #disaster_recovery }

Currently, it is the responsibility of the user to manage their own {{site.data.keyword.messagehub}} disaster recovery. {{site.data.keyword.messagehub}} data can be replicated between an {{site.data.keyword.messagehub}} instance in one region and another instance in a different region. However, the user is responsible for provisioning a remote {{site.data.keyword.messagehub}} instance and managing the replication.

The user is also responsible for the backup of message payload data. Although this data is replicated across multiple Kafka brokers within a cluster, which protects against the majority of failures, this replication does not cover a region-wide failure. 

Topic names are backed up by {{site.data.keyword.messagehub}}.










