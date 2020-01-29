---

copyright:
  years: 2015, 2020
lastupdated: "2020-01-29"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka, Sysdig, metrics, cost

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}
{:deprecated: .deprecated}
{:important: .important}

# {{site.data.keyword.messagehub}} metrics with {{site.data.keyword.mon_full}}
{: #metrics}

{site.data.keyword.cloud_notm}} 
{: shortdesc}


## Opting in to {{site.data.keyword.messagehub}} metrics
{: #opt_in_metrics}
Explain how to opt-in to {{site.data.keyword.messagehub}} metrics ( links to sysdig/metrics document)

To opt into using {{site.data.keyword.messagehub}} metrics, complete the steps detailed in 
[Getting started tutorial for {{site.data.keyword.mon_full}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](docs/services/Monitoring-with-Sysdig?topic=Sysdig-getting-started){:new_window}.


## {{site.data.keyword.messagehub}} metrics details
{: #metric_details}
Describe the metrics we are providing ( there is a script to generate document based on the metrics I onboard to sysdig, but need your help to refine the help text).
a. metrics dictionary (JP has a script to generate document from metrics metadata submitted to sysdig)
eg. https://test.cloud.ibm.com/docs/observability-monitoring?topic=observability-monitoring-supertenant-sample-doc.
We will need to refine the readable name and help text in our metadata: ; https://github.ibm.com/mhub/prometheus/tree/sysdig/sysdig/onboarding




## {{site.data.keyword.messagehub}} metrics cost information
{: #metric_costs}

Before you opt in to using {{site.data.keyword.mon_full}} metrics, you should be aware of the cost of doing so.
* 
The estimated cost depends on:
* the number of topics you use
* the {{site.data.keyword.messagehub}} plan that you use
* whether you are using a customer account or a provider account
Tell customer the cost before he/she decides to opt-in (how many time series we are sending for each plan, and estimated cost which varies to the number of topics). the estimated cost for different plans, I'm still waiting for sysdig to confirm the usage for both customer account and provider account.



