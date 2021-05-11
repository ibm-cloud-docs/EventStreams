---

copyright:
  years: 2015, 2021
lastupdated: "2021-02-12"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: EventStreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Connecting {{site.data.keyword.messagehub}} to Cloud Object Storage using the Kubernetes Service
{: #cos_connector}

The following task walks you through:
* getting the Kafka Connect runtime running in an IKS cluster 
* starting the COS Sink Connector to archive data from Kafka topics in {{site.data.keyword.messagehub}} to an instance of the {{site.data.keyword.cos_full}} service. 

The Connector consumes batches of messages from Kafka and uploads the message data as objects to a bucket in the Cloud Object Storage service. 

Complete the following steps to get set up:
{: shortdesc}

## Step 1. Install the prerequisites
{: #step1_install_prereqs}
Ensure you have the following software and services installed:

* An {{site.data.keyword.messagehub}} instance - Standard or Enterprise plan. You will need to create credentials.
* An instance of the Cloud Object Storage service with at least one bucket.
* An {{site.data.keyword.containerfull}} cluster. You can provision a free one for testing purposes. 

    You will also need CLI access to your cluster. For more information, see
 [Setting up the CLI and API](/docs/containers?topic=containers-cs_cli_install).
* A recent version of Kubectl.
* [git ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://git-scm.com/downloads){:new_window}

## Step 2. Clone the kafka-connect repositories
{: #step2_clone project}

Clone the following two repositories that contain the required files:

* https://github.com/ibm-messaging/kafka-connect-ibmcos-sink
* https://github.com/ibm-messaging/event-streams-samples


## Step 3. Create your Kafka Connect configuration
{: #step3_create_config}

1. You only have to set up this configuration once. {{site.data.keyword.messagehub}} stores it for future use.

    From the event-streams-samples project, navigate to the <code>kafka-connect/IKS directory</code>, edit the <code>connect-distributed.properties</code> file and replace &lt;BOOTSTRAP_SERVERS&gt; in one place and &lt;APIKEY&gt; in three places with your {{site.data.keyword.messagehub}} credentials.

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


## Step 5. Validate Kafka Connect is running
{: #step5_validate_connector}

To validate that Kafka Connect is running, port forward to the kafkaconnect-service Service on port 8083. For example:

```
kubectl port-forward service/kafkaconnect-service 8083
```
{: codeblock}

Keep the terminal that you've used for port forwarding open, and use another terminal for the next steps.

The Connect REST API is then available at http://localhost:8083. If you want more information about the API, see
[Kafka Connect REST Interface ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://kafka.apache.org/documentation/#connect_rest){:new_window}.

So, you now have the Kafka Connect runtime deployed and running in IKS. Next, let's configure and start the COS connector.


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

## Step 6. Configure the cos-sink json file
{: #step6_config_json}

Edit the <code>cos-sink.json</code> file located in <code>kafka-connect-ibmcos-sink/config/</code> so that at a minimum your required properties are completed with your information. Although the configuration properties cos.object.deadline.seconds, cos.interval.seconds, and cos.object.records are listed as optional, you must set at least one of these properties to a non-default value.

### cos-sink.json file properties

Replace the placeholders in the <code>cos-sink.json</code> file with your own values.

<dl>
<dt><strong>cos.api.key</strong></dt>
<dd>Required. API key used to connect to the Cloud Object Storage service instance.</dd>
<dt><strong>cos.bucket.location</strong></dt>
<dd>Required. Location of the Cloud Object Storage service bucket, for example: eu-gb.</dd>
<dt><strong>cos.bucket.name</strong></dt>
<dd>Required. Name of the Cloud Object Storage service bucket to write data into.</dd>
<dt><strong>cos.bucket.resiliency</strong></dt>
<dd>Required. Resiliency of the Cloud Object Storage bucket. Must be one of: cross-region, regional, or single-site.</dd>
<dt><strong>cos.service.crn</strong></dt>
<dd>Required. CRN for the Cloud Object Storage service instance.
<p>Ensure you enter the correct CRN:it is the resource instance ID ending with double colons. For example:<br/> 
<code>crn:v1:staging:public:cloud-object-storage:global:a/8c226dc8c8bfb9bc3431515a16957954:b25fe12c-9cf5-4ee8-8285-2c7e6ae707f6::</code></p></dd>
<dt><strong>cos.endpoint.visibility</strong></dt>
<dd>Optional. Specify public to connect to the Cloud Object Storage service over the public internet, or private to connect from a connector running inside the IBM Cloud network, for example from an IBM Cloud Kubernetes Service cluster. The default is public.</dd>
<dt><strong>cos.object.deadline.seconds </strong></dt>
<dd>Optional. The number of seconds (as measured wall clock time for the Connect Task instance) between reading the first record from Kafka, and writing all of the records read so far into a Cloud Object Storage object. This can be useful in situations where there are long pauses between Kafka records being produced to a topic, because it ensures that any records received by this connector will always be written into object storage within the specified period of time.</dd>
<dt><strong>cos.object.interval.seconds</strong></dt>
<dd>Optional. The number of seconds (as measured by the timestamps in Kafka records) between reading the first record from Kafka, and writing all of the records read so far into a Cloud Object Storage object.</dd>
<dt><strong>cos.object.records</strong></dt>
<dd>Optional. The maximum number of Kafka records to combine into a object.
</dd>
</dl>
 
### Get COS credentials using the IBM Cloud console
{: #connect_enterprise_external_console}

1. Locate your Cloud Object Storage service on the dashboard.
2. Click your service tile.
3. Click **Service Credentials**.
4. Click **New Credential**. 
5. Complete the details for your new credential like a name and role and click **Add**. A new credential appears in the credentials list.
6. Click this credential using **View Credentials** to reveal the details in JSON format.


## Step 7. Start the connector with its configuration
{: #step7_start_connector}

Run the following command to start the COS connector with the configuration that you provided in the previous step.

```
curl -X POST -H "Content-Type: application/json" http://localhost:8083/connectors --data "@./cos-sink.json"
```
{: codeblock}

## Step 8. Monitor your connector 
{: #step8_monitor_connector}

You can check your connector by going to <br/>
http://localhost:8083/connectors/cos-sink/status

If the state of the connector is not running, restart the connector.

