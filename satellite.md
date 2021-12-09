---

copyright:
  years: 2015, 2021
lastupdated: "2021-12-09"

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

* access to an AWS account

* sufficient access to create resources in both accounts

### Steps

1. Sign in to {{site.data.keyword.Bluemix_notm}} and target your target account.
2. Create a service-to-service binding between {{site.data.keyword.messagehub}} and Satellite in your {{site.data.keyword.Bluemix_notm}} account. 

   ```
   Role: All
   Source: Event Streams
   Target: Satellite service
   ```
   {: codeblock}

3. Complete the following steps on Satellite. For more information, see [Getting started with IBM Cloud Satellite](/docs/satellite?topic=satellite-getting-started).
    1. [Provision a Satellite location](/docs/satellite-working?topic=satellite-working-getting-started#create-location).
    2. Set up a Satellite location control plane 
    3. [Attach hosts to your Satellite location](/docs/satellite?topic=satellite-getting-started#attach-hosts-to-location) for the {{site.data.keyword.messagehub}} cluster to use.
    
4. Get the Satellite location ID.

   ```
   ibmcloud sat location ls
     >test-sat-loc          <location ID>
   ```
   {: codeblock}

5. Create the AWS access key and secret. 

   From the AWS Management Console, 
   1. Click **Security Credentials** in the top right corner. 
   2. In the main **Your Security Credentials** pane, select **Access keys (access key ID and secret access key)**. 
   3. Click **Create New Access Key** for CLI, SDK, and API access.
6. Create storage configuration for your {{site.data.keyword.messagehub}} cluster.

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

7. Verify that the storage config is successfully created.

   ```
   ibmcloud sat storage config get --config <configuration_name>
   ```
   {: codeblock}

8. Provision your {{site.data.keyword.messagehub}} service instance from the [{{site.data.keyword.Bluemix_notm}} catalog](https://cloud.ibm.com/catalog/event-streams). 

9. Obtain the {{site.data.keyword.messagehub}} service cluster ID from the list of services in the Satellite location.

   ```
   ibmcloud sat service ls --location c6l3qc0d0bmg9kc8otcg
     >mh-qlxttblrkqygwjxdpxqq   c6l53nud0sadctjok6eg   eventstreams-nextgen-int 
   ```
   {: codeblock}

10. Assign the storage to your {{site.data.keyword.messagehub}} service.

   ```
   ibmcloud sat storage assignment create  \
         --name "<assignment_name>"  \
         --service-cluster-id c6l53nud0sadctjok6eg  \
         --config '<configuration_name>'
```
   {: codeblock}

## Restrictions of the Satellite plan
{: #satellite_restrictions}

The following functions are not supported on the Satellite plan for {{site.data.keyword.messagehub}.

* IAM IP address access restrictions
* Encryption
* Schema Registry
* Cloud Service Endpoint support
* Stream to Cloud Object Storage using SQL Query
* Activity tracker?
* Monitoring Event Streams metrics using IBM Cloud Monitoring?
