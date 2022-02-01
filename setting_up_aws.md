---

copyright:
  year: 2022
lastupdated: "2022-01-31"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka, AWS, Satellite, location

subcollection: EventStreams

---

{:codeblock: .codeblock}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:beta: .beta}
{:shortdesc: .shortdesc}
{:step: data-tutorial-type='step'}
{:tutorial: data-hd-content-type='tutorial'}

# Setting up Amazon Web Services location
{: beta}

{: #satellite-aws}
{: toc-content-type="tutorial"}
{: toc-completion-time="15m"}

## Overview

Follow the steps below to set up the {{site.data.keyword.satellitelong}} plan for {{site.data.keyword.messagehub_full}} in a {{site.data.keyword.satelliteshort}} location that is using Amazon Web Services (AWS) infrastructure.
{: beta}

The following steps guide you through configuring, assigning, and provisioning block storage from your infrastructure provider. Storage capacity is the amount of block storage allocated in the {{site.data.keyword.messagehub}} service instance for retention of message data, management of message data, and for monitoring the operation of the {{site.data.keyword.messagehub}} service instance.

The following information outlines the type and amount of block storage that will be allocated by {{site.data.keyword.messagehub}}.

| Usage | Amount allocated | Total |
| --- | --- | --- |
| Message data retention | 2 TB x 3 replicas/availability zones | 6 TB total |
| Message data management | 250 GB x 3 replicas/availability zones | 750 GB total |
| Service instance monitoring | 125 GB x 3 replicas/availability zones | 375 GB total |
{: caption="Table 1. AWS Elastic Block Storage (EBS)" caption-side="bottom"}

## Step 1: Prepare a Satellite location for the IBM Satellite plan for Event Streams

{: #prepare-satellite-location}
{: step}

Before you deploy the {{site.data.keyword.satellitelong}} plan for {{site.data.keyword.messagehub_full}} service, prepare your {{site.data.keyword.satelliteshort}} location.

The following information regarding the amount of storage and hosts is for a single {{site.data.keyword.messagehub}} {{site.data.keyword.satelliteshort}} instance.  If multiple {{site.data.keyword.messagehub}} {{site.data.keyword.satelliteshort}} instances are required, the same amount of hosts and storage are needed for additional {{site.data.keyword.messagehub}} {{site.data.keyword.satelliteshort}} instance.
{:note: .note}

### Attach additional hosts to the Satellite location

{: #attach-additional-hosts}

These additional hosts are used to create a service cluster into which {{site.data.keyword.messagehub}} will be deployed. Attach the following hosts to your {{site.data.keyword.satelliteshort}} location:

- 6 type **4x16** hosts
  - On AWS, choose 6 hosts of type **AWS m5d.xlarge**.
- 3 type **32x128** hosts
  - On AWS, choose 3 hosts of type **AWS m5d.2xlarge**.

Refer to [Adding AWS hosts to Satellite](https://cloud.ibm.com/docs/satellite?topic=satellite-aws#aws-host-attach) for more detail on adding AWS hosts to your satellite location.
{: note}

### Create a Satellite block storage configuration

{: #satellite-blockstorage-config}

To make block storage available in a {{site.data.keyword.satelliteshort}} location, a storage configuration needs to be created. The configuration defines which {{site.data.keyword.satelliteshort}} template (or driver) to use, the version of the template, and the infrastructure provider credentials. The following example command shows how to create an AWS configuration for {{site.data.keyword.messagehub}}. A later step will assign this configuration to your {{site.data.keyword.satelliteshort}} service cluster of {{site.data.keyword.messagehub}}.

Refer to [Amazon Elastic Block Storage (EBS)](/docs/satellite?topic=satellite-config-storage-ebs) for more detail on block storage configurations.
{: note}

```bash
ibmcloud sat storage config create  \\
  --name 'aws-ebs-config-storage-es-1' \\
  --template-name 'aws-ebs-csi-driver' \\
  --template-version '0.9.14' \\
  --location '${LOCATION_ID}' \\
  -p "aws-access-key=${AWS_ACCESS_KEY_ID}" \\
  -p "aws-secret-access-key=${AWS_ACCESS_KEY}"
```

{:codeblock: .codeblock}
{: pre}

## Step 2: Grant a service authorization

{: step}
{: #service-authorization}

Begin by configuring IAM Authorizations. In order for the {{site.data.keyword.messagehub}} service to access the {{site.data.keyword.satelliteshort}} service, a service to service authorization needs to be created.

1. Log in to the {{site.data.keyword.cloud}} console account where your {{site.data.keyword.satelliteshort}} location was provisioned.
2. From the **Manage** tab, select **Access (IAM)**.
3. Choose the **Authorizations** tab from the left hand menu.
4. Click the **Create** button to create an authorization that allows a service instance access to another service instance.

- The source service is the service that is granted access to the target service. The roles you select define the level of access for this service. The target service is the service you are granting permission to be accessed by the source service, based on the assigned roles.
- In the **Source Service** field, select **{{site.data.keyword.messagehub}}**.
- Scope the access to **All resources**.
- In the **Target Service** field, select **Satellite**.
- Select all options:
  
  - **{{site.data.keyword.satelliteshort}} Cluster Creator**
  - **{{site.data.keyword.satelliteshort}} Link Administrator**
  - **{{site.data.keyword.satelliteshort}} Link Source Access Controller**
- Click the **Authorize** button.

## Step 3: Provisioning Event Streams Satellite deployment

{: step}
{: #provision-deployment}

Once you prepared your {{site.data.keyword.satelliteshort}} location and granted service authorization, you can provision your {{site.data.keyword.satellitelong_notm}} plan for {{site.data.keyword.messagehub}} {{site.data.keyword.satelliteshort}} service instance by selecting the {{site.data.keyword.satelliteshort}} location that you created in the **Location** dropdown of the provisioning page. When the provisioning starts, you can verify that the service instance provision has started in the {{site.data.keyword.cloud_notm}} **Resource List** by selecting **Services and software**.

When you provision {{site.data.keyword.messagehub}} service instance, a service cluster will automatically be deployed into your {{site.data.keyword.satelliteshort}} location. You can verify the start of the deployment of the service cluster by using the following steps:

1. From the left hand **Navigation Menu**, select **{{site.data.keyword.satelliteshort}}**, then **Locations**.
2. Select your {{site.data.keyword.satelliteshort}} location.
3. Select **Services**.
4. Verify that a service named **messagehub** is listed. If it is not yet listed, refresh the page until it is listed before moving to the next step. Make note of the **Cluster name** of the **messagehub** service.

While the service instance and cluster are provisioned, create the storage assignment. You do not need to wait for the service instance or cluster provision to complete to create the storage assignment. Proceed to the next step and complete the instructions.
{: .important}

## Step 4: Create a storage assignment

{: step}
{: #create-storage-assignment-aws}

When the {{site.data.keyword.messagehub}} service cluster is available in your {{site.data.keyword.satelliteshort}} location, the next step is to create a {{site.data.keyword.satelliteshort}} storage assignment. This will allow the service cluster to create volumes on the previously configured storage.

First, use the {{site.data.keyword.cloud_notm}} CLI to obtain the list of services in your {{site.data.keyword.satelliteshort}} location:

```bash
ibmcloud sat service ls --location <sat location name/location id>
```

A list of services are displayed. Identify the **messagehub** service that has a **Cluster Name** matching the service listed in the {{site.data.keyword.cloud_notm}} console in the previous step. Save the **Cluster ID** value for that service.

Use the **Cluster ID** as an input parameter value for `--service-cluster-id` in the following {{site.data.keyword.satelliteshort}} storage assignment command:

```bash
ibmcloud sat storage assignment create  \\
    --name "aws-ebs-es-assignment"  \\
    --service-cluster-id <Cluster-ID>  \\
    --config 'aws-ebs-config-storage-es-1'
```

After the storage assignment is created, allow up to 60 minutes for the {{site.data.keyword.messagehub}} service instance to be ready for use.
