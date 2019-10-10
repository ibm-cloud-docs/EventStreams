---

copyright:
  years: 2016, 2018
lastupdated: "2019-10-01"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

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

# {{site.data.keyword.cloudaccesstrailshort}} events 
{: #at_events}

Use the {{site.data.keyword.cloudaccesstrailfull}} service to track how users and applications interact with the {{site.data.keyword.messagehub}} service on the Standard and Enterprise plans in {{site.data.keyword.Bluemix}}. 
{: shortdesc}

The {{site.data.keyword.cloudaccesstrailfull_notm}} service records user-initiated activities that change the state of a service in {{site.data.keyword.Bluemix_notm}}. For more information, see the [{{site.data.keyword.cloudaccesstrailshort}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started){:new_window}.

<!-- You can create different sections to group events by area. -->

## List of events
{: #events}

<!-- Make sure you introduce the table with a detailed description that immediately precedes it. For example, see https://cloud.ibm.com/docs/services/cloud-activity-tracker/services?topic=cloud-activity-tracker-cf#catalog. -->

{{site.data.keyword.messagehub}} on the Standard and Enterprise plans automatically generate events so that you can track activity on your service.

| Action | Description |
|:-------|:------------|
| event-streams.topic.create | An event is created when you create a topic|
| event-streams.topic.delete | An event is created when you delete a topic|
| event-streams.storage-key.read | An event is created when access to the disk encryption key in {{site.data.keyword.keymanagementserviceshort}} has changed.</br> If the outcome of this event is <code>success</code>, access to the disk encryption key has been restored and the {{site.data.keyword.messagehub}} instance is available for use.</br> If the outcome is <code>failure</code>, access to the disk encryption key has been withdrawn and the {{site.data.keyword.messagehub}} instance is not available for use. |
| event-streams.storage-key.update | The disk encryption key in {{site.data.keyword.keymanagementserviceshort}} has been rotated and the {{site.data.keyword.messagehub}} instance has been updated to use the new key. |
{: caption="Table 1. {{site.data.keyword.messagehub}} events" caption-side="top"}
<!-- 03/09/19 Karen: kafka.scale.down and kafka.scale.up are both related to BYOK. -->

## Where to view the events
{: #ui}

<!-- For example, choose one of the following two options. -->

<!-- Option 2: Add the following sentence if your service sends events to the account domain. -->

{{site.data.keyword.cloudaccesstrailshort}} events are available in the {{site.data.keyword.cloudaccesstrailshort}} **account domain** that is available in the {{site.data.keyword.Bluemix_notm}} location (region) where the events are generated.







