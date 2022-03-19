---

copyright:
  years: 2022
lastupdated: "2022-03-03"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka, provision, location

subcollection: EventStreams

---

{:codeblock: .codeblock}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:shortdesc: .shortdesc}
{:step: data-tutorial-type='step'}
{:tutorial: data-hd-content-type='tutorial'}

# Provisioning {{site.data.keyword.messagehub}} for {{site.data.keyword.satellitelong}}

{: #satellite-provisioning}
{: toc-content-type="tutorial"}
{: toc-completion-time="15m"}

## Overview

{: #satellite-provision-overview}

Follow the steps below to set up the {{site.data.keyword.satellitelong}} plan for {{site.data.keyword.messagehub_full}} in a {{site.data.keyword.satelliteshort}} location.

The following steps guide you through provisioning a satellite location in your account, configure service authorization, adding compute hosts to the satellite location for {{site.data.keyword.messagehub_full}}, provision an {{site.data.keyword.messagehub_full}} service instance, and configure the block storage assignment for {{site.data.keyword.messagehub_full}}.

## Step 1: Provision a satellite location

{: #satellite-provision-location}
{: step}

1. Provision a {{site.data.keyword.satelliteshort}} location
   1. Refer to [Setting up {{site.data.keyword.satelliteshort}} locations](/docs/satellite?topic=satellite-locations). Follow the steps in [Manually creating {{site.data.keyword.satelliteshort}} locations](/docs/satellite?topic=satellite-locations#location-create-manual).
   2. {{site.data.keyword.messagehub_full}} supports satellite locations that are managed by several different regions.  Refer to the plan comparison table in [Choosing your plan](/docs/EventStreams?topic=EventStreams-plan_choose) for the list of supported regions.
   3. As noted in the [Manually creating {{site.data.keyword.satelliteshort}} locations](/docs/satellite?topic=satellite-locations#location-create-manual) information, the names of the zones specified in the {{site.data.keyword.satelliteshort}} location Zone fields must match exactly the names of the corresponding zones in your infrastructure provider, where you plan to create hosts.

2. Before you proceed to the next step:

   - The {{site.data.keyword.satelliteshort}} location must be provisioned and have a Normal state.
   - The {{site.data.keyword.satelliteshort}} location control plane service must be running and have a Normal state.

The following information regarding the amount of storage and hosts is for a single {{site.data.keyword.messagehub}} {{site.data.keyword.satelliteshort}} instance.  If multiple {{site.data.keyword.messagehub}} {{site.data.keyword.satelliteshort}} instances are required, the same amount of hosts and storage are needed for additional {{site.data.keyword.messagehub}} {{site.data.keyword.satelliteshort}} instance.
{:note: .note}

## Step 2: Grant service authorization

{: step}
{: #satellite-service-authorization}

In order for the {{site.data.keyword.messagehub}} service to access the {{site.data.keyword.satelliteshort}} service, a service to service authorization needs to be created.

1. In the {{site.data.keyword.cloud}} console account where your {{site.data.keyword.satelliteshort}} location was provisioned, from the **Manage** tab, select **Access (IAM)**.
2. Choose the **Authorizations** tab from the left hand menu.
3. Click the **Create** button to create an authorization that allows a service instance access to another service instance.

- The source service is the service that is granted access to the target service. The roles you select define the level of access for this service. The target service is the service you are granting permission to be accessed by the source service, based on the assigned roles.
- In the **Source Service** field, select **{{site.data.keyword.messagehub}}**.
- Scope the access to **All resources**.
- In the **Target Service** field, select **Satellite**.
- Select all options:
  
  - **{{site.data.keyword.satelliteshort}} Cluster Creator**
  - **{{site.data.keyword.satelliteshort}} Link Administrator**
  - **{{site.data.keyword.satelliteshort}} Link Source Access Controller**
- Click the **Authorize** button.

## Step 3: Attach additional hosts to the Satellite location

{: #satellite-attach-additional-hosts}
{: step}

{{site.data.keyword.messagehub}} provides high availability using multi-zone region deployment to protect against single points of failure.  These additional hosts are used to create a service cluster into which {{site.data.keyword.messagehub}} will be deployed. You must provision and balance the host compute infrastructure for the zones in your satellite location.

Attach the following hosts to your {{site.data.keyword.satelliteshort}} location:

- 6 nodes of 4 vCPU and 16 GiB memory
- 3 nodes of 8 vCPU and 32 GiB memory

The above hosts requirement is for a single {{site.data.keyword.messagehub}} {{site.data.keyword.satelliteshort}} instance.  If multiple {{site.data.keyword.messagehub}} {{site.data.keyword.satelliteshort}} instances are required, the hosts requirement applies to each {{site.data.keyword.messagehub}} instance.
{:note: .note}

## Step 4: Provision {{site.data.keyword.messagehub}} service instance

{: step}
{: #satellite-provision-es-instance}

After preparing your {{site.data.keyword.satelliteshort}} location and granting service authorization, you can provision a {{site.data.keyword.messagehub}} service instance:  

1. Navigate to the catalog, by clicking **Catalog** in the navigation bar.
2. Look for the Event Streams tile in the Integration section and select it.
3. In the **Select a location** field, select from the displayed list the satellite location you provisioned.
4. Specify a **Service name** if something other than the default name is desired
5. Click **Create** and you're automatically redirected to your new instance.

When you provision an {{site.data.keyword.messagehub}} service instance, a service cluster will automatically be deployed into your {{site.data.keyword.satelliteshort}} location. You can verify the start of the deployment of the service cluster:

1. From the left hand **Navigation Menu**, select **{{site.data.keyword.satelliteshort}}**, then **Locations**.
2. Select your {{site.data.keyword.satelliteshort}} location.
3. Select **Services**.
4. Verify that a service named **messagehub** is listed. If it is not yet listed, refresh the page until it is listed before moving to the next step.

While the service instance and cluster are provisioned, create the storage assignment. You do not need to wait for the service instance or cluster provision to complete to create the storage assignment. Proceed to the next step and complete the instructions.
{: .important}

## Step 5: Create the block storage configuration assignment (using Satellite Storage UI)

{: step}
{: #satellite-create-storage-assignment}

The steps below require that you have access to Storage UI for Satellite.  To enable your access, you must be added to the allowlist. [Contact IBM](https://www.ibm.com/contact/us/en/) to learn more.
{: .important}

During the {{site.data.keyword.messagehub}} service instance provision, block storage configuration will be automatically queued for confirmation and assignment.  This confirmation and assignment requires acknowledgement from the Satellite location administrator.

1. Navigate to Satellite, by clicking Satellite > Locations in the navigation bar.
2. Select your satellite location.
3. Select the Services tab.
4. Look for the acknowledgement pop-up to complete any configuration and approve the storage assignment.

After the storage assignment is created, allow up to 60 minutes for the {{site.data.keyword.messagehub}} service instance to be ready for use.
