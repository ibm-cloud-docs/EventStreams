---

copyright:
  years: 2015, 2019
lastupdated: "2019-11-27"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:faq: data-hd-content-type='faq'}
{:deprecated: .deprecated}

# FAQs
{: #faqs}

Answers to common questions about the {{site.data.keyword.IBM}} {{site.data.keyword.messagehub}} service.

For answers to questions specific to the now deprecated Classic plan, see [FAQs for the Classic plan](/docs/services/EventStreams?topic=eventstreams-faqs_classic).
{: shortdesc}

<!--17/10/17 - Karen: same info duplicated at messagehub104 -->
## How do I use Kafka APIs to create and delete topics?
{: #topic_admin}
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
{: faq}

{{site.data.keyword.messagehub}} retains consumer offsets for 7 days. This corresponds to the Kafka configuration offsets.retention.minutes. 

Offset retention is system-wide so you cannot set it at an individual topic level. All consumer groups get only 7 days of stored offsets even if using a topic with a log retention that has been increased to the maximum of 30 days. 

The internal Kafka `__consumer_offsets` topic is visible to you as read-only on the Enterpise plan. 
You are strongly recommended not to attempt to manage the topic in any way. You cannot access the `__consumer_offsets` topic in any way on the Standard plan. 

<!--following message retention info duplicated in eventstreams057-->


## How can I clean up a consumer group with no consumers?
{: #clean_consumer_group}
{: faq}

After consumers have left, a group continues to exist only if it has offsets. Consumer offsets are deleted after 7 days of inactivity. Consequently, a consumer group is deleted when the last committed offset for that group expires.

If you want to explicitly delete a group at a time you choose, you can use the 
[deleteConsumerGroups() API ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://kafka.apache.org/23/javadoc/org/apache/kafka/clients/admin/AdminClient.html#deleteConsumerGroups-java.util.Collection-){:new_window}.


## How long are messages retained?
{: #messages_retained}
{: faq}

By default, messages are retained in Kafka for up to 24 hours and
each partition is capped at 1 GB. If the 1 GB cap is reached, the
oldest messages are discarded to stay within the limit.

You can change the time limit for message retention when you
create a topic using either the user interface or the
administration API. The time limit is a minimum of an hour and a
maximum of 30 days.

For information about restrictions on the settings allowed when you create topics using a Kafka client or Kafka Streams, see [How do I use Kafka APIs to create and delete topics?](/docs/services/EventStreams?topic=eventstreams-faqs#topic_admin).

## What is {{site.data.keyword.messagehub}}'s availability behavior?
{: #availability}
{: faq}

If you write {{site.data.keyword.messagehub}} apps, use this information to understand what normal {{site.data.keyword.messagehub}} availability behavior is and what your apps are expected to handle.

### APIs
{: #api_availability }

As part of the regular operation of {{site.data.keyword.messagehub}}, the nodes of the Kafka clusters are occasionally restarted.
In some cases, your apps will be aware as the cluster reassigns resources. Write your apps to be resilient
to these changes and to be able to reconnect and retry operations.

## What is {{site.data.keyword.messagehub}}'s maximum message size? 
{: #max_message_size }
{: faq}

{{site.data.keyword.messagehub}}'s maximum message size is 1 MB, which is the Kafka default. 

## What are {{site.data.keyword.messagehub}}'s replication settings? 
{: #replication }
{: faq}

{{site.data.keyword.messagehub}} is configured to provide strong availability and durability.
The following configuration settings apply to all topics and cannot be changed:
* replication.factor = 3 
* min.insync.replicas = 2

## What are the restrictions and defaults for topics and partitions?
{: #topics_partitions_defaults}
{: faq}

*  Topic names are restricted to a maximum of 100 characters.
*  The default number of partitions for a topic is one.
*  Each {{site.data.keyword.Bluemix_notm}} space has a limit of 100 partitions. To create
   more partitions, you must use a new {{site.data.keyword.Bluemix_notm}} space.

## How do I check which {{site.data.keyword.messagehub}} plan I've provisioned?
{: #plan_check}
{: faq}

To confirm which type of {{site.data.keyword.messagehub}} plan you've provisioned (Lite, Standard, Enterprise, or Classic), complete the following steps:
1. In the {{site.data.keyword.Bluemix_notm}} console, navigate to the instance of {{site.data.keyword.messagehub}} that you want to check.
2. Click the **Plan** tab in the navigation pane on the left.
The **Current plan** section displays your plan type. 

## Can I change my {{site.data.keyword.messagehub}} plan using the {{site.data.keyword.Bluemix_notm}} console?
{: #plan_migrate}
{: faq}

Yes, but only if you are moving from the Lite plan to the Standard plan.

1. In the {{site.data.keyword.Bluemix_notm}} console, navigate to the instance of {{site.data.keyword.messagehub}} Lite plan that you want to change. 
2. Click the **Plan** tab in the navigation pane on the left.
3. In the **Change pricing plan** section, check the **Standard** box. Click **Upgrade**.
<br/>
<br/>

However, this option does not currently work in the {{site.data.keyword.Bluemix_notm}} console for any other combination of plans. For example, if you try to change the pricing plan from Classic to Standard, you'll see an error message like the the following:
```
Could not find VCAP::CloudController::ServicePlan with guid: ibm.eventstreams.standard 
```
{:codeblock}


## What are the differences between the {{site.data.keyword.messagehub}} Standard and {{site.data.keyword.messagehub}} Enterprise plans?
{: #plan_compare }
{: faq}

To find out more information about the different {{site.data.keyword.messagehub}} plans, see [Choosing your plan](/docs/services/EventStreams?topic=eventstreams-plan_choose).

## How do I handle disaster recovery?
{: #disaster_recovery }
{: faq}

Currently, it is the responsibility of the user to manage their own {{site.data.keyword.messagehub}} disaster recovery. {{site.data.keyword.messagehub}} data can be replicated between an {{site.data.keyword.messagehub}} instance in one location (region) and another instance in a different location. However, the user is responsible for provisioning a remote {{site.data.keyword.messagehub}} instance and managing the replication. 

We suggest a tool like Kafka MirrorMaker to replicate data between clusters. For information about how to run MirrorMaker, see 
[{{site.data.keyword.messagehub}} kafka-mirrormaker repository ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/event-streams-samples/tree/master/kafka-mirrormaker){:new_window}.

The user is also responsible for the backup of message payload data. Although this data is replicated across multiple Kafka brokers within a cluster, which protects against the majority of failures, this replication does not cover a location-wide failure. 

Topic names are backed up by {{site.data.keyword.messagehub}}, although it is recommended good practice for users to back up topic names and the configuration data for those topics.

If you have configured your {{site.data.keyword.messagehub}} instance in a Multi-Zone Region, a regional disaster is very unlikely. However, we recommend that users do plan for such circumstances. If a user's instance is no longer available because of a disaster (and a remote DR instance is not already set up), the user should consider configuring a new instance in a new region and restoring their topics and data from backup if available. Applications can then be pointed at the new instance.












