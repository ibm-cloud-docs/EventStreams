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


# Getting started with the IBM Satellite plan for Event Streams
{: #satellite_getting_started}

Use the Satellite plan to deploy an Enterprise plan into Satellite locations of your choice. Using {{site.data.keyword.satellitelong_notm}}, you can create a hybrid environment that brings the scalability and on-demand flexibility of public cloud services to the applications and data that run in your secure private cloud. 

## Provisioning a Satellite instance

Complete the following steps to deploy a Satellite instance. 

### Prerequisites

You must have the following: 
* access to an {{site.data.keyword.Bluemix}} account

* access to an on-prem or AWS account

* sufficient access to create the required resources in both accounts

## Steps overview

What are we trying to achieve?

1. Provision an {{site.data.keyword.Bluemix_notm}} Satellite location. This enables you to bring your own hosts to the {{site.data.keyword.Bluemix_notm}} and provision {{site.data.keyword.Bluemix_notm}} services onto your machines. The examples in this topic mainly discuss AWS as the host provider because for our Beta release, we have mainly focused on AWS EC2.

   For provisioning and machine selection for {{site.data.keyword.messagehub}}' requirements, see [Setting up your AWS machines](/docs/EventStreams?topic=EventStreams-aws).

   Our steps follow the **Public cloud** > **Other cloud** type provisioning flow. However, you might be able to use these steps to deploy and configure Satellite for any hosts.

   Note that block storage and ingress requirements are not currently discussed in detail. We're planning to fill this gap later.

2. We'll discuss provisioning the AWS infrastructure.

3. After adding enough machines to your Satellite location, we'll proceed to provision an {{site.data.keyword.messagehub}} for Satellite instance.

4. We'll then create a block storage assignment for {{site.data.keyword.messagehub}}' purposes from AWS into your new {{site.data.keyword.messagehub}} cluster.

5. The ongoing provisioning now automatically attaches the block storage to your {{site.data.keyword.messagehub}} cluster, the provisioning completes, and you'll be ready to use {{site.data.keyword.messagehub}}.



### Steps

1. Sign in to {{site.data.keyword.Bluemix_notm}} and target your target account.
2. Create a service-to-service binding between {{site.data.keyword.messagehub}} and Satellite in your {{site.data.keyword.Bluemix_notm}} account, if you haven't already done so. You can verify this by navigating to the following page: **{{site.data.keyword.Bluemix_notm}} dashboard** > **Manage** > **Account** > **Manage access and users** > **Access (IAM)** page > **Authorizations**.

   ```
   Role: All
   Source: Event Streams
   Target: Satellite service
   ```
   {: codeblock}

3. Complete the following steps on Satellite. For more information, see [Getting started with IBM Cloud Satellite](/docs/satellite?topic=satellite-getting-started).
   1. [Provision a Satellite location](/docs/satellite-working?topic=satellite-working-getting-started#create-location).
   Provision your location manually from the [Satellite catalog](https://cloud.ibm.com/satellite/): **Locations** > **Create location** > **Advanced Configuration** > **Public cloud** > **Other cloud** > **Manual**
   2. Set up a Satellite location control plane 
   3. [Attach hosts to your Satellite location](/docs/satellite?topic=satellite-getting-started#attach-hosts-to-location) for the {{site.data.keyword.messagehub}} cluster to use.
4. After you have provisioned your Satellite location, download the provisioning script provided by IBM Cloud Satellite. Run this script on your machines.

   If you are using AWS, you need to make some updates to the script. In your script, add the following lines *after* the line that first mentions `API_URL`:

   ```
   bash
   # Enable AWS RHEL package updates
   yum update -y
   yum-config-manager --enable '*'
   yum repolist all
   yum install container-selinux -y
   echo "repos enabled"
   ```
   {: codeblock}

   Before you can create the {{site.data.keyword.messagehub}} instance and its storage configuration for your new Satellite location, you need to complete the provisioning of the Satellite location, including the configuration and provisioning of its control plane. 

5. Get the Satellite location ID.

   ```
   ibmcloud sat location ls
     >test-sat-loc          <location ID>
   ```
   {: codeblock}

6. Create the AWS access key and secret. 

   From the AWS Management Console:
   1. Click **Security Credentials** in the top right corner. 
   2. In the main **Your Security Credentials** pane, select **Access keys (access key ID and secret access key)**. 
   3. Click **Create New Access Key** for CLI, SDK, and API access.
7. Create storage configuration for your {{site.data.keyword.messagehub}} cluster.

   ```
   ibmcloud sat storage template ls
   ibmcloud sat storage config create  \
      --name '<configuration_name>' \
      --template-name 'aws-ebs-csi-driver' \
      --template-version '0.9.14' \
      --location '<location ID>' \
      -p "aws-access-key=<my_aws_access_key_id>" \
      -p "aws-secret-access-key=<my_aws_access_key_secret>"
   ```
   {: codeblock}

8. Verify that the storage config is successfully created.

   ```
   ibmcloud sat storage config get --config <configuration_name>
   ```
   {: codeblock}

9. Provision your {{site.data.keyword.messagehub}} service instance from the [{{site.data.keyword.Bluemix_notm}} catalog](https://cloud.ibm.com/catalog/event-streams). 

10. Obtain the {{site.data.keyword.messagehub}} service cluster ID from the list of services in the Satellite location.

   ```
   ibmcloud sat service ls --location c6l3qc0d0bmg9kc8otcg
     >mh-qlxttblrkqygwjxdpxqq   c6l53nud0sadctjok6eg   eventstreams-nextgen-int 
   ```
   {: codeblock}

   _Check what should replace eventstreams-nextgen-int_
   {: note}

11. Run the command 

   ```
   ibmcloud sat service ls --location <location_id> 
   ```
   {: codeblock}

   and wait for the status of the new service to become normal. For example:

   ```
   Cluster Name              Cluster ID             Service                    Status               Created      Hosts   Needs more hosts?
   Control plane             c6ou4fiw0268us5d3d4g   satellite                  All Workers Normal   3 days ago   3       no
   mh-int-pipe-sat-rymxbpj   c6ousl0w01nmcvqp5ojg   eventstreams-nextgen-int   All Workers Normal   3 days ago   9       no
   ```

   _Check what the cluster name should be and service will probably be messagehub_
   {: note}

12. Wait until you can see the cluster in the sat loc location, then assign the storage to your {{site.data.keyword.messagehub}} service.

   ```
   ibmcloud sat storage assignment create  \
         --name "<assignment_name>"  \
         --service-cluster-id c6l53nud0sadctjok6eg  \
         --config '<configuration_name>'
```
   {: codeblock}

## Restrictions of the Satellite plan
{: #satellite_restrictions}

The following functions are not supported on the Satellite plan for {{site.data.keyword.messagehub}}.

* IAM IP address access restrictions
* Bring Your Own Key (BYOK)
* Schema Registry
* Cloud Service Endpoint support
* Stream to Cloud Object Storage using SQL Query
* Activity tracker?
* Monitoring Event Streams metrics using IBM Cloud Monitoring?
