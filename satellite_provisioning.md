---

copyright:
  years: 2022
lastupdated: "2022-05-05"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka, provision, location

subcollection: EventStreams

content-type: tutorial
services: messagehub
account-plan:
completion-time: 15m

---

{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:shortdesc: .shortdesc}
{:step: data-tutorial-type='step'}

# Provisioning {{site.data.keyword.messagehub}} for {{site.data.keyword.satelliteshort}}
{: #satellite-provisioning}
{: toc-content-type="tutorial"}
{: toc-services="messagehub"}
{: toc-completion-time="15m"}

## Overview
{: #satellite-provision-overview}

Complete the steps to set up the {{site.data.keyword.satellitelong}} plan for {{site.data.keyword.messagehub_full}} in a {{site.data.keyword.satelliteshort}} location.

The following steps guide you through provisioning a {{site.data.keyword.satelliteshort}} location in your account, configuring service authorization, adding compute hosts to the {{site.data.keyword.satelliteshort}} location, provisioning an {{site.data.keyword.messagehub_full}} service instance, and configuring the block storage assignment, so that
{{site.data.keyword.messagehub}} can allocate block storage.

## Provision a {{site.data.keyword.satelliteshort}} location
{: #satellite-provision-location}
{: step}

1. Provision a {{site.data.keyword.satelliteshort}} location.

    1. Refer to [Setting up {{site.data.keyword.satelliteshort}} locations](/docs/satellite?topic=satellite-locations). Complete the steps in [Manually creating {{site.data.keyword.satelliteshort}} locations](/docs/satellite?topic=satellite-locations#location-create-manual).

       IBM Cloud {{site.data.keyword.satelliteshort}} provides Quick Start templates to help with the provisioning of a {{site.data.keyword.satelliteshort}} location and initial set of host instances. The templates however only provision one type (size) of host instance. {{site.data.keyword.messagehub}} requires more than one type of host instance. The recommendation to use the manual steps to create your {{site.data.keyword.satelliteshort}} location allows you to provide multiple types of host instances. Optionally, use the quick start template to create hosts for the {{site.data.keyword.satelliteshort}} location's control plane and part of the {{site.data.keyword.messagehub}} requirement, then use the manual steps to add additional host types required by {{site.data.keyword.messagehub}}.
       {: important}

    2. {{site.data.keyword.messagehub_full}} supports {{site.data.keyword.satelliteshort}} locations that are managed by several different regions. Refer to the plan comparison table in [Choosing your plan](/docs/EventStreams?topic=EventStreams-plan_choose) for the list of supported regions.
    3. As noted in the [Manually creating {{site.data.keyword.satelliteshort}} locations](/docs/satellite?topic=satellite-locations#location-create-manual) information, the names of the zones specified in the {{site.data.keyword.satelliteshort}} location zone fields must exactly match the names of the corresponding zones in your infrastructure provider, where you plan to create hosts.

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

   1. The source service is the service that is granted access to the target service. The roles you select define the level of access for this service. The target service is the service you grant permission to be accessed by the source service, based on the assigned roles.
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

When {{site.data.keyword.messagehub}} provisions, the provision process discovers the 4 vCPU and 8 vCPU hosts in the {{site.data.keyword.satelliteshort}} location and automatically assign them to the {{site.data.keyword.messagehub}} service instance. If 4 vCPU and 8 vCPU hosts are not available in the {{site.data.keyword.satelliteshort}} location, the {{site.data.keyword.messagehub}} provision runs until the hosts are attached to the {{site.data.keyword.satelliteshort}} location. The {{site.data.keyword.messagehub}} provision does not use other types of hosts in replacmement of what is indicated above.
{: important}

The hosts requirement is for a single {{site.data.keyword.messagehub}} {{site.data.keyword.satelliteshort}} instance. If multiple {{site.data.keyword.messagehub}} 
{{site.data.keyword.satelliteshort}} instances are required, the hosts requirement applies to each {{site.data.keyword.messagehub}} instance.
{: note}

## Provision {{site.data.keyword.messagehub}} service instance
{: #satellite-provision-es-instance}
{: step}

After preparing your {{site.data.keyword.satelliteshort}} location, granting service authorization, and attaching additional hosts, you can provision a {{site.data.keyword.messagehub}} service instance: 

1. Navigate to the catalog, by clicking **Catalog** in the navigation bar.
2. Look for the **Event Streams** tile in the **Integration** section and select it.
3. In the **Select a location** field, select the {{site.data.keyword.satelliteshort}} location you provisioned. When your {{site.data.keyword.satelliteshort}} location is selected, the pricing plan information will be updated. Review the {{site.data.keyword.satelliteshort}} plan details.
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
{: #satellite-create-storage-assignment}
{: step}

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


## (Optional) Enable Schema Registry API
{: #satellite-enable-schema-registry}
{: step}

The Schema Registry API is not automatically enabled when you provision an {{site.data.keyword.messagehub}} Satellite instance. 
You must provide an {{site.data.keyword.cos_full_notm}} bucket for Schema Registry as its backend storage to enable this API. You are responsible for managing this bucket, including but not limited to: data encryption, data backup, and disaster recovery.

1. Create an Cloud Object Storage instance either on {{site.data.keyword.Bluemix}} or on a Satellite location.
    The COS instance on Cloud can be in the same account or in a different account as the {{site.data.keyword.messagehub}} Satellite instance.
    The COS instance on Satellite must be in the same account and in the same location as the {{site.data.keyword.messagehub}} Satellite instance.

2. Create a bucket in the COS instance.
    If the COS instance is on {{site.data.keyword.Bluemix}}, ensure the bucket is in the same region as the {{site.data.keyword.messagehub}} Satellite instance's control region.
    If the COS instance is on Satellite, ensure the COS instance's location is the same as the {{site.data.keyword.messagehub}} Satellite instance's location.
    To obtain {{site.data.keyword.messagehub}} Satellite instance's control region or location, check its CRN. For example: 

    ```text
    crn:v1:bluemix:public:messagehub:satloc_dal_c9ntbe5f0gmsm06ofoq0:a/b5b95705e299425cb5c3c82e54d4533b:6b6e769a-f3c8-4e36-aa59-0736cdc036af::
    ```
    {: codeblock}

    `satloc_dal_c9ntbe5f0gmsm06ofoq0` is the scope, in which `dal` is the control region's short name and stands for the us-south region, `c9ntbe5f0gmsm06ofoq0` is the location ID.

3. Create an authorization policy between the {{site.data.keyword.messagehub}} Satellite instance and the COS bucket.
    The source is the {{site.data.keyword.messagehub}} Satellite instance, the target is the COS bucket, and the role is Writer.
    If the COS on Cloud instance is in a different account, ensure that the authorization policy is created in the COS instance's account and the {{site.data.keyword.messagehub}} instance's account is set as the source account.

    If the {{site.data.keyword.messagehub}} Satellite instance has not been provisioned, use the following command to provision the instance with the additional parameter.

    ```sh
    ibmcloud resource service-instance-create <instance-name> messagehub Satellite <location-id> -p '{"cos_bucket_crn":"<cos-bucket-crn>"}'
    ```
    {: codeblock}

    If the {{site.data.keyword.messagehub}} Satellite instance has been provisioned, use the following command to update the instance with the -p parameter.

    ```sh
    ibmcloud resource service-instance-update <instance-name> -p '{"cos_bucket_crn":"<cos-bucket-crn>"}'
    ```
    {: codeblock}
