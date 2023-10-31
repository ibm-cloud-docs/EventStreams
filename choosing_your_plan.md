---

copyright:
  years: 2015, 2023
lastupdated: "2023-10-31"

keywords: plan, Enterprise, Standard, Lite, pricing, Satellite, throughput, partitions, tenancy, compliance

subcollection: EventStreams

---

{{site.data.keyword.attribute-definition-list}}

# Choosing your plan
{: #plan_choose}

{{site.data.keyword.messagehub}} is available as Lite plan, Standard plan, Enterprise plan, or {{site.data.keyword.satelliteshort}} plan depending on your requirements.
{: shortdesc}

For information about {{site.data.keyword.messagehub}} plan pricing, see the [catalog](https://cloud.ibm.com/catalog){: external}. Search for `{{site.data.keyword.messagehub}}`, then click the {{site.data.keyword.messagehub}} tile to go to the provisioning page.

## Lite plan
{: #plan_lite}

The Lite plan is free for users who want to try out {{site.data.keyword.messagehub}} or build a proof-of-concept. Do not use the Lite plan for production use. It offers shared access to a multi-tenant {{site.data.keyword.messagehub}} cluster.

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

## Satellite plan
{: #plan_satellite}

The {{site.data.keyword.satellitelong}} plan is appropriate if you want to deploy an Enterprise plan into {{site.data.keyword.satelliteshort}} locations of your own choice. Using {{site.data.keyword.satelliteshort}}, you can create a hybrid environment that brings the scalability and on-demand flexibility of public cloud services to the applications and data that run in your secure private cloud.

The {{site.data.keyword.messagehub}} {{site.data.keyword.satelliteshort}} plan does not yet provide the compliance certifications that the Enterprise or Standard plans conform to.
{: important}

## What is supported by the Lite, Standard, Enterprise, and Satellite plans
{: #what_is_supported}

The following table summarizes what is supported by the plans:

|   | Lite plan  |  Standard plan |  Enterprise plan  |  {{site.data.keyword.satelliteshort}} plan  |
|---|---|---|---|---|
| **Tenancy**  |Multi-tenant   | Multi-tenant  | Single tenant | Single tenant     |
| **Availability zones**   |  3  |   3  |3    \n   (1 in single zone locations)   |   3  |
| **Availability**  |  99.99% [^tabletext1] |  99.99% | 99.99%  (99.9% in single zone locations) [^tabletext2]  |  Not applicable    |
| **Kafka version on cluster**  | Kafka 3.3 | Kafka 3.3  | Kafka 3.3 |  Kafka 3.3   |
| **Kafka Connect and Kafka Streams supported**  | No |  Yes | Yes  |   Yes  |
| **Stream to Cloud Object Storage by using {{site.data.keyword.sqlquery_short}}**  | No |  Yes | Yes  |   No  |
| **Managed Schema Registry supported**  | No |  No |  Yes |  Yes [^tabletext3]  |
| **Customer-managed encryption**  | No  |  No |  Yes [^tabletext4]  |  No   |
| **Fine-grained access control**  | Yes  |  Yes |  Yes  |  Yes   |
| **Activity tracker events**  | No  |  Yes |  Yes |  No   |
| **Monitoring Event Streams metrics by using IBM Cloud Monitoring**  | Yes  |  Yes |  Yes |  Yes  |
| **Private Networking (Cloud Service Endpoint support)** | No   | No  |  Yes |  Not applicable  |
| **Scale plan capacity** | No   | No  |  Yes |   No  |
| **Maximum number of partitions**  | 1 [^tabletext5]  | 100   |3000 - 9000 scales with throughput [^tabletext6] | 3000    |
| **Maximum retention limits**   | 100 MB for the partition   | 1 GB per partition  | 2 TB - 12 TB of scalable usable storage [^tabletext7] |  2 TB of usable storage   |
| **Maximum throughput**  | 100 KB per second per partition  |  1 MB per second per partition (20 MB per service instance) | 150 MB/s - 450 MB/s of scalable throughput [^tabletext8] | 150 MB/s [^tabletext9]  |
| **Maximum message size**  | 1 MB  | 1 MB   | 1 MB |   1 MB  |
| **Maximum number of connected clients**  | 5   | 500  | 10 000  |   10 000  |
| **Location (region) availability** | Dallas (us-south)  |  **Multizone location (MZR)**   \n Dallas (us-south)   \n Sao Paulo (br-sao)   \n Toronto (ca-tor)   \n Washington (us-east)   \n Frankfurt (eu-de)   \n London (eu-gb)   \n Madrid (eu-es)   \n  Osaka (jp-osa)   \n Sydney (au-syd)   \n Tokyo (jp-tok)|   **Multizone location (MZR)**  \n Dallas (us-south)   \n Sao Paulo (br-sao)   \n Toronto (ca-tor)   \n Washington (us-east)   \n Frankfurt (eu-de)   \n London (eu-gb)   \n Madrid (eu-es)   \n  Osaka (jp-osa)   \n Sydney (au-syd)   \n Tokyo (jp-tok)\n    \n  **Single zone location (SZR)**   \n Chennai (che01)  |  **Your Satellite location managed in**   \n Dallas   \n Sao Paulo   \n  Toronto   \n Washington   \n Frankfurt   \n London   \n Osaka   \n Sydney   \n Tokyo   |
| **APIs supported** |  Kafka API   \n Admin REST API  \n REST Producer API |  Kafka API   \n Admin REST API   \n REST Producer API    |  Kafka API   \n Admin REST API   \n REST Producer API   \n  Schema Registry API  | Kafka API   \n Admin REST API   \n REST Producer API   \n  Schema Registry API [^tabletext10] |
| **Deployment timeframe** | Instantaneous provisioning  | Instantaneous provisioning    |Expect provisioning to take up to 3 hours. As Enterprise has its own dedicated resources for each cluster, it requires more time for provisioning.  |  If all your infrastructure is correctly in place, expect provisioning to take up to 1 hour because {{site.data.keyword.satelliteshort}} has its own dedicated resources for each instance.   |
| **Compliance** |GDPR   \n  Privacy Shield  | GDPR   \n  Privacy Shield   \n  ISO 27001, 27017, 27018, 2701    \n  SOC 1 Type     \n  SOC 2 Type 2   \n  SOC 3   \n  PCI DSS \n ISMAP \n C5  |  GDPR   \n Privacy Shield   \n ISO 27001, 27017, 27018, 2701   \n  SOC 1 Type 2   \n  SOC 2 Type 2   \n  SOC 3   \n  HIPAA ready   \n  PCI DSS  \n ISMAP \n C5 \n IRAP |   GDPR   \n   ISO 27001, 27017, 27018, 2701 [^tabletext11]  |
| **Manage security and compliance**  | No  |  No |  Yes |  No   |
| **IAM address restrictions** | No | Yes | Yes | No |
| **IAM token authentication only** | No | No | Yes | Yes |
| **Mirroring** | No | No | Yes | No |
{: caption="Table 1. Plan comparison table" caption-side="bottom"}

[^tabletext1]: After 30 days of inactivity, your instance is deleted. (Inactivity is defined as a zero bytes_out metric, even though you might create a partition or produced messages.)

[^tabletext2]: For more information about availability, see [single zone location deployments](/docs/EventStreams?topic=EventStreams-sla#sla_szr).

[^tabletext3]: The Schema Registry API is not automatically enabled on the Satellite plan. For more information about how to enable it, see [Enable the schema registry API](/docs/EventStreams?topic=EventStreams-satellite-provisioning#satellite-enable-schema-registry).

[^tabletext4]: Only supported on clusters that were created after October 2019.

[^tabletext5]: If you migrate from the Lite to the Standard plan, allow a few minutes for the cached limit of one partition to clear. You can then take advantage of the 100 partition limit for the Standard plan.

[^tabletext6]: This value scales relative to the maximum throughput. For example, if you have a throughput of 150 MB/s the maximum partitions would be 3000, for a throughput of 300 MB/s, 6000 and for 450 MB/s, 9000. This limit is a hard limit for partitions on the Enterprise plan. If you reach this limit, you can no longer create topics. To increase the number of partitions beyond the maximum, [contact IBM](/docs/get-support?topic=get-support-open-case&interface=ui#creating-support-case){: external}.

[^tabletext7]: Maximum message retention (storage) can be specified when the service instance is created. Storage can be later scaled independently as demands increase. The minimum usable storage available is dependent upon the number of capacity units that are configured for the service instance. For more information about capacity options, see [Scaling Event Streams capacity](/docs/EventStreams?topic=EventStreams-ES_scaling_capacity).

[^tabletext8]: Maximum throughput can be specified when the service instance is created. Throughput is expressed as the sum of the number of bytes per second that can be both sent and received in a service instance. Throughput can be later scaled as demands increase. Although throughput scaling is independent of storage, a defined minimum storage amount is required for each tier. For more information about capacity options, see [Scaling Event Streams capacity](/docs/EventStreams?topic=EventStreams-ES_scaling_capacity).

[^tabletext9]: The {{site.data.keyword.satelliteshort}} plan design and deployment is similar to the Enterprise plan and provides a maximum throughput of 150 MB/s. The flexibility of the {{site.data.keyword.satelliteshort}} environment can impact the actual maximum throughput. When you provide infrastructure for your {{site.data.keyword.satelliteshort}} deployment, the following items might impact throughput: 1) Performance of hosts that are attached to your {{site.data.keyword.satelliteshort}} location for use by {{site.data.keyword.messagehub}}. 2) Type, configuration, and performance of the block storage provided. 3) Network latency between the hosts, block storage, and the {{site.data.keyword.satelliteshort}} location. 4) For information about infrastructure, see [Before you begin](/docs/EventStreams?topic=EventStreams-satellite_about#satellite_before_you_begin).

[^tabletext10]: The Schema Registry API is not automatically enabled on the Satellite plan. For information about how to enable it, see [Enable the schema registry API](/docs/EventStreams?topic=EventStreams-satellite-provisioning#satellite-enable-schema-registry).

[^tabletext11]: All compliance certifications available on the Standard and Enterprise plans are currently not available on the {{site.data.keyword.satelliteshort}} plan. Adding the same certifications to the {{site.data.keyword.satelliteshort}} plan is in process. For general {{site.data.keyword.satelliteshort}} compliance standards information, see [Platform compliance and certification](/docs/satellite?topic=satellite-compliance) and [Compliance standards FAQ](/docs/satellite?topic=satellite-faqs#standards){: external}.

For more information about limits, see [limits and quotas](/docs/EventStreams?topic=EventStreams-kafka_quotas).
