---

copyright:
  year: 2022
lastupdated: "2022-02-09"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: EventStreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}
{:beta: .beta}


# Getting started with the IBM Satellite plan for Event Streams (Beta)
{: #satellite_getting_started}

Use the {{site.data.keyword.satelliteshort}} plan to deploy Enterprise plan functionality into {{site.data.keyword.satelliteshort}} locations of your choice. Using {{site.data.keyword.satellitelong}}, you can create a hybrid environment that brings the scalability and on-demand flexibility of public cloud services to the applications and data that run in your secure private cloud.
{: beta}

## Beta
{: #satellite_beta}

The {{site.data.keyword.satellitelong}} plan for {{site.data.keyword.messagehub_full}} is currently available as a limited access Beta service and is only visible to approved users.

Review the IBM Terms for usage of the Beta service at [IBM Cloud (Public Cloud) Service Description](https://www.ibm.com/support/customer/csol/terms?id=i126-6605&lc=en#detail-document), see section *Beta Services*.

Raise a [support ticket](/docs/get-support?topic=get-support-open-case&interface=ui#creating-support-case) to request access to the beta service.

- IBM Internal users:
  - Log in using the ibmcloud CLI.
  - Run the following command to get your account GUID: `bx account list`.
  - Include the account GUID value to be given access in your ticket.
  
- Users outside IBM:
  - Include the account ID to be given access in your ticket.
  - Wait for response to your ticket before you attempt to access the {{site.data.keyword.messagehub}} Beta service.

### Example request
{: #satellite_example_request}

```
We request access to the IBM Satellite plan for Event Streams (Beta).

The account to authorize:  xxxxxxxxxxxxx
```
{: codeblock}

## Overview
{: #overview}

To deploy {{site.data.keyword.messagehub_full}} into a {{site.data.keyword.satelliteshort}} location, the following high-level steps must be completed:

1. Provision an {{site.data.keyword.satellitelong_notm}} location and its control plane. It enables you to bring your own hosts to the {{site.data.keyword.cloud}} and provision {{site.data.keyword.cloud_notm}} services onto your machines. Host compute and storage requirements are detailed in each of the infrastructure's (for example, AWS, and on-premises) specific topics.

2. Provision and attach host compute infrastructure, and create the block storage configuration for your {{site.data.keyword.satelliteshort}} location. {{site.data.keyword.messagehub}} will use the hosts and block storage when it is provisioned.

3. Set up service-to-service authorization between {{site.data.keyword.messagehub}} and {{site.data.keyword.satelliteshort}} within your account.

4. Provision an {{site.data.keyword.messagehub}} service instance in your account, and a service cluster in your {{site.data.keyword.satelliteshort}} location.

5. Create the block storage assignment for the {{site.data.keyword.messagehub}} service cluster that was provisioned. 
{{site.data.keyword.messagehub}} will use the block storage for the retention of your message data.

    The storage capacity cannot be scaled up for the initial release of {{site.data.keyword.satellitelong_notm}} plan for {{site.data.keyword.messagehub}}.

    {{site.data.keyword.messagehub}} stores three replicas of your message data to ensure the highest level of resilience across three availability zones. When {{site.data.keyword.messagehub}} is provisioned for {{site.data.keyword.satelliteshort}}, 2 TB of storage is allocated from your configured block storage infrastructure for each of the three replicas (availability zones). This is equivalent to deploying 6 TB of storage if you run your own Apache Kafka cluster with the same replication policy enabled.

    In addition to the message data retention block storage, storage is allocated by {{site.data.keyword.messagehub}} for managing your message data and for monitoring the operation of the {{site.data.keyword.messagehub}} service instance.

    Specific storage capacity amounts are detailed in each of the infrastructure (for example, AWS and on-premises) specific topics.

6. Provisioning of {{site.data.keyword.messagehub}} service instance completes and is ready to use.

## Before you begin
{: #satellite_before_you_begin}

1. Refer to the [Satellite usage requirements](https://cloud.ibm.com/docs/satellite?topic=satellite-requirements).
2. Set up the [IBM Cloud command-line interface (CLI)](https://cloud.ibm.com/docs/satellite?topic=satellite-setup-cli), the plug-in for {{site.data.keyword.satelliteshort}} commands, and other related CLIs.
3. Create a {{site.data.keyword.satelliteshort}} location, see [Setting up Satellite locations](/docs/satellite?topic=satellite-locations). Follow the steps in [Manually creating Satellite locations](/docs/satellite?topic=satellite-locations#location-create-manual).

  Supported options for the {{site.data.keyword.satelliteshort}} location Managed from field include:
  
  - Dallas
  - Washington DC
    
  As noted in the [Manually creating Satellite locations](/docs/satellite?topic=satellite-locations#location-create-manual) information, the names of the zones specified in the {{site.data.keyword.satelliteshort}} location Zone fields must match exactly the names of the corresponding zones in your infrastructure provider, where you plan to create hosts.
4. Before you proceed to the steps in the infrastructure specific topic:

  - The {{site.data.keyword.satelliteshort}} location must be provisioned and have a Normal state.
  - The {{site.data.keyword.satelliteshort}} location control plane service must be running and have a Normal state.


## Provision Event Streams
{: #provision_es}

Follow the steps to set up [Amazon Web Services (AWS)](/docs/EventStreams?topic=EventStreams-setting-up-amazon-web-services-location).

## Limitations of the IBM Satellite plan for Event Streams
{: #satellite_restrictions}

- The following infrastruture provider is supported:
  - [Amazon Web Services (AWS)](/docs/EventStreams?topic=EventStreams-setting-up-amazon-web-services-location)

- Your {{site.data.keyword.satelliteshort}} location can be managed from the following {{site.data.keyword.cloud_notm}} data centers:

  - Dallas
  - Washington DC

- The following functions are not supported on the {{site.data.keyword.satellitelong_notm}} plan for {{site.data.keyword.messagehub}}:

  - Scale up of message retention storage
  - IAM IP address access restrictions
  - Bring Your Own Key (BYOK)
  - Schema Registry
  - Cloud Service Endpoint support
  - Stream to {{site.data.keyword.cos_full_notm}} using {{site.data.keyword.sqlquery_full}}
  - Activity tracker
  - Monitoring {{site.data.keyword.messagehub}} metrics using {{site.data.keyword.monitoringfull}}
