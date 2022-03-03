---

copyright:
  years: 2015, 2022
lastupdated: "2022-02-24"

content-type: tutorial
services: EventStreams
completion-time: 15m

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka, on-premises, location

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

# Setting up on-premises Web Services location with NetApp ONTAP-SAN (21.04) storage
{: beta}
{: #satellite-onprem}
{: toc-content-type="tutorial"}
{: toc-completion-time="15m"}

## Overview
{: #onprem-overview}

Complete the following steps to set up the {{site.data.keyword.satellitelong}} plan for {{site.data.keyword.messagehub}} in a {{site.data.keyword.satelliteshort}} location that is using on-premises infrastructure.
{: beta}

The following steps guide you through configuring, assigning, and provisioning block storage from your infrastructure provider. Storage capacity is the amount of block storage allocated in the {{site.data.keyword.messagehub}} service instance for retention of message data, management of message data, and for monitoring the operation of the {{site.data.keyword.messagehub}} service instance.

The following information outlines the type and amount of block storage that is allocated by {{site.data.keyword.messagehub}}.

| Usage | Amount allocated | Total |
| --- | --- | --- |
| Message data retention | 2 TB x 3 replicas/availability zones | 6 TB total |
| Message data management | 250 GB x 3 replicas/availability zones | 750 GB total |
| Service instance monitoring | 125 GB x 3 replicas/availability zones | 375 GB total |
{: caption="Table 1. NetApp ONTAP-SAN block storage" caption-side="bottom"}

## Prepare a Satellite location for the IBM Satellite plan for Event Streams
{: #prepare-satellite-location}
{: step}

Before you deploy the {{site.data.keyword.satelliteshort}} plan for {{site.data.keyword.messagehub}} service, prepare your {{site.data.keyword.satelliteshort}} location.

The following information about the amount of storage and hosts is for a single {{site.data.keyword.messagehub}} {{site.data.keyword.satelliteshort}} instance. If multiple {{site.data.keyword.messagehub}} {{site.data.keyword.satelliteshort}} instances are required, the same amount of hosts and storage are needed for additional {{site.data.keyword.messagehub}} {{site.data.keyword.satelliteshort}} instance.
{: note}

### Attach additional hosts to the Satellite location
{: #attach-additional-hosts}

These additional hosts are used to create a service cluster into which {{site.data.keyword.messagehub}} will be deployed. Attach the following hosts to your {{site.data.keyword.satelliteshort}} location:

- 6 type **4x16** hosts
- 3 type **8x32** hosts

Event Streams provides high availability via multi-zone region deployment to protect against single points of failure.  The host compute infrastructure needs to be provisioned balanced for the zones in your satellite location.
{: note}

### Create a Satellite block storage configuration
{: #satellite-blockstorage-config}

To make block storage available in a {{site.data.keyword.satelliteshort}} location, a storage configuration needs to be created. The configuration defines which {{site.data.keyword.satelliteshort}} template (or driver) to use, the version of the template, and the infrastructure provider credentials. The following example command shows how to create an NetApp ONTAP-SAN configuration for {{site.data.keyword.messagehub}}. A later step assigns this configuration to your {{site.data.keyword.satelliteshort}} service cluster of {{site.data.keyword.messagehub}}.

For NetApp ONTAP-SAN, you must create two storage configurations. One is for the trident operator and the other is for the SAN storage. Use the following command examples to create the configurations.

Refer to [NetApp ONTAP-SAN 21.04](/docs/satellite?topic=satellite-config-storage-netapp-2104) for more detail on the NetApp templates and configuration parameters used below.
{: note}

1. Your Satellite location is managed from an {{site.data.keyword.cloud_notm}} region. Use the following command to target that region. For more information, see [Satellite regions](/docs/satellite?topic=satellite-sat-regions).

   ```bash
   ibmcloud target -r <region>
   ```
   
2. Operator configuration:

   ```bash
   ibmcloud sat storage config create  \\
      --name 'netapp-trident-config-storage-es-1' \\
      --template-name 'netapp-trident' \\
      --template-version '21.04' \\
      --location '${LOCATION_ID}'
   ```
   
3. SAN configuration:

   ```bash
   ibmcloud sat storage config create  \\
     --name 'netapp-san-config-storage-es-1' \\
     --template-name 'netapp-ontap-san' \\
     --template-version '21.04' \\
     --location '${LOCATION_ID}' \\
     -p "dataLIF=${DATALIF}" \\
     -p "managementLIF=${MGMLIF}" \\
     -p "svm=${SVM}" \\
     -p "username=${USERNAME}" \\
     -p "password=${PASSWORD}" \\
     -p "limitVolumeSize=2500Gi"
   ```

## Grant a service authorization
{: step}
{: #service-authorization}

Begin by configuring IAM authorizations. For the {{site.data.keyword.messagehub}} service to access the {{site.data.keyword.satelliteshort}} service, a service-to-service authorization must to be created.

1. Log in to the {{site.data.keyword.cloud}} console account where your {{site.data.keyword.satelliteshort}} location was provisioned.
2. From the **Manage** tab, select **Access (IAM)**.
3. Choose the **Authorizations** tab from the left hand menu.
4. Click the **Create** button to create an authorization that allows a service instance access to another service instance.

- The source service is the service that is granted access to the target service. The roles you select define the level of access for this service. The target service is the service you are granting permission to be accessed by the source service, based on the assigned roles.
- In the **Source Service** field, select **{{site.data.keyword.messagehub}}**.
- Scope the access to **All resources**.
- In the **Target Service** field, select **{{site.data.keyword.satelliteshort}}**.
- Select all options:
  
  - **{{site.data.keyword.satelliteshort}} Cluster Creator**
  - **{{site.data.keyword.satelliteshort}} Link Administrator**
  - **{{site.data.keyword.satelliteshort}} Link Source Access Controller**
- Click the **Authorize** button.

## Provisioning {{site.data.keyword.messagehub}} Satellite deployment
{: step}
{: #provision-deployment}

After preparing your {{site.data.keyword.satelliteshort}} location and granting service authorization, provision your {{site.data.keyword.satellitelong_notm}} plan for {{site.data.keyword.messagehub}} {{site.data.keyword.satelliteshort}} service instance by selecting the {{site.data.keyword.satelliteshort}} location that you created in the **Location** dropdown of the provisioning page. When the provisioning starts, verify that the service instance provision has started in the {{site.data.keyword.cloud_notm}} **Resource List** by selecting **Services and software**.

When you provision {{site.data.keyword.messagehub}} service instance, a service cluster is automatically deployed into your {{site.data.keyword.satelliteshort}} location. To verify the start of the deployment of the service cluster by using the following steps:

1. From the left hand **Navigation Menu**, select **{{site.data.keyword.satelliteshort}}**, then **Locations**.
2. Select your {{site.data.keyword.satelliteshort}} location.
3. Select **Services**.
4. Verify that a service named **messagehub** is listed. If it is not yet listed, refresh the page until it is listed before moving to the next step. Make note of the **Cluster name** of the **messagehub** service.

While the service instance and cluster are provisioned, create the storage assignment. You do not need to wait for the service instance or cluster provision to complete to create the storage assignment. Proceed to the next step and complete the instructions.
{: important}

## Create a storage assignment
{: step}
{: #create-storage-assignment-onprem}

When the {{site.data.keyword.messagehub}} service cluster is available in your {{site.data.keyword.satelliteshort}} location, the next step is to create a {{site.data.keyword.satelliteshort}} storage assignment. This allows the service cluster to create volumes on the previously configured storage.

First, use the {{site.data.keyword.cloud_notm}} CLI to obtain the list of services in your {{site.data.keyword.satelliteshort}} location:

```bash
ibmcloud sat service ls --location <sat location name/location id>
```

A list of services are displayed. Identify the **messagehub** service that has a **Cluster Name** matching the service listed in the {{site.data.keyword.cloud_notm}} console in the previous step. Save the **Cluster ID** value for that service.

Use the **Cluster ID** as an input parameter value for `--service-cluster-id` in the following {{site.data.keyword.satelliteshort}} storage assignment command:

1. Operator storage assignment:

   ```bash
   ibmcloud sat storage assignment create  \\
      --name "netapp-trident-es-assignment"  \\
      --service-cluster-id <Cluster-ID>  \\
      --config 'netapp-trident-config-storage-es-1'
   ```
   
2. SAN storage assignment:

   ```bash
   ibmcloud sat storage assignment create  \\
      --name "netapp-san-es-assignment"  \\
      --service-cluster-id <Cluster-ID>  \\
      --config 'netapp-san-config-storage-es-1'
   ```

After the storage assignment is created, allow up to 60 minutes for the {{site.data.keyword.messagehub}} service instance to be ready for use.
