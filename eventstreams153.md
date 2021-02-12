---

copyright:
  years: 2015, 2021
lastupdated: "2021-02-12"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka, MQ bridge

subcollection: EventStreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Connecting IBM MQ to {{site.data.keyword.messagehub}} using the Kubernetes Service
{: #mq_connector}

The following task walks you through:
* getting the Kafka Connect runtime running in an IKS cluster 
* starting the MQ Source Connector to copy messages from an IBM MQ source queue to a destination Kafka topic in {{site.data.keyword.messagehub}}

The MQ Source Connector connects to an IBM MQ queue manager and consumes MQ message data from an MQ queue. The Connector converts each MQ message into a Kafka record and sends the message to an {{site.data.keyword.messagehub}} Kafka topic.

Complete the following steps to get set up:
{: shortdesc}

## Step 1. Install the prerequisites
{: #step1_install_prereqs_mq}
Ensure you have the following software and services installed:

* An {{site.data.keyword.messagehub}} instance - Standard or Enterprise plan. 
* An instance of [IBM MQ on Cloud ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/mqcloud?topic=mqcloud-mqoc_getting_started){:new_window} or [IBM MQ Version 8 ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/messaging/mq-downloads){:new_window}, or later. 
   
   You can configure the MQ Connector to authenticate with IBM MQ using a user identifier and password. We recommend that you grant the following permissions only to the identity associated with an instance of the MQ bridge:
   * CONNECT authority. The MQ Connector must be able to connect to the MQ queue manager.
   * GET authority for the queue that the MQ Connector is configured to consume from.
* An {{site.data.keyword.containerfull}} cluster. You can provision a free one for testing purposes. 

    You will also need CLI access to your cluster. For more information, see
 [Setting up the CLI and API](/docs/containers?topic=containers-cs_cli_install).
* A recent version of Kubectl.
* [git ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://git-scm.com/downloads){:new_window}

## Step 2. Clone the kafka-connect repositories
{: #step2_clone project_mq}

Clone the following two repositories that contain the required files:

* https://github.com/ibm-messaging/kafka-connect-mq-source
* https://github.com/ibm-messaging/event-streams-samples


## Step 3. Create your Kafka Connect configuration
{: #step3_create_config_mq}

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
{: #step4_deploy_kafka_mq}

Apply the configuration in the <code>kafka-connect.yaml</code> file by running the following command:

```
kubectl apply -f ./kafka-connect.yaml
```
{: codeblock}


## Step 5. Validate Kafka Connect is running
{: #step5_validate_connector_mq}

To validate that Kafka Connect is running, port forward to the kafkaconnect-service Service on port 8083. For example:

```
kubectl port-forward service/kafkaconnect-service 8083
```
{: codeblock}

Keep the terminal that you've used for port forwarding open, and use another terminal for the next steps.

The Connect REST API is then available at http://localhost:8083. If you want more information about the API, see
[Kafka Connect REST Interface ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://kafka.apache.org/documentation/#connect_rest){:new_window}.

So, you now have the Kafka Connect runtime deployed and running in IKS. Next, let's configure and start the MQ Connector.


<!--
## Step 6. Build the connector
{: #step6_build_connector}

1. Clone the repository with the following command:

    ```
    git clone https://github.com/ibm-messaging/kafka-connect-mq-source
    ```

2. Change into the <code>kafka-connect-mq-source</code> directory:

    ```
    cd kafka-connect-mq-source
    ```

3. Build the connector using Gradle:

    ```
    $ gradle shadowJar
    ```
-->

## Step 6. Configure the mq-source json file
{: #step6_config_json_mq}

Edit the <code>mq-source.json</code> file located in <code>kafka-connect-mq-source/config</code> so that, at a minimum, the required properties are completed with your information.

### mq-source.json file properties

Replace the placeholders in the <code>mq-source.json</code> file with your own values.

<dl>
<dt><strong>TOPIC</strong></dt>
<dd>Required. Name of the destination Kafka topic</dd>
<dt><strong>QUEUE_MANAGER</strong></dt>
<dd>Required. Name of the source MQ queue manager</dd>
<dt><strong>QUEUE</strong></dt>
<dd>Required. Name of the source MQ queue </dd>
<dt><strong>CHANNEL_NAME</strong></dt>
<dd>Required (unless you're using bindings or a CCDT file). Name of the server-connection channel.</dd>
<dt><strong>CONNECTION_NAME_LIST</strong></dt>
<dd>Required (unless you're using bindings or a CCDT file). A list of one or more host(port) pairs for connecting to the queue manager. Separate entries with a comma. 
</dl>

<!--
### Get IBM MQ on Cloud credentials using the IBM Cloud console
{: #connect_enterprise_external_console_mq}

1. Locate your MQ service on the dashboard.
2. Click your service tile.
3. Click **Service Credentials**.
4. Click **New Credential**. 
5. Complete the details for your new credential like a name and role and click **Add**. A new credential appears in the credentials list.
6. Click this credential using **View Credentials** to reveal the details in JSON format.
-->

## Step 7. Start the connector with its configuration
{: #step7_start_connector_mq}

Run the following command to start the MQ connector with the configuration that you provided in the previous step.

```
curl -X POST -H "Content-Type: application/json" http://localhost:8083/connectors --data "@./mq-source.json"
```
{: codeblock}

## Step 8. Monitor your connector 
{: #step8_monitor_connector_mq}

You can check your connector by going to <br/>
http://localhost:8083/connectors/mq-source/status

If the state of the connector is not running, restart the connector.

