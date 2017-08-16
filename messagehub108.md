---

copyright:
  years: 2015, 2017
lastupdated: "2017-08-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.messagehub}} FAQs
{: #faqs}

Answers to common questions about the {{site.data.keyword.IBM}} {{site.data.keyword.messagehub}} service.

## What's the default value for Kafka offsets.retention.minutes?
{: #offsets notoc}
The default value is 7 days. 

Offset retention is system wide so you cannot set it at an individual topic level. All consumer groups get only 7 days of stored offsets even if their topic has been increased to the maximum 30 days of log retention. 

## What is {{site.data.keyword.messagehub}}'s availability behavior?
{: #availability notoc}

If you write {{site.data.keyword.messagehub}} apps, use this information to understand what normal {{site.data.keyword.messagehub}} availability behavior is and what your apps are expected to handle.

### APIs
{: #api_availability notoc}

As part of the regular operation of {{site.data.keyword.messagehub}}, the nodes of the Kafka clusters are occasionally restarted.
In some cases, your apps will be aware as the cluster reassigns resources. Write your apps to be resilient
to these changes and to be able to reconnect and retry operations.

### {{site.data.keyword.messagehub}} bridges
{: #bridge_availability notoc}

Write your apps to handle the possibility that bridges might restart from time to time.
