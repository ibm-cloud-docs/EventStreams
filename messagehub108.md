---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.messagehub}} availability behavior
{: #availability}

If you write {{site.data.keyword.messagehub}} apps, use this information to understand what normal {{site.data.keyword.messagehub}} availability behavior is and what your apps are expected to handle.

## APIs
{: #api_availability notoc}

Write your apps to expect connection breakages and the delivery interruptions caused by those breakages.

## {{site.data.keyword.messagehub}} bridges
{: #bridge_availability notoc}

Write your apps to handle the possibility that bridges might restart from time to time.
