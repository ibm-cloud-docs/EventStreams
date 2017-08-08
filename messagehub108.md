---

copyright:
  years: 2015, 2017
lastupdated: "2017-08-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.messagehub}} FAQs
{: #faqs}

Answers to common questions about the {{site.data.keyword.IBM}} {{site.data.keyword.messagehub}} service.

## What's the default for Kafka `offsets.retention.minutes`?
{: #offsets}
The default is 24 hours. 

## What's {{site.data.keyword.messagehub}}'s availability behavior?
{: #availability notoc}

If you write {{site.data.keyword.messagehub}} apps, use this information to understand what normal {{site.data.keyword.messagehub}} availability behavior is and what your apps are expected to handle.

## APIs
{: #api_availability notoc}

Write your apps to expect connection breakages and the delivery interruptions caused by those breakages.

## Writing {{site.data.keyword.messagehub}} apps to use with bridges
{: #bridge_availability notoc}

Write your apps to handle the possibility that bridges might restart from time to time.
