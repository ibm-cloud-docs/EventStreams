---

copyright:
  year: 2022
lastupdated: "2022-01-26"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka, AWS, Satellite, location

subcollection: EventStreams

---

{:codeblock: .codeblock}
{:screen: .screen}
{:download: .download}
{:external: target="_blank" .external}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:beta: .beta}
{:shortdesc: .shortdesc}
{:support: data-reuse='support'}
{:step: data-tutorial-type='step'}
{:tutorial: data-hd-content-type='tutorial'}

# Setting up Amazon Web Services Location

{: #satellite-aws}
{: toc-content-type="tutorial"}
{: toc-completion-time="15m"}

## Overview

Follow the steps below to set up the IBM Satellite plan for Event Streams in a Satellite location that is using Amazon Web Services (AWS) infrastructure.

The following steps guide you through configuring, assigning, and provisioning block storage from your infrastructure provider. Storage capacity is the amount of block storage allocated in the Event Streams service instance for retention of message data, management of message data, and for monitoring the operation of the Event Streams service instance.

The following information outlines the type and amount of block storage that will be allocated by Event Streams.

AWS Elastic Block Storage (EBS)

- message data retention 2 TB x three replicas/availability zones = 6 TB total
- message data management 250 GB x three replicas/availability zones = 750 GB total
- service instance monitoring 125 GB x three replicas/availability zones = 375 GB total
- storage class: sat-aws-block-bronze

## Step 1: Prepare a Satellite location for the IBM Satellite plan for Event Streams

{: #prepare-satellite-location}
{: step}

Before you deploy the Event Streams enabled by IBM Cloud Satellite service, prepare your Satellite location.

### Attach additional hosts to the Satellite location

{: #attach-additional-hosts}

These additional hosts are used to create a service cluster into which Event Streams will be deployed. Attach the following hosts to your Satellite location:

- six type **4x16** hosts
  - on AWS, choose six hosts of type **AWS m5d.xlarge**
- three type **32x128** hosts
  - on AWS choose three hosts of type **AWS m5d.2xlarge**

### Create a Satellite block storage configuration

{: #satellite-blockstorage-config}

To make block storage available in a Satellite location, a storage configuration needs to be created. The configuration defines which Satellite template/driver to use, the version of the template, and the infrastructure provider credentials. The following example command shows how to create an AWS configuration for Event Streams. A later step will assign this configuration to your Satellite instance of Event Streams.

Refer to [Amazon Elastic Block Storage (EBS)](/docs/satellite?topic=satellite-config-storage-ebs) for more detail on block storage configurations.
{: note}

Example command:

```bash
ibmcloud sat storage config create  \\
  --name 'aws-ebs-config-storage-es-1' \\
  --template-name 'aws-ebs-csi-driver' \\
  --template-version '0.9.14' \\
  --location '${LOCATION_ID}' \\
  -p "aws-access-key=${AWS_ACCESS_KEY_ID}" \\
  -p "aws-secret-access-key=${AWS_ACCESS_KEY}"
```

{: pre}

## Step 2: Grant a service authorization

{: step}
{: #service-authorization}

Begin by configuring IAM Authorizations. In order for the Event Streams service to access the Satellite service, a service to service authorization needs to be created.

- Log in to the IBM Cloud console account where your Satellite location was provisioned.
- From the **Manage** tab, select **Access (IAM)**.
- Choose the **Authorizations** tab from the left hand menu.
- Click the **Create** button to create an authorization that allows a service instance access to another service instance.
  - The source service is the service that is granted access to the target service. The roles you select define the level of access for this service. The target service is the service you are granting permission to be accessed by the source service, based on the assigned roles.
  - In the **Source Service** field, select **Event Streams**.
  
    - Scope the access to **All resources**.
  - In the **Target Service** field, select **Satellite**.
  - Select all options:
  
    - **Satellite Cluster Creator**
    - **Satellite Link Administrator**
    - **Satellite Link Source Access Controller**
- Click the **Authorize** button.

## Step 3: Provisioning Event Streams Satellite Deployment

{: step}
{: #provision-deployment}

Once you prepared your Satellite location and granted service authorization, you can provision your IBM Satellite plan for Event Streams Satellite service instance by selecting the Satellite location that you created in the **Location** dropdown of the provisioning page. When the provisioning starts, you can verify that the service instance provision has started in the IBM Cloud **Resource List** by selecting **Services and software**.

When you provision Event Streams service instance, a service cluster will automatically be deployed into your Satellite location. The deployment of the service cluster can take up to one hour, and can be verified using these steps:

1. From the left hand **Navigation Menu**, select **Satellite**, then **Locations**.
2. Select your Satellite location.
3. Select **Services**.
4. Verify that a service named **messagehub** is listed. If it is not yet listed, refresh the page until it is listed before moving to the next step. Make note of the **Cluster name** of the **messagehub** service.

While the service instance and cluster are provisioned, create the storage assignment. You do not need to wait for the service instance/cluster provision to complete to create the storage assignment. Proceed to the next step and complete the instructions.
{: .important}

## Step 4: Create a Storage Assignment

{: step}
{: #create-storage-assignment-aws}

When the Event Streams service cluster is available in your Satellite location, the next step is to create a Satellite storage assignment. This will allow the service cluster to create volumes on the previously configured storage.

First, use the IBM Cloud CLI to obtain the list of services in your Satellite location:

```bash
ibmcloud sat service ls --location <sat location name/location id>
```

A list of services are displayed. Identify the **messagehub** service that has a **Cluster Name** matching the service listed in the IBM Cloud console in the previous step. Save the **Cluster ID** value for that service.

{: pre}

  Use the **Cluster ID** as an input parameter value for `--service-cluster-id` in the following Satellite storage assignment command:

```bash
ibmcloud sat storage assignment create  \\
    --name "aws-ebs-es-assignment"  \\
    --service-cluster-id <Cluster-ID>  \\
    --config 'aws-ebs-config-storage-es-1'
```

{: pre}

After the storage assignment is created, allow up to 60 minutes for the Event Streams service instance to be ready for use.
