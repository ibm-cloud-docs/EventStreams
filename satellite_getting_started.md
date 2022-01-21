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

Use the Satellite plan to deploy an Enterprise plan into Satellite locations of your choice. Using {{site.data.keyword.satellitelong_notm}}, you can create a hybrid environment that brings the scalability and on-demand flexibility of public cloud services to the applications and data that run in your secure private cloud.

## Overview
{: #overview}

To deploy Event Streams into a Satellite location, the following high-level steps must be completed:

1. Provision an IBM Cloud Satellite location and its control pane. It enables you to bring your own hosts to the IBM Cloud and provision IBM Cloud services onto your machines. Host compute and storage requirements are detailed in each of the infrastructures' (for example, AWS, and on-premises) specific topics.

2. Provision and attach host compute infrastructure to your Satellite location that will be used by Event Streams.

3. Set up service-to-service authorization between Event Streams and Satellite within your account.

4. Provision a service instance of Event Streams in your account, and a service cluster in your Satellite location.

5. Configure block storage and assign it to the Event Streams instance that you provisioned. Event Streams will use the block storage for the retention of your message data.

    The storage capacity cannot be scaled up for the initial release of Event Streams for Satellite.

    Event Streams stores three replicas of your message data to ensure the highest level of resilience across three availability zones. When Event Streams is provisioned for Satellite, 2 TB of storage is allocated from your configured block storage infrastructure for each of the three replicas (availability zones). This is equivalent to deploying 6 TB of storage if you run your own Apache Kafka cluster with the same replication policy enabled.

    In addition to the message data retention block storage, storage is allocated by Event Streams for managing your message data and for monitoring the operation of the Event Streams service instance.

    Specific storage capacity amounts are detailed in each of the infrastructure (for example, AWS, and on-premises) specific topics.

6. Provisioning Event Streams completes and is ready to use.

## Before you begin
{: #satellite_before_you_begin}

- Refer to the Satellite usage requirements.
- Set up the IBM Cloud command-line interface (CLI), the plug-in for Satellite commands, and other related CLIs.
- Create a Satellite location, see [Setting up Satellite locations](). Follow the steps in [Manually creating Satellite locations]().
  - For the management location, choose Dallas or Washington DC.
  - If you create your Satellite location using AWS infrastructure, adjust the Satellite location host zones to AWS-default zone names, for example, us-east-1a, us-east-1b, or us-east-1c.
- Before you procede, set up your Satellite location and ensure that the Satellite control plane is up and running.

## Restrictions of the Satellite plan
{: #satellite_restrictions}

IBM Event Streams enabled by IBM Cloud Satellite is restricted to Satellite locations managed from Dallas and Washington D.C 
and supports Satellite locations on Amazon Web Services (AWS) and on-premises.

The following functions are not supported on the Satellite plan for {{site.data.keyword.messagehub}.

- IAM IP address access restrictions
- Bring Your Own Key (BYOK)
- Schema Registry
- Cloud Service Endpoint support
- Stream to Cloud Object Storage using SQL Query
- Activity tracker
- Monitoring Event Streams metrics using IBM Cloud Monitoring
