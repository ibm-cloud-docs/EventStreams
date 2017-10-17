---

copyright:
  years: 2015, 2017
lastupdated: "2017-09-26"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.messagehub}} FAQs
{: #faqs}

Answers to common questions about the {{site.data.keyword.IBM}} {{site.data.keyword.messagehub}} service.

<!--17/10/17 - Karen: same info duplicated at messagehub104 -->
## How do I use Kafka APIs to create and delete topics?
{: #topic_admin notoc}

If you're using a Kafka client at 0.11 or later, or Kafka Streams at 0.10.2.0 or later, you can use APIs to create and delete topics. We've put some restrictions on the settings allowed when you create topics. Currently, you can modify the following settings only:

<dl>
<dt>cleanup.policy</dt>
<dd>Set to <code>delete</code> (default), <code>compact</code> or <code>delete,compact</code></dd>
<dt>retention.ms</dt>
<dd>The default retention period is 24 hours. The minimum is 1 hour and the maximum is
30 days. Specify this value as multiples of hours.

<p>**Note:**
If the cleanup policy is <code>compact</code> only, we automatically add <code>delete</code> but disable deletion based on time. Messages in the topic are compacted up to 1 GB before being deleted.</p>
</dd>
</dl>
## How long does Message Hub set the log retention window for the consumer offsets topic?
{: #offsets notoc}
{{site.data.keyword.messagehub}} retains consumer offsets for 7 days. This corresponds to the Kafka configuration offsets.retention.minutes. 

Offset retention is system-wide so you cannot set it at an individual topic level. All consumer groups get only 7 days of stored offsets even if using a topic with a log retention that has been increased to the maximum of 30 days. 

## What is {{site.data.keyword.messagehub}}'s availability behavior?
{: #availability}

If you write {{site.data.keyword.messagehub}} apps, use this information to understand what normal {{site.data.keyword.messagehub}} availability behavior is and what your apps are expected to handle.

### APIs
{: #api_availability notoc}

As part of the regular operation of {{site.data.keyword.messagehub}}, the nodes of the Kafka clusters are occasionally restarted.
In some cases, your apps will be aware as the cluster reassigns resources. Write your apps to be resilient
to these changes and to be able to reconnect and retry operations.

### {{site.data.keyword.messagehub}} bridges
{: #bridge_availability notoc}

Write your apps to handle the possibility that bridges might restart from time to time.

## What's {{site.data.keyword.messagehub}}'s replication factor? 
{: #replication}

The replication factor is 3 and replication has no impact on cost. 

## How many insync replicas are supported? 
{: #replicas}

You can set a maximum of 2 insync replicas when producing messages.
