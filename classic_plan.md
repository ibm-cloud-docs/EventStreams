---

copyright:
  years: 2015, 2019
lastupdated: "2019-11-04"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: EventStreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:deprecated: .deprecated}

# The Classic plan 
{: #plan_choose_classic}

The Classic plan is deprecated. From November 1, 2019, you can no longer provision new instances of the Classic Plan. However, existing instances will continue to be supported.
From June 30, 2020, the Classic Plan will be retired and no longer supported.Any instance of the Classic Plan still provisioned at this date will be deleted. 
For more information, see 
[IBM {{site.data.keyword.messagehub}} Classic Plan is being retired ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/blog/announcements/ibm-event-streams-classic-plan-is-being-retired){: new_window}.
{: deprecated}

{{site.data.keyword.messagehub}} is available as different plans depending on your requirements. For information about the Standard and Enterprise plans, see [Choosing your plan](/docs/EventStreams?topic=EventStreams-plan_choose#plan_choose).
{: shortdesc}
 

## Migrating from the Classic plan
{: #migrating_from_classic}

{{site.data.keyword.messagehub}} is available as different plans depending on your requirements. You can migrate to either the Enterprise or Standard plans. For information to help you select a plan, see [Choosing your plan](/docs/EventStreams?topic=EventStreams-plan_choose#plan_choose).

For an overview of migrating from the Classic plan to the new Standard plan, see [Upgrading to the new Standard plan](/docs/EventStreams?topic=EventStreams-migrate_classic_plan).

For information about migrating specific capabilities, refer to the following: 
* If you currently use the REST APIs on the Classic plan, see [Migrating the REST APIs](/docs/EventStreams?topic=EventStreams-migrate_rest_apis).
* If you currently use the {{site.data.keyword.mql}} API on the Classic plan, see [Migrating MQ Light to Kafka](/docs/EventStreams?topic=EventStreams-migrate_mqlight).
* If you currently use the Cloud Object Storage bridge or the MQ bridge, see [Migrating to Kafka Connect](/docs/EventStreams?topic=EventStreams-migrate_bridges).

## Classic plan overview
{: #classic_overview}

The Classic plan is appropriate if you require event ingest and distribution capabilities but do not require any additional benefits of the Enterprise plan. The Classic plan offers shared access to a multi-tenant {{site.data.keyword.messagehub}} cluster.


## What's supported by the Classic plan

The following table summarizes what is supported by the plan:


|   |  Classic Plan |
|---|---|
| **Tenancy**  |Multi-tenant   |
|**Availability zones**   | Not supported  |
| **Availability**  |  99.99% |
| **Kafka version on cluster**  | Kafka 1.1 | 
| **Fine-grained access control**  | No  | 
|  **Cloud Service Endpoint support** | No   |
| **Kafka Connect and Kafka Streams supported**  |  Yes | 
| **Maximum number of partitions**  | 100 | 
|**Maximum retention period**   | 1 GB per partition for up to 30 days   |
| **Maximum throughput**  | 1 MB per second per partition  | 
| **Maximum message size**  | 1 MB  | 
| **Maximum number of connected clients**  |Not specified   | 10 000  |
|  **Location (region) availability** |Dallas (us-south)  \n London (eu-gb)   \n Sydney (au-syd)   \n Frankfurt (eu-de) - no {{site.data.keyword.mql}} API   |
| **APIs supported** |  Kafka API   \n Admin REST API   \n Kafka REST API   \n {{site.data.keyword.mql}} API |
| **Cloud Object Storage bridge and MQ bridge supported** | Yes  |
| **Deployment timeframe** | Instantaneous provisioning  | 
{: caption="Table 1. Supported capabilities on Classic plan" caption-side="top"}

