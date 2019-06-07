---

copyright:
  years: 2015, 2019
lastupdated: "2019-05-13"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:faq: data-hd-content-type='faq'}

# FAQs for the Classic plan 
{: #faqs_classic}

Answers to common questions about the {{site.data.keyword.IBM}} {{site.data.keyword.messagehub}} service for the Classic plan.

For answers to questions related to all {{site.data.keyword.messagehub}} plans, see [FAQs](/docs/services/EventStreams?topic=eventstreams-faqs#faqs).
{: shortdesc}

<!--17/10/17 - Karen: same info duplicated at messagehub104 -->
## How do I use Kafka APIs to create and delete topics?
{: #topic_admin_classic}
{: faq}

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
</dd>
</dl>


## How long does {{site.data.keyword.messagehub}} set the log retention window for the consumer offsets topic?
{: #offsets_classic }
{: faq}

{{site.data.keyword.messagehub}} retains consumer offsets for 7 days. This corresponds to the Kafka configuration offsets.retention.minutes. 

Offset retention is system-wide so you cannot set it at an individual topic level. All consumer groups get only 7 days of stored offsets even if using a topic with a log retention that has been increased to the maximum of 30 days. 

<!--following message retention info duplicted in eventstreams057 and evenstreams108-->

## How long are messages retained?
{: #messages_retained_classic}

By default, messages are retained in Kafka for up to 24 hours and
each partition is capped at 1 GB. If the 1 GB cap is reached, the
oldest messages are discarded to stay within the limit.

You can change the time limit for message retention when you
create a topic using either the user interface or the
administration API. The time limit is a minimum of an hour and a
maximum of 30 days.

For information about restrictions on the settings allowed when you create topics using a Kafka client or Kafka Streams, see [How do I use Kafka APIs to create and delete topics?](/docs/services/EventStreams?topic=eventstreams-faqs_classic#topic_admin_classic).


## What is {{site.data.keyword.messagehub}}'s availability behavior?
{: #availability_classic}
{: faq}

If you write {{site.data.keyword.messagehub}} apps, use this information to understand what normal {{site.data.keyword.messagehub}} availability behavior is and what your apps are expected to handle.

### APIs
{: #api_availability_classic }

As part of the regular operation of {{site.data.keyword.messagehub}}, the nodes of the Kafka clusters are occasionally restarted.
In some cases, your apps will be aware as the cluster reassigns resources. Write your apps to be resilient
to these changes and to be able to reconnect and retry operations.

### {{site.data.keyword.messagehub}} bridges 
{: #bridge_availability_classic }

Write your apps to handle the possibility that bridges might restart from time to time.

## What is {{site.data.keyword.messagehub}}'s maximum message size? 
{: #max_message_size_classic }
{: faq}

{{site.data.keyword.messagehub}}'s maximum message size is 1 MB, which is the Kafka default. 

## What are {{site.data.keyword.messagehub}}'s replication settings? 
{: #replication_classic }
{: faq}

{{site.data.keyword.messagehub}} is configured to provide strong availability and durability.
The following configuration settings apply to all topics and cannot be changed:
* replication.factor = 3
* min.insync.replicas = 2

## How does {{site.data.keyword.messagehub}}'s billing work on the Classic plan? 
{: #billing_classic }
{: faq}

{{site.data.keyword.messagehub}} on the Classic plan regularly samples a user's topic count and {{site.data.keyword.Bluemix_notm}} records the maximum sample value each day. {{site.data.keyword.messagehub}} bills for the maximum number of concurrent partitions seen and for the sum of messages that are sent and received daily.

For example, if you create and delete 1 topic 10 times in a day, you are charged for a maximum of 1 topic. However, if you create 10 topics and delete them, you might be charged for either 0 or 10 topics depending when the sampling takes place.

{{site.data.keyword.messagehub}} bills either for each message or for each 64 k. A message up to 64 k counts as 1 billable message. Messages larger than 64 k count as the following number of billable messages: <code><var class="keyword varname">message_size</var> &divide; 64 k</code>.

<!--12/04/18 - Karen: same info duplicated at messagehub057 -->
## How often does the Kafka REST API restart? 
{: #REST_restart_classic }
{: faq}

The Kafka REST API restarts once a day for a short period of
time. 

During this period, the Kafka REST API might become
unavailable. If this happens, you are recommended to retry your
request. After the REST API has restarted, you will have to
create your Kafka consumer instances again. If this is the case, the
REST API returns the following JSON:

```'{"error_code":40403,"message":"Consumer instance not found."}'
```
{:screen}

## What are the differences between the {{site.data.keyword.messagehub}} plans?
{: #plan_compare_classic }
{: faq}

To find out more information about the other {{site.data.keyword.messagehub}} plans, see [Choosing your plan](/docs/services/EventStreams?topic=eventstreams-plan_choose).For information about the Classic plan, see [Classic plan overview](/docs/services/EventStreams?topic=eventstreams-plan_choose_classic#plan_choose_classic).


## How do I handle disaster recovery?
{: #disaster_recovery_classic }
{: faq}

Currently, it is the responsibility of the user to manage their own {{site.data.keyword.messagehub}} disaster recovery. {{site.data.keyword.messagehub}} data can be replicated between an {{site.data.keyword.messagehub}} instance in one location (region) and another instance in a different location. However, the user is responsible for provisioning a remote {{site.data.keyword.messagehub}} instance and managing the replication.

The user is also responsible for the backup of message payload data. Although this data is replicated across multiple Kafka brokers within a cluster, which protects against the majority of failures, this replication does not cover a location-wide failure. 

Topic names are backed up by {{site.data.keyword.messagehub}}.










