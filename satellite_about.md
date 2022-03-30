---

copyright:
  years: 2022
lastupdated: "2022-03-30"

keywords: IBM Event Streams, Satellite

subcollection: EventStreams

---

{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}
{:beta: .beta}

# About {{site.data.keyword.satellitelong}} for {{site.data.keyword.messagehub}}
{: #satellite_about}

The {{site.data.keyword.satellitelong}} plan for {{site.data.keyword.messagehub_full}} deploys functionality similar to the Enterprise plan into {{site.data.keyword.satelliteshort}} locations of your choice. Using {{site.data.keyword.satellitelong}}, you can create a hybrid environment that brings the scalability and on-demand flexibility of public cloud services to the applications and data that run in your secure private cloud.

For a detailed comparison of the {{site.data.keyword.messagehub}} plans and the functionality of each, refer to [Choosing your plan](/docs/EventStreams?topic=EventStreams-plan_choose).

The {{site.data.keyword.messagehub}} {{site.data.keyword.satelliteshort}} plan does not yet provide the compliance certifications that the Enterprise or Standard plans conform to. {: important}

## Overview
{: #satellite_overview}

To deploy {{site.data.keyword.messagehub}} into a {{site.data.keyword.satelliteshort}} location, the following high-level steps must be completed and are detailed in [Provisioning Event Streams for Satellite](/docs/EventStreams?topic=EventStreams-satellite-provisioning):

1. Provision an {{site.data.keyword.satellitelong_notm}} location and its control plane in your account. It enables you to bring your own hosts to the {{site.data.keyword.cloud}} and provision {{site.data.keyword.cloud_notm}} services onto your hosts. 

2. Set up service-to-service authorization between {{site.data.keyword.messagehub}} and {{site.data.keyword.satelliteshort}} in your account.

3. Provision and attach host compute infrastructure to your {{site.data.keyword.satelliteshort}} location. {{site.data.keyword.messagehub}} will use the hosts when it is provisioned. {{site.data.keyword.messagehub}} provides high availability using multi-zone region deployment to protect against single points of failure. You must provision and balance the host compute infrastructure for the zones in your satellite location. Host compute requirements are listed in the provisioning details.

4. Provision an {{site.data.keyword.messagehub}} service instance in your account and a service cluster in your {{site.data.keyword.satelliteshort}} location.

5. Configure block storage for your {{site.data.keyword.satelliteshort}} location that {{site.data.keyword.messagehub}} will then allocate during the service instance provision process.  {{site.data.keyword.messagehub}} uses the block storage for the retention of your message data.

    The block storage capacity cannot be scaled up for the initial release of {{site.data.keyword.satellitelong_notm}} plan for {{site.data.keyword.messagehub}}.

    {{site.data.keyword.messagehub}} stores three replicas of your message data to ensure the highest level of resilience across three availability zones. When {{site.data.keyword.messagehub}} is provisioned for {{site.data.keyword.satelliteshort}}, 2 TB of storage is allocated from your configured block storage infrastructure for each of the three replicas (availability zones). This is equivalent to deploying 6 TB of storage if you run your own Apache Kafka cluster with the same replication policy enabled.

    In addition to the message data retention block storage, storage is allocated by {{site.data.keyword.messagehub}} for managing your message data and for monitoring the operation of the {{site.data.keyword.messagehub}} service instance.

    Specific block storage capacity amounts and supported storage classes are detailed below.

6. Provisioning of {{site.data.keyword.messagehub}} service instance completes and is ready to use.

## Before you begin
{: #satellite_before_you_begin}

1. Refer to the [Satellite usage requirements](https://cloud.ibm.com/docs/satellite?topic=satellite-requirements).
2. Set up the [IBM Cloud command-line interface (CLI)](https://cloud.ibm.com/docs/satellite?topic=satellite-setup-cli), the plug-in for {{site.data.keyword.satelliteshort}} commands, and other related CLIs.
3. The {{site.data.keyword.messagehub}} service instance provision process uses the Satellite Storage user interface. To enable your access to the Storage UI for Satellite, you must be added to the allowlist. [Contact IBM](https://www.ibm.com/contact/us/en/) to learn more.
4. The [Provisioning Event Streams for Satellite](/docs/EventStreams?topic=EventStreams-satellite-provisioning) steps simplify block storage configuration and assignment by using the Storage UI for Satellite.  At this time, the Storage UI requires your account to be allowlisted to access it.  To enable your access [Contact IBM](https://www.ibm.com/contact/us/en/) to learn more.  If you prefer to use the CLI to create the storage configuration from templates, and then assign that configuration to the {{site.data.keyword.messagehub}} messagehub service cluster you do not need access to the Storage UI for Satellite.
5. {{site.data.keyword.messagehub}} uses block storage for retention of message data, management of message data, and for monitoring the operation of the {{site.data.keyword.messagehub}} service instance. During the provision of the {{site.data.keyword.messagehub}} service instance, the block storage configuration completes. To prepare for that configuration, review the following:

    1. The [What is supported](/docs/EventStreams?topic=EventStreams-plan_choose#what_is_supported) information notes the flexibility of the {{site.data.keyword.satelliteshort}} infrastructure provided can impact the actual maximum throughput {{site.data.keyword.messagehub}} {{site.data.keyword.satelliteshort}} can provide.  The performance of the hosts, network latency, block storage performance can all impact maximum throughput.

	   As you review the block storage information below and select a storage class, to achieve a maximum throughput you should select block storage that provides a minimum of **4 IOPS per GB** of storage and that can support 75MB/s disk writes and 25MB/s disk reads concurrently.

	2. To configure block storage, {{site.data.keyword.satellitelong_notm}} provides configuration templates for several storage infrastructure providers. The [Understanding Satellite storage templates](https://cloud.ibm.com/docs/satellite?topic=satellite-sat-storage-template-ov) information explains how the storage templates work and how to configure them using the IBM Cloud CLI. The {{site.data.keyword.messagehub}} service instance provision helps simplify the configuration by prompting for the needed configuration. To prepare for the configuration, perform the following steps:
    
        1. Review the supported block storage classes in the [Storage class reference](https://cloud.ibm.com/docs/satellite?topic=satellite-storage-class-ref).
	3. Identify the block storage classes availabe for your storage infrastructure provider.
	4. When available, select a block storage class that has a **Volume Binding Mode** = **WaitForFirstConsumer**.
    5. The following table outlines the amount of block storage that will be allocated by {{site.data.keyword.messagehub}}.
    
	| Usage | Amount allocated | Total |
	| --- | --- | --- |
	| Message data retention | 2 TB x 3 replicas/availability zones | 6 TB total |
	| Message data management | 250 GB x 3 replicas/availability zones | 750 GB total |
	| Service instance monitoring | 125 GB x 3 replicas/availability zones | 375 GB total |
	{: caption="Table 1. Block storage usage" caption-side="bottom"}

	The information regarding the amount of storage is for a single {{site.data.keyword.messagehub}} {{site.data.keyword.satelliteshort}} service instance. If multiple {{site.data.keyword.messagehub}} {{site.data.keyword.satelliteshort}} instances are required, the information applies to each instance of {{site.data.keyword.messagehub}}.
{: note}

## Provision {{site.data.keyword.messagehub}}
{: #satellite_provision_es}

Complete the steps in [Provisioning Event Streams for Satellite](/docs/EventStreams?topic=EventStreams-satellite-provisioning).
