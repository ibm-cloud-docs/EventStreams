---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-27b"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Connecting {{site.data.keyword.messagehub}} to {{site.data.keyword.cos_full_notm}} using {{site.data.keyword.containerfull_notm}} (IKS)
{: #cos_connector}

You can connect {{site.data.keyword.messagehub}} to {{site.data.keyword.cos_full}} to read data from an {{site.data.keyword.messagehub}} Kafka topic
and place the data into [{{site.data.keyword.IBM_notm}} Cloud Object Storage ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/services/cloud-object-storage?topic=cloud-object-storage-about#about){:new_window}.
{: shortdesc}

The connector allows you to archive data from the Kafka topics in {{site.data.keyword.messagehub}} to an instance of the [Cloud Object Storage service ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/services/cloud-object-storage?topic=cloud-object-storage-about#about){:new_window}. The connector consumes
batches of messages from Kafka and uploads the message data as objects to a bucket in the Cloud Object Storage service.
Complete the following steps to walk through the setup:

## Step 1. Install the pre-requisites
{: #step1_install_prereqs}
Ensure you have the following software and services set up:

* An {{site.data.keyword.messagehub}} instance - Standard or Enterprise plan
* An instance of the Cloud Object Storage service with at least one bucket
* An IKS cluster. You can provision a free one for testing purposes.
* A recent version of Kubectl (for example 1.14)
* [git ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://git-scm.com/downloads){:new_window}
* [Gradle 4.0, or later ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://gradle.org/install/){:new_window}
* Java 8 or later


## Step 2. Create your Kafka Connect configuration
{: #step2_create_config}

a. Edit the <code>connect-distributed.properties</code> file and replace <BOOTSTRAP_SERVERS> and <APIKEY> with your {{site.data.keyword.messagehub}} credentials.

b. Then run the following commands to create a secret and a ConfigMap :
```
kubectl create secret generic connect-distributed-config --from-file=connect-distributed.properties
```
{: codeblock}

<br/>

```
kubectl create configmap connect-log4j-config --from-file=connect-log4j.properties
```
{: codeblock}


## Step 3. Deploy Kafka Connect
{: #step3_deploy_kafka}

Apply the configuration in the <code>kafka-connect.yaml</code> file by running the following command:

```
kubectl apply -f ./kafka-connect.yaml
```
{: codeblock}

* To create an instance from the {{site.data.keyword.Bluemix_notm}} console, go to the {{site.data.keyword.messagehub}} entry in the [catalog ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/catalog/services/event-streams){:new_window}.

* To create an instance from the CLI on the Enterprise plan, run a command like the following:
  ```
  ibmcloud resource service-instance-create <INSTANCE_NAME> messagehub enterprise <REGION>
  ```
  {: codeblock}
  
  Because Enterprise has its own dedicated resources for each cluster, it requires more time for provisioning so a new Enterprise instance might take up to 3 hours.


* To create an instance from the CLI on the Standard plan,run a command like the following:

  ```
  ibmcloud resource service-instance-create <INSTANCE_NAME> messagehub standard <REGION>
  ```
  {: codeblock}

  Provisioning a new Standard instance is instantaneous because the underlying resources are already set up.

## Step 4. Manage connectors
{: #step4_manage_connectors}

To manage connectors, port forward to the kafkaconnect-service Service on port 8083. For example:

```
kubectl port-forward service/kafkaconnect-service 8083
```
  {: codeblock}

The Connect REST API is then available at http://localhost:8083.


* To create an API key from the {{site.data.keyword.Bluemix_notm}} console, enter the Service credentials from the instance page, and click **New Credentials**.

* To create an API key from the CLI, run this command:
  ```
  ibmcloud resource service-key-create <KEY_NAME> <ROLE_NAME> --instance-name <INSTANCE_NAME>
  ```
  {: codeblock}

## Step 5. Build the connector
{: #step5_build_connector}

  a. Clone the repository with the following command:

  ```
  git clone https://github.com/ibm-messaging/kafka-connect-ibmcos-sink
  ```

  b. Change into the <code>kafka-connect-ibmcos-sink</code> directory:

  ```
  cd kafka-connect-ibmcos-sink
  ```

  c. Build the connector using Gradle:

  ```
  $ gradle shadowJar
  ```



Run the following command:
```
ibmcloud plugin install event-streams
```
{: codeblock}

## Step 6. Configure the cos-sink json file 
{: #step6_config_json}

kafka-connect-ibmcos-sink/config/cos-sink.json


### cos-sink.json file properties

<dl>
<dt><strong>cos.api.key</strong></dt>
<dd>Required. API key used to connect to the Cloud Object Storage service instance.</dd>
<dt><strong>cos.bucket.location</strong></dt>
<dd>Required. Location of the Cloud Object Storage service bucket, for example: eu-gb.</dd>
<dt><strong>cos.bucket.name</strong></dt>
<dd>Required. Name of the Cloud Object Storage service bucket to write data into.</dd>
<dt><strong>cos.bucket.resiliency</strong></dt>
<dd>Required. Resiliency of the Cloud Object Storage bucket. Must be one of: cross-region, regional, or single-site.</dd>
<dt><strong>cos.endpoint.visibility</strong></dt>
<dd>Optional. Specify public to connect to the Cloud Object Storage service over the public internet, or private to connect from a connector running inside the IBM Cloud network, for example from an IBM Cloud Kubernetes Service cluster. The default is public.</dd>
<dt><strong>cos.object.deadline.seconds </strong></dt>
<dd>Optional. The number of seconds (as measured wall clock time for the Connect Task instance) between reading the first record from Kafka, and writing all of the records read so far into a Cloud Object Storage object. This can be useful in situations where there are long pauses between Kafka records being produced to a topic, as it ensures that any records received by this connector will always be written into object storage within the specified period of time.</dd>
<dt><strong>cos.object.interval.seconds</strong></dt>
<dd>Optional. The number of seconds (as measured by the timestamps in Kafka records) between reading the first record from Kafka, and writing all of the records read so far into a Cloud Object Storage object.</dd>
<dt><strong>cos.object.records</strong></dt>
<dd>Optional. The maximum number of Kafka records to combine into a object.
</dd>
<dt><strong>cos.service.crn</strong></dt>
<dd>Required. CRN for the Cloud Object Storage service instance.</dd>
</dl>
 



 

 

 








Note that while the configuration properties cos.object.deadline.seconds, cos.interval.seconds, and cos.object.records are all listed as optional, at least one of these properties must be set to a non-default value.


Before you can run any of the {{site.data.keyword.messagehub}} CLI commands, you must first initialize the plugin. Run the following command then select your {{site.data.keyword.messagehub}} instance:

```
ibmcloud es init
```

<br/>
For information about the {{site.data.keyword.messagehub}} CLI commands, see [CLI reference](/docs/services/EventStreams?topic=eventstreams-cli_reference#cli_reference).










