---

copyright:
  years: 2015, 2020
lastupdated: "2020-02-03"

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

Before you opt in to using {{site.data.keyword.mon_full}} metrics, be aware of the cost of doing so. The estimated cost depends on the following considerations:

* how often time series is sent for each plan
* the number of topics you use
* the {{site.data.keyword.messagehub}} plan that you use
* whether you are using a customer account or a provider account




