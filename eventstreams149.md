---

copyright:
  years: 2015, 2019
lastupdated: "2019-07-23"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Connecting {{site.data.keyword.messagehub}} to Cloud Object Storage using IKS
{: #cos_connector}

The following steps detail how to get the Kafka Connect runtime running in an IKS cluster and start the COS Sink Connector to archive data from Kafka topics in Event Streams to an instance of the Cloud Object Storage service. The connector consumes batches of messages from Kafka and uploads the message data as objects to a bucket in the Cloud Object Storage service. Complete the following steps to walk through the setup:

You can connect {{site.data.keyword.messagehub}} to {{site.data.keyword.cos_full}} to read data from an {{site.data.keyword.messagehub}} Kafka topic
and place the data into [{{site.data.keyword.IBM_notm}} Cloud Object Storage ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/services/cloud-object-storage?topic=cloud-object-storage-about#about){:new_window}.
{: shortdesc}

The connector allows you to archive data from the Kafka topics in {{site.data.keyword.messagehub}} to an instance of the [Cloud Object Storage service ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/services/cloud-object-storage?topic=cloud-object-storage-about#about){:new_window}. The connector consumes
batches of messages from Kafka and uploads the message data as objects to a bucket in the Cloud Object Storage service.
Complete the following steps to walk through the setup:

## Step 1. Install the pre-requisites
{: #step1_install_prereqs}
Ensure you have the following software and services installed:

* An {{site.data.keyword.messagehub}} instance - Standard or Enterprise plan. You will need to create credentials.
* An instance of the Cloud Object Storage service with at least one bucket
* An {{site.data.keyword.containerfull}} cluster. You can provision a free one for testing purposes. 

    You will also need CLI access to your cluster. For more information, see
 [Setting up the CLI and API](/docs/containers?topic=containers-cs_cli_install)
* A recent version of Kubectl (for example 1.14)
* [git ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://git-scm.com/downloads){:new_window}
* [Gradle 4.0, or later ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://gradle.org/install/){:new_window}
* Java 8 or later

## Step 2. Clone the kafka-connect repositories
{: #step3_clone project}

Clone the following two repositories that contain the required files:

* https://github.com/ibm-messaging/kafka-connect-ibmcos-sink

* https://github.com/ibm-messaging/event-streams-samples


## Step 3. Create your Kafka Connect configuration
{: #step3_create_config}

1. You only have to set up this configuration once. {{site.data.keyword.messagehub}} stores it for future use.

    From the event-streams-samples project, navigate to the kafka-connect/IKS directory, edit the <code>connect-distributed.properties</code> file and replace &lt;BOOTSTRAP_SERVERS&gt; in one place and &lt;APIKEY&gt; in three places with your {{site.data.keyword.messagehub}} credentials.

    Provide &lt;BOOTSTRAP_SERVERS&gt; as a comma-separated list. If they are not valid, you will get an error.

    Your &lt;APIKEY&gt; will appear in clear text on your machine but will be secret when pushed to IKS.

    Kafka Connect can run multiple workers for reliability and scalability reasons. If your IKS cluster has more than 1 node and you want multiple Connect workers, edit the <code>kafka-connect.yaml</code> file and edit the entry <code>replicas: 1</code>.

2. Then run the following commands:
<br/>
    To create a secret: 
    ```
    kubectl create secret generic connect-distributed-config --from-file=connect-distributed.properties
   ```
    {: codeblock}
    <br/>
    To create a ConfigMap:
    ```
    kubectl create configmap connect-log4j-config --from-file=connect-log4j.properties
    ```
    {: codeblock}


## Step 4. Deploy Kafka Connect
{: #step4_deploy_kafka}

Apply the configuration in the <code>kafka-connect.yaml</code> file by running the following command:

```
kubectl apply -f ./kafka-connect.yaml
```
{: codeblock}


## Step 5. Manage connectors
{: #step5_manage_connectors}

To manage connectors, port forward to the kafkaconnect-service Service on port 8083. For example:

```
kubectl port-forward service/kafkaconnect-service 8083
```
  {: codeblock}

Keep the terminal used for port forwarding open, and use another terminal for the following steps.

The Connect REST API is then available at http://localhost:8083.

So you now have the Kafka Connect runtime deployed and running in IKS. Next, let's start the COS connector!

For more information about the API, see
[Kafka Connect REST Interface ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://kafka.apache.org/documentation/#connect_rest){:new_window}

<!--
## Step 6. Build the connector
{: #step6_build_connector}

1. Clone the repository with the following command:

    ```
    git clone https://github.com/ibm-messaging/kafka-connect-ibmcos-sink
    ```

2. Change into the <code>kafka-connect-ibmcos-sink</code> directory:

    ```
    cd kafka-connect-ibmcos-sink
    ```

3. Build the connector using Gradle:

    ```
    $ gradle shadowJar
    ```
-->

## Step 6. Configure the cos-sink json and cos-sink.properties files
{: #step6_config_json}

Edit the <code>cos-sink.json</code> and cos-sink.properties files located in <code>kafka-connect-ibmcos-sink/config/</code> so that at a minimum your required properties are completed with your information. Although the configuration properties cos.object.deadline.seconds, cos.interval.seconds, and cos.object.records are listed as optional, you must set at least one of these properties to a non-default value.

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
<dd>Required. CRN for the Cloud Object Storage service instance.
<p>Ensure you enter the correct CRN:it is the resource instance ID ending with double colons. For example, 
<code>crn:v1:staging:public:cloud-object-storage:global:a/8c226dc8c8bfb9bc3431515a16957954:b25fe12c-9cf5-4ee8-8285-2c7e6ae707f6::</code></dd>
</dl>
 
### Get COS credentials using the IBM Cloud console
{: #connect_enterprise_external_console}

1. Locate your Cloud Object Storage service on the dashboard.
2. Click your service tile.
3. Click **Service Credentials**.
4. Click **New Credential**. 
5. Complete the details for your new credential like a name and role and click **Add**. A new credential appears in the credentials list.
6. Click this credential using **View Credentials** to reveal the details in JSON format.


## Step nn Start the connector with its configuration

```
curl -X POST -H "Content-Type: application/json" http://localhost:8083/connectors
--data "@./cos-sink.json"
```
  {: codeblock}

## Step 7. Monitoring your connectors 
{: #step7_monitor_connectors}

You can check your connector by going to
http://localhost:8083/connectors/cos-sink/status

If the state of the connector is not running, you will need to restart it.

