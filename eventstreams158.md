---

copyright:
  years: 2015, 2020
lastupdated: "2020-02-03c"

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

# Metrics with IBM Cloud Monitoring with Sysdig
{: #metrics}

{{site.data.keyword.mon_full}} is a third-party cloud-native, and container-intelligence management system that you can include as part of your {{site.data.keyword.cloud_notm}} architecture. Use it to gain operational visibility into the performance and health of your applications, services, and platforms. It offers administrators, DevOps teams, and developers full stack telemetry with advanced features to monitor and troubleshoot, define alerts, and design custom dashboards. {{site.data.keyword.mon_full_notm}} is operated by Sysdig in partnership with {{site.data.keyword.IBM_notm}}.
{:shortdesc}


## Opting in to {{site.data.keyword.messagehub}} metrics
{: #opt_in_metrics}

To opt into using {{site.data.keyword.messagehub}} Sysdig metrics, complete the steps detailed in 
[Getting started tutorial for {{site.data.keyword.mon_full}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-getting-started#step1){:new_window}.


## {{site.data.keyword.messagehub}} metrics details
{: #metric_details}

Describe the metrics we are providing ( there is a script to generate document based on the metrics I onboard to sysdig)
a. metrics dictionary (JP has a script to generate document from metrics metadata submitted to sysdig)
eg. https://test.cloud.ibm.com/docs/observability-monitoring?topic=observability-monitoring-supertenant-sample-doc.


[Monitoring Event Streams metrics ![External link icon](../../icons/launch-glyph.svg "External link icon")]
 (/docs/observability-monitoring?topic=observability-monitoring-monitor-sysdig){:new_window}.


## {{site.data.keyword.messagehub}} metrics cost information
{: #metric_costs}

Before you opt in to using {{site.data.keyword.mon_full}} metrics, be aware of the cost of doing so. The estimated cost depends on the following considerations:

* how often time series is sent for each plan
* the number of topics you use
* the {{site.data.keyword.messagehub}} plan that you use
* whether you are using a customer account or a provider account

| Plans            | Tier         | Data collection  |
|------------------|--------------|------------------|
| `Trial`          |              | Data is collected for a maximum of 20 containers per node or for 200 custom metrics per node for 30 days only. |
| `Graduated tier` | `Basic`      | Data is collected for a maximum of 20 containers per node or for 200 custom metrics per node. |
| `Graduated tier` | `Pro`        | Data is collected for a maximum of 50 containers per node or for 500 custom metrics per node. |
| `Graduated tier` | `Advanced`   | Data is collected for a maximum of 110 containers per node or for 3000 custom metrics per node. |
{: caption="Table 1. List of service plans" caption-side="top"} 




