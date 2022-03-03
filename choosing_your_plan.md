---

copyright:
  years: 2015, 2022
lastupdated: "2022-02-15"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka, plan. Enterprise, Standard, Lite

subcollection: EventStreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:note: .note}
{:deprecated: .deprecated}
{:beta: .beta}

# Choosing your plan 

{: #plan_choose}

{{site.data.keyword.messagehub}} is available as Lite plan, Standard plan, Enterprise plan, or {{site.data.keyword.satelliteshort}} plan {: beta} depending on your requirements. 

{: shortdesc}

## Lite plan

{: #plan_lite}

The Lite plan is free for users who want to try out {{site.data.keyword.messagehub}} or build a proof-of-concept. We do not recommend the Lite plan for production use. The Lite plan offers shared access to a multi-tenant {{site.data.keyword.messagehub}} cluster.

## Standard plan

{: #plan_standard}

The Standard plan is appropriate if you require event ingest and distribution capabilities but do not require any additional benefits of the Enterprise plan. The Standard plan offers shared access to a multi-tenant {{site.data.keyword.messagehub}} cluster that seamlessly autoscales as you increase the number of partitions you are using for your workload. 

The architecture is highly available by default. The service is distributed across three availability zones, which means that the cluster is resilient to the failure of a single zone or any component within that zone.


## Enterprise plan 

{: #plan_enterprise}

The Enterprise plan is appropriate if data isolation, performance, and increased retention are important considerations. 
The Enterprise plan includes the following features:

- Exclusive access to a single-tenant {{site.data.keyword.messagehub}} service instance deployed in a highly available multi zone region (MZR).
- Option to provision a single-tenant {{site.data.keyword.messagehub}} service instance in a geographically local but single zone location [(SZR)](/docs/EventStreams?topic=EventStreams-sla#sla_szr).
- Scaling options to customize throughput, storage capacity, or both.

The architecture is highly available when you choose to deploy into a multi-zone region. The service is distributed across three availability zones, which means that the cluster is resilient to the failure of a single zone or any component within that zone.

## Satellite plan (Beta) 
{: beta}

{: #plan_satellite}

The {{site.data.keyword.satelliteshort}} plan is appropriate if you want to deploy an Enterprise plan into {{site.data.keyword.satelliteshort}} locations of your own choice. Using {{site.data.keyword.satellitelong}}, you can create a hybrid environment that brings the scalability and on-demand flexibility of public cloud services to the applications and data that run in your secure private cloud. 
{: beta}

The {{site.data.keyword.satelliteshort}} plan is currently available as a limited access Beta service. To request access to the beta service, refer to the information at [Getting started with the IBM Satellite plan for Event Streams (Beta)](/docs/EventStreams?topic=EventStreams-getting-started-with-the-ibm-satellite-plan-for-event-streams-beta#beta).

## What is supported by the Lite, Standard, Enterprise, and Satellite plans

{: #what_is_supported}

The following table summarizes what is supported by the plans:

|   | Lite plan  |  Standard plan |  Enterprise plan  |  {{site.data.keyword.satelliteshort}} plan (Beta) |
|---|---|---|---|---|
| **Tenancy**  |Multi-tenant   | Multi-tenant  | Single tenant | Single tenant     |
|**Availability zones**   |  3  |   3  |3    \n   (1 in single zone locations)   |   3  |
| **Availability**  |  99.99% [^tabletext](/docs/EventStreams?topic=EventStreams-plan_choose#footnote_lite) |  99.99% | 99.99%   \n  (99.9% in single zone locations) [^tabletext2](/docs/EventStreams?topic=EventStreams-plan_choose#footnote_plans)  |  Not applicable    |
| **Kafka version on cluster**  | Kafka 2.8 | Kafka 2.8  | Kafka 2.8 |  Kafka 2.8   |
| **Kafka Connect and Kafka Streams supported**  | No |  Yes | Yes  |   Yes  |
| **Stream to Cloud Object Storage using SQL Query**  | No |  Yes | Yes  |   No  |
| **Managed Schema Registry supported**  | No |  No |  Yes |  No   |
| **Customer-managed encryption**  | No  |  No |  Yes |  No   |
| **Fine-grained access control**  | Yes  |  Yes |  Yes |  Yes   |
| **Activity tracker events**  | No  |  Yes |  Yes |  Not during Beta   |
| **Monitoring Event Streams metrics using IBM Cloud Monitoring**  | Yes  |  Yes |  Yes |  Yes  |
|  **Cloud Service Endpoint support** | No   | No  |  Yes |  Not applicable  |
|  **Scale plan capacity** | No   | No  |  Yes |   No  |
| **Maximum number of partitions**  | 1  [<sup>3</sup>](/docs/EventStreams?topic=EventStreams-plan_choose#footnote_partitions_lite)  | 100   |3000 - 9000 scales with throughput [<sup>4</sup>](/docs/EventStreams?topic=EventStreams-plan_choose#footnote_partitions) | 3000    |
|**Maximum retention limits**   | 100 MB for the partition   | 1 GB per partition  | 2 TB - 12 TB of scalable usable storage [<sup>5</sup>](/docs/EventStreams?topic=EventStreams-plan_choose#footnote_retention)|  2 TB of scalable usable storage   |
| **Maximum throughput**  | 100 KB per second per partition  |  1 MB per second per partition (20 MB per service instance) | 150 MB/s - 450 MB/s of scalable throughput [<sup>6</sup>](/docs/EventStreams?topic=EventStreams-plan_choose#footnote_throughput)  | TBD for Beta   |
| **Maximum message size**  | 1 MB  | 1 MB   | 1 MB |   1 MB  |
| **Maximum number of connected clients**  | 5   | 500  | 10 000  |   10 000  |
|  **Location (region) availability** | Dallas (us-south)  |  **Multizone location (MZR)**   \n Dallas (us-south)   \n Washington (us-east)   \n London (eu-gb)   \n Sydney (au-syd)   \n Frankfurt (eu-de)  \n Tokyo (jp-tok)   \n  Osaka (jp-osa)  \n Toronto (ca-tor)   \n Sao Paulo (br-sao)   |   **Multizone location (MZR)**   \n Dallas (us-south)   \n Washington (us-east)   \n London (eu-gb)   \n Sydney (au-syd)   \n Frankfurt (eu-de)   \n  Tokyo (jp-tok)   \n  Osaka (jp-osa)  \n Toronto (ca-tor)   \n Sao Paulo (br-sao)    \n    \n  **Single zone location (SZR)**   \n Seoul (seo01)   \n Chennai (che01)  |  Your own {{site.data.keyword.satelliteshort}} locations   |
| **APIs supported** |  Kafka API   \n Admin REST API  \n REST Producer API |  Kafka API   \n Admin REST API   \n REST Producer API    |  Kafka API   \n Admin REST API   \n REST Producer API   \n  Schema Registry API  | Kafka API   \n Admin REST API   \n REST Producer API    |
| **Deployment timeframe** | Instantaneous provisioning  | Instantaneous provisioning    |Expect provisioning to take up to 3 hours. Because Enterprise has its own dedicated resources for each cluster, it requires more time for provisioning  |  If all your infrastructure is correctly in place, expect provisioning to take up to 1 hour because {{site.data.keyword.satelliteshort}} has its own dedicated resources for each instance   |
| **Compliance** |GDPR   \n  Privacy Shield  | GDPR   \n  Privacy Shield   \n  ISO 27001, 27017, 27018, 2701    \n  SOC 1 Type     \n  SOC 2 Type 2   \n  PCI |  GDPR   \n Privacy Shield   \n ISO 27001, 27017, 27018, 2701   \n  SOC 1 Type 2   \n  SOC 2 Type 2 \n HIPAA ready    \n  PCI |   Not applicable for Beta  |
| **Manage security and compliance**  | No  |  No |  Yes |  No   |

For more information about limits, see [limits and quotas](/docs/EventStreams?topic=EventStreams-kafka_quotas).

### Footnotes

{: #footnote_plans notoc}

1. After 30 days of inactivity, your instance is deleted. (Inactivity is defined as a zero bytes_out metric, even though you might create a partition or produced messages.) {: #footnote_lite notoc}
2. For more information about availability, see [single zone location deployments](/docs/EventStreams?topic=EventStreams-sla#sla_szr). {: #footnote_szr notoc}
3. If you migrate from the Lite to the Standard plan, allow a few minutes for the cached limit of one partition to clear. You can then take advantage of the 100 partition limit for the Standard plan. {: #footnote_partitions_lite notoc}
4. This value scales relative to the maximum throughput. For example, if you have a throughput of 150 MB/s the maximum partitions would be 3000, for a throughput of 300 MB/s, 6000 and for 450 MB/s, 9000. This limit is a hard limit for partitions on the Enterprise plan. If you reach this limit, you can no longer create topics. To increase the number of partitions beyond the maximum, [contact IBM ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/get-support?topic=get-support-open-case&interface=ui#creating-support-case){: new_window}. {: #footnote_partitions notoc}
5. Maximum message retention (storage) can be specified when the service instance is created. Storage can be later scaled independently as demands increase. The minimum usable storage available is dependent upon the number of capacity units that are configured for the service instance. For more information about capacity options, see [Scaling Event Streams Capacity](/docs/EventStreams?topic=EventStreams-ES_scaling_capacity). {: #footnote_retention notoc}
6. Maximum throughput can be specified when the service instance is created. Throughput is expressed as the sum of the number of bytes per second that can be both sent and received in a service instance. Throughput can be later scaled as demands increase. 
Although throughput scaling is independent of storage, a defined minimum storage amount is required for each tier. 
For more information about capacity options, see [Scaling Event Streams capacity](/docs/EventStreams?topic=EventStreams-ES_scaling_capacity). {: #footnote_throughput notoc}

