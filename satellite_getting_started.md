---

copyright:
  years: 2015, 2022
lastupdated: "2022-01-18"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: EventStreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}


# Getting Started
{: #satellite-get-started}

With IBM Cloud™ Databases (ICD) enabled by IBM Cloud Satellite, you can deploy ICD instances into a Satellite location. (ICD) enabled by IBM Cloud Satellite currently supports the following ICD managed database services:
- [{{site.data.keyword.databases-for-etcd}}](/docs/databases-for-etcd)
- [{{site.data.keyword.databases-for-postgresql}}](/docs/databases-for-postgresql)
- [{{site.data.keyword.databases-for-redis}}](/docs/databases-for-redis)
- [{{site.data.keyword.messages-for-rabbitmq}}](/docs/messages-for-rabbitmq)

 Once your Satellite location instance is deployed, ICD will install an ICD Satellite service cluster in your Satellite location into which your database instances will be deployed. 

 Your ICD service cluster can operate multiple database instances, even with different database types. For instance, you may operate a {{site.data.keyword.databases-for-etcd}} and a {{site.data.keyword.databases-for-postgresql}} instance on the same service cluster. 

The service cluster name is based on the first database instance, even if multiple instances exist. For example, if your service cluster has both a {{site.data.keyword.databases-for-etcd}} and a {{site.data.keyword.databases-for-postgresql}} instance on the same service cluster, the name will be based on your {{site.data.keyword.databases-for-etcd}} instance.
{: .note}

ICD enabled by IBM Cloud Satellite supports Satellite locations on [Amazon Web Services (AWS)](/docs/satellite?topic=satellite-aws) and [on-premises](/docs/cloud-databases?topic=cloud-databases-satellite-on-prem). 
{: shortdesc}

## Before you begin
{: #before-begin}

- Refer to the [Satellite Usage requirements](/docs/satellite?topic=satellite-requirements).
- Be sure you have set up the [IBM Cloud command-line interface (CLI)](/docs/satellite?topic=satellite-setup-cli), the plug-in for Satellite commands, and other related CLIs.
- If you have not already created a Satellite location, see [Setting up Satellite locations](/docs/satellite?topic=satellite-locations). We recommend following the steps in the [Manually creating Satellite locations](/docs/satellite?topic=satellite-locations#location-create) documentation.
    - For the management location, choose **Washington DC**. If creating your Satellite location on AWS, adjust the **host zones** to AWS-default zone names, for example: **us-east-1a**, **us-east-1b**, **us-east-1c**.

As ICD enabled by IBM Cloud Satellite solely supports resource deployment in the `us-east` region, you must choose the **Washington DC** location when provisioning. 
{: .note}

- Before proceeding with **Step 1**, you should have set up your Satellite location properly and ensured the Satellite control plane is up and running.
