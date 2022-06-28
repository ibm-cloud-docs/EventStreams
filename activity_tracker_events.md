---

copyright:
  years: 2016, 2021
lastupdated: "2022-06-14"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka, activity

subcollection: EventStreams

---

{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:table: .aria-labeledby="caption"}
{:deprecated: .deprecated}

# {{site.data.keyword.cloudaccesstrailshort}} events 
{: #at_events}

Use the {{site.data.keyword.cloudaccesstrailfull}} service to track how users and applications interact with the {{site.data.keyword.messagehub}} service on the Standard and Enterprise plans in {{site.data.keyword.Bluemix}}. 
{: shortdesc}

The {{site.data.keyword.cloudaccesstrailfull_notm}} service records user-initiated activities that change the state of a service in {{site.data.keyword.cloud_notm}}. For more information, see the [{{site.data.keyword.cloudaccesstrailshort}}](/docs/activity-tracker?topic=activity-tracker-getting-started){: external}.

Events are formatted according to the Cloud Auditing Data Federation (CADF) standard, further details of the information 
they include can be found [here](https://cloud.ibm.com/docs/Activity-Tracker-with-LogDNA?topic=Activity-Tracker-with-LogDNA-event).

## Topic events
{: #topic-events}

{{site.data.keyword.messagehub}} instances that are on the Enterprise plan or the Standard plan automatically generate topic events. 

The following table lists the topic events: 

| Action | Description |
|:-------|:------------|
| event-streams.topic.create | An event is created when you create a topic.|
| event-streams.topic.delete | An event is created when you delete a topic.|
| event-streams.topic.update | An event is created when you update a topic's configuration or increase partitions.|
{: caption="Table 1. {{site.data.keyword.messagehub}} topic events" caption-side="top"}

Additional information about topic configuration is logged in the update and delete events,  for example partitions, `retentionMs`, and `segmentMs`.

## Message audit events
{: #message-events}

You can enable message audit events on a per topic basis for {{site.data.keyword.messagehub}} instances that are on the `Enterprise plan`. 
Also, see [How to enable message audit events](/docs/EventStreams?topic=EventStreams-at_events#enable-message-events).

The following table lists the message audit events:

| Action | Description |
|:-------|:------------|
| event-streams.message.read | An event is created when message audit is enabled on a topic and a consumer is reading data from this topic.|
| event-streams.message.write | An event is created when message audit is enabled on a topic and a producer is writing data to this topic.|
| event-streams.message.delete | An event is created when message audit is enabled on a topic and records are deleted from this topic. Records deletion because of retention policy does not generate.|
{: caption="Table 2. {{site.data.keyword.messagehub}} message events" caption-side="top"}

{{site.data.keyword.messagehub}} can sustain high requests rate so not every request triggers an event. Instead, events are aggregated by 
initiator (user ID or service ID), host (IP address), operation (read, write, delete), outcome (success or failure), and topic over a 1 hour period.

## Instance events (deprecated)
{: #instance-events}

{{site.data.keyword.messagehub}} instances that are on the Enterprise plan automatically generate instance events.

The following table lists the instance events, which are now replaced by [service instance events](/docs/activity-tracker?topic=activity-tracker-at_events_rc#rc_provision).
{: deprecated}


| Action | Description |
|:-------|:------------|
| event-streams.instance.create | An event is created when you create an instance.|
| event-streams.instance.delete | An event is created when you delete an instance.|
| event-streams.instance.update | An event is created when you update an instance’s throughput, storage, service endpoint type (public/private), and allowlist.|
{: caption="Table 3. {{site.data.keyword.messagehub}} instance events" caption-side="top"}

## Other events
{: #other-events}

{{site.data.keyword.messagehub}} instances that are on the `Enterprise plan` automatically generate events so that you can track activity on your service. 

| Action | Description |
|:-------|:------------|
| event-streams.storage-key.read | An event is created when access to the disk encryption key in {{site.data.keyword.keymanagementserviceshort}} changed. If the outcome of this event is `success`, access to the disk encryption key is restored and the {{site.data.keyword.messagehub}} instance is available for use. If the outcome is `failure`, access to the disk encryption key was withdrawn and the {{site.data.keyword.messagehub}} instance is not available for use. |
| event-streams.storage-key.update | The disk encryption key in {{site.data.keyword.keymanagementserviceshort}} was rotated and the {{site.data.keyword.messagehub}} instance was updated to use the new key. |
| event-streams.schema.create | A schema  or schema version was created or updated in the {{site.data.keyword.messagehub}} schema registry for the enterprise instance either through the administration API or through the Confluent Serdes.
| event-streams.schema.delete | A schema or schema version was deleted from the {{site.data.keyword.messagehub}} schema registry for the enterprise instance.|
| event-streams.schema-rule.create | A new rule or global rule was created in the {{site.data.keyword.messagehub}} schema registry for the enterprise instance.|
| event-streams.schema-rule.update | An existing rule or global rule was updated in the {{site.data.keyword.messagehub}} schema registry for the enterprise instance.|
| event-streams.schema-rule.delete | A rule was deleted in the {{site.data.keyword.messagehub}} schema registry for the enterprise instance.|
{: caption="Table 4. {{site.data.keyword.messagehub}} events" caption-side="top"}

## Where to view the events
{: #ui}

{{site.data.keyword.cloudaccesstrailshort}} events are available in the {{site.data.keyword.cloudaccesstrailshort}} **account domain** that is available in the {{site.data.keyword.cloud_notm}} location (region) where the events are generated.

Events that are generated by an instance of the {{site.data.keyword.messagehub}} service are automatically forwarded to the {{site.data.keyword.at_full_notm}} service instance that is available in the same location.

{{site.data.keyword.at_full_notm}} can have only one instance per location. To view events, you must access the web UI of the {{site.data.keyword.at_full_notm}} service in the same location where your service instance is available. For more information, see [Launching the web UI through the {{site.data.keyword.cloud_notm}} UI](/docs/activity-tracker?topic=activity-tracker-getting-started#gs_step4){: external}.


## How to enable message audit events
{: #enable-message-events}

Message audit events can be enabled on a per topic basis. To do so, complete the following steps:

1. Install {{site.data.keyword.messagehub}} CLI plug-in v2.3 or later: 

   ```text
   ibmcloud plugin install event-streams
   ```
   {: pre}

2. Enable message audit on an existing topic:

   ```text
   ibmcloud es topic-update <topic-name> --config message.audit.enable=true
   ```
   {: pre}

   Or create a new topic with message audit enabled:

   ```text
   ibmcloud es topic-create <topic-name> --partitions <number-of-partitions> --config message.audit.enable=true
   ```
   {: pre}

After the topic's message audit config is updated, it takes about 5 minutes for message audit events to show up in {{site.data.keyword.cloudaccesstrailshort}}.
{: important}

Additionally, be aware of the implications of enabling message audit events:

1. An internal Kafka topic is used for streaming events to {{site.data.keyword.cloudaccesstrailshort}}, thus it uses a small amount of the cluster's network bandwidth and storage. Typically throughput is less than 1 KB/s, and storage does not exceed 1 GB.
   
2. Because more events are sent to {{site.data.keyword.cloudaccesstrailshort}}, this incurs extra storage costs for {{site.data.keyword.cloudaccesstrailshort}}. Each event's size is about 1 KB, a rough estimation of how much storage it takes: Assuming cluster has 100 topics, each topic has 10 clients actively producing and consuming, each client runs on three different locations, then it generates 100x10x3=3000 events per hour, that is 2 GB per month.
