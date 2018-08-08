---

copyright:
  years: 2016, 2018
lastupdated: "2018-08-03"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:table: .aria-labeledby="caption"}

<!-- Name your file `at-events.md` and include it in the Reference nav group in your toc file. -->

# {{site.data.keyword.cloudaccesstrailshort}} events in {{site.data.keyword.messagehub}} Enterprise plan
{: #at_events}

Use the {{site.data.keyword.cloudaccesstrailfull}} service to track how users and applications interact with the {{site.data.keyword.messagehub}} service in {{site.data.keyword.Bluemix}}. 
{: shortdesc}

The {{site.data.keyword.cloudaccesstrailfull_notm}} service records user-initiated activities that change the state of a service in {{site.data.keyword.Bluemix_notm}}. For more information, see the [{{site.data.keyword.cloudaccesstrailshort}}](/docs/services/cloud-activity-tracker/index.html#getting-started-with-cla).

<!-- You can create different sections to group events by area. -->

## List of events
{: #events}

<!-- Make sure you introduce the table with a detailed description that immediately precedes it. For example, see https://console.bluemix.net/docs/services/cloud-activity-tracker/services/at_events_cf.html#catalog. -->

{{site.data.keyword.messagehub}} on the Enterprise plan automatically generates events so that you can track activity on your service.

| Action | Description |
|:-------|:------------|
| messagehub.topic.create | An event is created when you create a topic|
| messagehub.topic.delete | An event is created when you delete a topic|
{: caption="Table 1. {{site.data.keyword.messagehub}} events" caption-side="top"}

## Where to view the events
{: #ui}

<!-- For example, choose one of the following two options. -->

<!-- Option 1: Add the following sentence if your service is provisioned within a Cloud Foundry org and space. -->

{{site.data.keyword.cloudaccesstrailshort}} events are available in the {{site.data.keyword.cloudaccesstrailshort}} **space domain** that is associated with the Cloud Foundry space where the {{site.data.keyword.cloudaccesstrailshort}} service is provisioned.






