---

copyright:
  years: 2015, 2022
lastupdated: "2022-01-21"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: EventStreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}

# Getting started with the IBM Satellite plan for Event Streams
{: #satellite_getting_started}

Use the Satellite plan to deploy Enterprise plan functionality into Satellite locations of your choice. Using {{site.data.keyword.satellitelong_notm}}, you can create a hybrid environment that brings the scalability and on-demand flexibility of public cloud services to the applications and data that run in your secure private cloud.

## Overview
{: #overview}

To deploy Event Streams into a Satellite location, the following high-level steps must be completed:

1. Provision an IBM Cloud Satellite location and its control pane. It enables you to bring your own hosts to the IBM Cloud and provision IBM Cloud services onto your machines. Host compute and storage requirements are detailed in each of the infrastructures' (for example, AWS and on-premises) specific topics.

2. Provision and attach host compute infrastructure, and create the block storage configuration for your Satellite location.  Event Streams will use the hosts and block storage when it is provisioned.

3. Set up service-to-service authorization between Event Streams and Satellite within your account.

4. Provision an Event Streams service instance in your account, and a service cluster in your Satellite location.

5. Create the block storage and assignment for the Event Streams service cluster that was provisioned. Event Streams will use the block storage for the retention of your message data.

    The storage capacity cannot be scaled up for the initial release of IBM Satelite plan for Event Streams.

    Event Streams stores three replicas of your message data to ensure the highest level of resilience across three availability zones. When Event Streams is provisioned for Satellite, 2 TB of storage is allocated from your configured block storage infrastructure for each of the three replicas (availability zones). This is equivalent to deploying 6 TB of storage if you run your own Apache Kafka cluster with the same replication policy enabled.

    In addition to the message data retention block storage, storage is allocated by Event Streams for managing your message data and for monitoring the operation of the Event Streams service instance.

    Specific storage capacity amounts are detailed in each of the infrastructure (for example, AWS and on-premises) specific topics.

6. Provisioning of Event Streams service instance completes and is ready to use.

## Before you begin
{: #satellite_before_you_begin}

- Refer to the [Satellite usage requirements](https://cloud.ibm.com/docs/satellite?topic=satellite-requirements).
- Set up the [IBM Cloud command-line interface (CLI)](https://cloud.ibm.com/docs/satellite?topic=satellite-setup-cli), the plug-in for Satellite commands, and other related CLIs.
- Create a Satellite location, see [Setting up Satellite locations](https://cloud.ibm.com/docs/satellite?topic=satellite-locations). Follow the steps in [Manually creating Satellite locations](https://cloud.ibm.com/docs/satellite?topic=satellite-locations#location-create-manual).
  - Supported options for the Satellite location Managed from field include
    - Dallas
    - Washington DC
  - As noted in the [Manually creating Satellite locations](https://cloud.ibm.com/docs/satellite?topic=satellite-locations#location-create-manual) information, the names of the zones specified in the Satellite location Zone fields must match exactly the names of the corresponding zones in your infrastructure provider where you plan to create hosts
- Before you procede to the steps in the infrastructure specific topic
  - the Satellite location must be provisioned and have a Normal state
  - the Satellite control plane service is running and have a Normal state

## Limitations/Restrictions of the IBM Satellite plan for Event Streams
{: #satellite_restrictions}

- The following infrastruture providers are supported
  - AWS
- Your Satellite location can be Managed from these IBM Cloud data centers
  - Dallas
  - Washington DC
- At this time, the following functions are not supported on the IBM Satellite plan for Event Streams
  - Scale up of message retention storage
  - IAM IP address access restrictions
  - Bring Your Own Key (BYOK)
  - Schema Registry
  - Cloud Service Endpoint support
  - Stream to Cloud Object Storage using SQL Query
  - Activity tracker
  - Monitoring Event Streams metrics using IBM Cloud Monitoring
