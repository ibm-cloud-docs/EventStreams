---

copyright:
  years: 2022
lastupdated: "2022-04-01"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka, provision, location

subcollection: EventStreams

---

{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:beta: .beta}
{:shortdesc: .shortdesc}
{:step: data-tutorial-type='step'}
{:tutorial: data-hd-content-type='tutorial'}

# Provisioning {{site.data.keyword.messagehub}} for {{site.data.keyword.satellitelong}} (Beta)
{: #satellite-provisioning}
{: toc-content-type="tutorial"}
{: toc-completion-time="15m"}
{:beta: .beta}

## Overview
{: #satellite-provision-overview}
{: beta}

Complete the steps to set up the {{site.data.keyword.satellitelong}} plan for {{site.data.keyword.messagehub_full}} in a {{site.data.keyword.satelliteshort}} location.
{: beta}

The following steps guide you through provisioning a {{site.data.keyword.satelliteshort}} location in your account, configuring service authorization, adding compute hosts to the {{site.data.keyword.satelliteshort}} location, provisioning an {{site.data.keyword.messagehub_full}} service instance, and configuring the block storage assignment, so that
{{site.data.keyword.messagehub}} can allocate block storage.

## Provision a {{site.data.keyword.satelliteshort}} location
{: #satellite-provision-location}
{: step}

1. Provision a {{site.data.keyword.satelliteshort}} location.

    1. Refer to [Setting up {{site.data.keyword.satelliteshort}} locations](/docs/satellite?topic=satellite-locations). 
    Complete the steps in [Manually creating {{site.data.keyword.satelliteshort}} locations](/docs/satellite?topic=satellite-locations#location-create-manual).
    2. {{site.data.keyword.messagehub_full}} supports {{site.data.keyword.satelliteshort}} locations that are managed by several different regions. 
    Refer to the plan comparison table in [Choosing your plan](/docs/EventStreams?topic=EventStreams-plan_choose) for the list of supported regions.
    3. As noted in the [Manually creating {{site.data.keyword.satelliteshort}} locations](/docs/satellite?topic=satellite-locations#location-create-manual) information, 
    the names of the zones specified in the {{site.data.keyword.satelliteshort}} location zone fields must exactly match the names of the corresponding zones in your 
    infrastructure provider, where you plan to create hosts.

2. Before you proceed to the next step, ensure that the following criteria is met:

   - The {{site.data.keyword.satelliteshort}} location must be provisioned and have a Normal state.
   - The {{site.data.keyword.satelliteshort}} location control plane service must be running and have a Normal state.

## Grant service authorization
{: step}
{: #satellite-service-authorization}

In order for the {{site.data.keyword.messagehub}} service to access the {{site.data.keyword.satelliteshort}} service, a service-to-service authorization must be 
created.

1. In the {{site.data.keyword.cloud}} console account where your {{site.data.keyword.satelliteshort}} location was provisioned, from the **Manage** tab, select **Access (IAM)**.
2. Choose the **Authorizations** tab from the left hand menu.
3. Click the **Create** button to create an authorization that allows a service instance access to another service instance.

   1. The source service is the service that is granted access to the target service. The roles you select define the level of access for this service. 
   The target service is the service you grant permission to be accessed by the source service, based on the assigned roles.
   2. In the **Source Service** field, select **{{site.data.keyword.messagehub}}**.
   3. Scope the access to **All resources**.
   4. In the **Target Service** field, select **{{site.data.keyword.satelliteshort}}**.
   5. Scope the access to **All resources**.
   6. Select all options:
        - **{{site.data.keyword.satelliteshort}} Cluster Creator**
        - **{{site.data.keyword.satelliteshort}} Link Administrator**
        - **{{site.data.keyword.satelliteshort}} Link Source Access Controller**
   7. Click the **Authorize** button.

## Attach additional hosts to the {{site.data.keyword.satelliteshort}} location
{: #satellite-attach-additional-hosts}
{: step}

{{site.data.keyword.messagehub}} provides high availability using multi-zone region deployment to protect against single points of failure. These additional hosts are used to create a service cluster into which {{site.data.keyword.messagehub}} gets deployed. You must provision and balance the host compute infrastructure for the zones in your {{site.data.keyword.satelliteshort}} location.

Attach the following hosts to your {{site.data.keyword.satelliteshort}} location:

- 6 nodes of 4 vCPU and 16 GiB memory
- 3 nodes of 8 vCPU and 32 GiB memory

The hosts requirement is for a single {{site.data.keyword.messagehub}} {{site.data.keyword.satelliteshort}} instance. If multiple {{site.data.keyword.messagehub}} 
{{site.data.keyword.satelliteshort}} instances are required, the hosts requirement applies to each {{site.data.keyword.messagehub}} instance.
{:note}

## Provision {{site.data.keyword.messagehub}} service instance
{: step}
{: #satellite-provision-es-instance}

After preparing your {{site.data.keyword.satelliteshort}} location, granting service authorization, and attaching additional hosts, you can provision a {{site.data.keyword.messagehub}} service instance: 

1. Navigate to the catalog, by clicking **Catalog** in the navigation bar.
2. Look for the **Event Streams** tile in the **Integration** section and select it.
3. In the **Select a location** field, select the {{site.data.keyword.satelliteshort}} location you provisioned. When your {{site.data.keyword.satelliteshort}} 
location is selected, the pricing plan information will be updated. Review the {{site.data.keyword.satelliteshort}} plan details.
4. Specify a **Service name** if something other than the default name is desired.
5. Click **Create**.

When you provision an {{site.data.keyword.messagehub}} service instance, a service cluster is automatically deployed into your {{site.data.keyword.satelliteshort}} 
location. You can verify the start of the deployment of the service cluster with the following steps:

1. From the left hand **Navigation Menu**, select **{{site.data.keyword.satelliteshort}}**, then **Locations**.
2. Select your {{site.data.keyword.satelliteshort}} location.
3. Select **Services**.
4. Verify that a service named **messagehub** is listed. If it is not yet listed, refresh the page until it is listed before moving to the next step.

While the service instance and cluster are provisioned, create the storage assignment. Proceed to the next step and complete the instructions.
{: important}

## Create the block storage configuration assignment (using {{site.data.keyword.satelliteshort}} Storage UI)
{: step}
{: #satellite-create-storage-assignment}

The following steps require that you have access to Storage UI for {{site.data.keyword.satelliteshort}}. To enable your access, you must be added to the allowlist. See [Before you begin](/docs/EventStreams?topic=EventStreams-satellite_about#satellite_before_you_begin) for details on requesting allowlist access. If you prefer to use the CLI to create the storage configuration from templates, and then assign that configuration to the {{site.data.keyword.messagehub}} messagehub service cluster, you do not need access to the Storage UI for Satellite. If you use the CLI, complete the storage configuration and assignment.
{: important}

During the {{site.data.keyword.messagehub}} service instance provision, block storage configuration is automatically queued for confirmation and assignment. This confirmation and assignment requires acknowledgement from the {{site.data.keyword.satelliteshort}} location administrator.

1. Navigate to **{{site.data.keyword.satelliteshort}}**, by clicking **{{site.data.keyword.satelliteshort}}** > **Locations** in the navigation bar.
2. Select your {{site.data.keyword.satelliteshort}} location.
3. Select the **Services** tab.
4. Look for the acknowledgement pop-up.

   1. Complete the storage configuration set up.
   2. Complete assignment of the storage configuration to the {{site.data.keyword.messagehub}} service cluster.

After the storage assignment is created, allow up to 60 minutes for the {{site.data.keyword.messagehub}} service instance to be ready for use.
