---

copyright:
  years: 2023
lastupdated: "2023-10-17"

keywords: quick setup guide

subcollection: EventStreams

content-type: tutorial
services: eventstreams
account-plan:
completion-time: 60m

---

{{site.data.keyword.attribute-definition-list}}
{:ui: .ph data-hd-interface="ui"}
{:cli: .ph data-hd-interface="cli"}
{:api: .ph data-hd-interface="api"}

# Quick Setup Guide for {{site.data.keyword.messagehub}} for {{site.data.keyword.cloud_notm}}
{: #quick-setup-guide}
{: toc-content-type="tutorial"}
{: toc-services="eventstreams"}
{: toc-completion-time="60m"}

This tutorial guides you through the steps to start using {{site.data.keyword.messagehub}} quickly by provisioning an instance, creating a topic and a credential then producing and consuming data. Additionally, you'll learn how to connect {{site.data.keyword.mon_full_notm}} and {{site.data.keyword.at_full}} and optionally how to use Kafka Connect or kSQLdb. Finally, you'll also find out how to get help with {{site.data.keyword.messagehub}}.
{: shortdesc}

Complete the following steps: {: ui}
* [Prerequisites](#prereqs)
* [Step 1: Choose your plan](#choose_plan)
* [Step 2: Provision an {{site.data.keyword.messagehub}} instance using the console](#provision_instance_ui)
* [Step 3: Create a topic and partitions using the console](#create_topic_ui)
* [Step 4: Create an IAM service credential using the console](#create_credential_ui)
* [Step 5: Produce data using the console](#produce_data_ui)
* [Step 6: Consume data using the console](#consume_data_ui)
* [Step 7: Connect IBM Cloud Monitoring](#connect_monitoring_ui)
* [Step 8: Connect Activity Tracker](#activity_tracker_ui)
* [Step 9: (Optional) Using Kafka Connect or kSQLdb](#kafka_connect_ksql)
* [Step 10: If you need more help](#getting_help)
{: ui}

Complete the following steps: {: cli}
* [Prerequisites](#prereqs)
* [Step 1: Choose your plan](#choose_plan)
* [Step 2: Provision an {{site.data.keyword.messagehub}} instance using the CLI](#provision_instance_cli)
* [Step 3: Create a topic and partitions using the CLI](#create_topic_cli)
* [Step 4: Create an IAM service credential using the CLI](#create_credential_cli)
* [Step 5: Produce data using the CLI](#produce_data_cli)
* [Step 6: Consume data using the CLI](#consume_data_cli)
* [Step 7: Connect IBM Cloud Monitoring](#connect_monitoring_cli)
* [Step 8: Connect Activity Tracker](#activity_tracker_cli)
* [Step 9: (Optional) Using Kafka Connect or kSQLdb](#kafka_connect_ksql)
* [Step 10: If you need more help](#getting_help)
{: cli}

Complete the following steps: {: api}
* [Prerequisites](#prereqs)
* [Step 1: Choose your plan](#choose_plan)
* [Step 2: Provision an {{site.data.keyword.messagehub}} instance using the API](#provision_instance_api)
* [Step 3: Create a topic and partitions using the API](#create_topic_api)
* [Step 4: Create an IAM service credential using the API](#create_credential_api)
* [Step 5: Produce data using the API](#produce_data_api)
* [Step 6: Consume data using the API](#consume_data_api)
* [Step 7: Connect IBM Cloud Monitoring](#connect_monitoring_api)
* [Step 8: Connect Activity Tracker](#activity_tracker_api)
* [Step 9: (Optional) Using Kafka Connect or kSQLdb](#kafka_connect_ksql)
* [Step 10: If you need more help](#getting_help)
{: api}



## Prerequisites
{: #prereqs}
{: step}

Before you get started, we highly recommend you read the following information to better understand Apache Kafka, which {{site.data.keyword.messagehub}} is built on:
* [Apache Kafka concepts](/docs/EventStreams?topic=EventStreams-apache_kafka)
* [Apache Kafka fundamentals](https://developer.ibm.com/articles/event-streams-kafka-fundamentals/?mhsrc=ibmsearch_a&mhq=event%20streams)


## Choose your plan 
{: #choose_plan}
{: step}

{{site.data.keyword.messagehub}} offers three different plans. To help you decide which one to choose, see [Choosing your plan](/docs/EventStreams?topic=EventStreams-plan_choose){: external} for more information.

* The Lite plan offers access to a single partition in a multi-tenant {{site.data.keyword.messagehub}} cluster free of charge.	

* The Standard plan offers pay-as-you-go access to the multi-tenant {{site.data.keyword.messagehub}} service. It's charged on a per partition-hour basis with an additional per GB charge for outbound data consumption.

* The Enterprise plan offers pay-as-you-go access to an isolated single-tenant {{site.data.keyword.messagehub}} service. This plan also offers user-managed encryption, private endpoints, and a selection of throughput and storage options. 

## Provision an {{site.data.keyword.messagehub}} instance by using the console
{: #provision_instance_ui}
{: step}
{: ui}

1. Log in to the {{site.data.keyword.cloud_notm}} console.
  
2. Click the [**{{site.data.keyword.messagehub}} service**](https://cloud.ibm.com/catalog/event-streams){: external} in the **Catalog**.
  
3. Select the **Lite plan**, **Standard plan**, or **Enterprise plan** from the **Select a pricing plan** section.
  
4. Enter a name for your service. You can use the default value.
  
5. Click **Create**. The {{site.data.keyword.messagehub}} **Resource list** page opens. 

6. When your instance has been created, click on the instance name to view more information.


## Provision an {{site.data.keyword.messagehub}} instance by using the CLI
{: #provision_instance_cli}
{: step}
{: cli}

To use the {{site.data.keyword.messagehub}} CLI for the first time, see [Getting started with the CLI](/docs/EventStreams?topic=EventStreams-cli#cli).

To provision an instance of {{site.data.keyword.messagehub}} Standard Plan with the {{site.data.keyword.cloud_notm}} CLI, complete the following steps:

1. Install the {{site.data.keyword.Bluemix_notm}} CLI
{: #step1_install_cli}

    For more information about how to install the CLI, see [Getting started with the {{site.data.keyword.Bluemix_notm}} CLI](/docs/cli?topic=cloud-cli-getting-started){: external}.

2. Log in to {{site.data.keyword.Bluemix_notm}} 
{: #step2_login}

    Run the following command to log in to {{site.data.keyword.Bluemix_notm}}:

    ```text
    ibmcloud login -a cloud.ibm.com
    ```
    {: codeblock}

3. Create an {{site.data.keyword.messagehub}} instance on {{site.data.keyword.Bluemix_notm}} by using the Lite, Standard, or Enterprise plans.
{: #step3_es_instance}
     
    Select one of the following methods:

    * To create an instance from the CLI on the Enterprise plan, run the following command:

        ```text
        ibmcloud resource service-instance-create <INSTANCE_NAME> messagehub enterprise <REGION>
        ```
        {: codeblock}
   
        Because the Enterprise plan has its own dedicated resources for each cluster, it requires more time for provisioning so a new Enterprise instance might take up to 3 hours.


    * To create an instance from the CLI on the Standard plan, run the following command:

        ```text
        ibmcloud resource service-instance-create <INSTANCE_NAME> messagehub standard <REGION>
        ```
        {: codeblock}

        Provisioning a new Standard plan instance is instantaneous because the underlying resources are already set up.


## Provision an {{site.data.keyword.messagehub}} instance by using the API
{: #provision_instance_api}
{: step}
{: api}

**Which API should we focus on? How do you provision an instance via the API?**


## Create a topic and select number of partitions by using the console
{: #create_topic_ui}
{: step}
{: ui}

For guidance about the settings that you can modify when creating topics, see [topic configuration](/docs/EventStreams?topic=EventStreams-kafka_java_api).

1. From your newly provisioned instance in the [**Catalog**](https://cloud.ibm.com/catalog/event-streams){: external}, navigate to **Topics** from the menu on the left.
2. Click the **Create topic** button and an enter a topic name. Click **Next**. Topic names are restricted to a maximum of 100 characters.
3. Select the number of partitions. Click **Next**.

    One or more partitions make up a topic. A partition is an ordered list of messages. 1 partition is sufficient for getting started, but production systems often have more.

    Partitions are distributed across the brokers to increase the scalability of your topic. You can also use them to distribute messages across the members of a consumer group.

    _Talk about Creating, listing, updating, and deleting topics, Describing the cluster.
    Bring in information like suggested topic naming strategies_

4. Set the message retention period. This is how long messages are retained before they are deleted.
    If your messages are not read by a consumer within this time, they will be missed.

    Click **Create topic**.

### Working with topics
{: #work_topic_ui}
{: ui}

After you create topics, you can use the console to [list](#list_topic_ui), [delete](#delete_topic_ui), and [update the configuration of topics](#ibmcloud_es_topic_update_cli). You can also use the CLI to [view details about your cluster](#ibmcloud_es_cluster_cli).


_Talk about Creating, listing, updating, and deleting topics, Describing the cluster_
_Bring in information like suggested topic naming strategies_

#### List topics
{: #list_topic_ui}
{: ui}

From your {{site.data.keyword.messagehub}} instance in the [**Catalog**](https://cloud.ibm.com/catalog/event-streams){: external}, navigate to **Topics** from the menu on the left.

From the **Topics page**, you can view the following information about your topics: 
**Name**, **Partitions**, **Retention time**, **Retention size**, **Cleanup policy**, and **Stream landing**.

#### Delete a topic
{: #delete_topic_ui}
{: ui}

From your {{site.data.keyword.messagehub}} instance in the [**Catalog**](https://cloud.ibm.com/catalog/event-streams){: external}, navigate to **Topics** from the menu on the left.

From the **Topics page**, click the three dots to the right of the topic name and click **Delete this topic**. 


## Create a topic and select number of partitions by using the CLI 
{: #create_topic_cli}
{: step}
{: cli}

For guidance about the settings that you can modify when creating topics, see [topic configuration](/docs/EventStreams?topic=EventStreams-kafka_java_api).

Run the following [**ibmcloud es topic-create** command](/docs/EventStreams?topic=EventStreams-cli_reference#ibmcloud_es) to create a new topic with one partition: 

```bash
ibmcloud es topic-create [--name] topic1 [--partitions 1] 
```
{: codeblock}

**Prerequisites**: None

**Command options**:

--name value
:   Topic name. Topic names are restricted to a maximum of 100 characters.

--partitions value
:   Set the number of partitions for the topic.

    One or more partitions make up a topic. A partition is an ordered list of messages. 1 partition is sufficient for getting started, but production systems often have more.

    Partitions are distributed across the brokers to increase the scalability of your topic. You can also use them to distribute messages across the members of a consumer group.

### Working with topics
{: #work_topic_cli}
{: cli}

After you create topics, you can use the CLI to [list](#ibmcloud_es_topic_list_cli), [delete](#ibmcloud_es_topic_delete_cli), and [update the configuration of topics](#ibmcloud_es_topic_update_cli). You can also use the CLI to [view details about your cluster](#ibmcloud_es_cluster_cli).


_Bring in information like suggested topic naming strategies_

#### List a topic using the **ibmcloud es topics** command
{: #ibmcloud_es_topic_list_cli}

Run the **ibmcloud es topics** command to list your topics.

```bash
ibmcloud es topics [--filter FILTER] [--json]
```
{: codeblock}

**Prerequisites**: None

**Command options**:

--filter value, -f value (optional)
:   Topic name.
  
--json (optional)
:   Format output in JSON. Up to 1000 topics are returned.

#### Delete a topic using the **ibmcloud es topic-delete** command
{: #ibmcloud_es_topic_delete_cli}

Run the **ibmcloud es topic-delete** command to delete a topic.

```bash
ibmcloud es topic-delete [--name] TOPIC_NAME [--force]
```
{: codeblock}

**Prerequisites**: None

**Command options**:

--name value, -n value
:   Topic name.

--force, -f (optional)
:   Delete without confirmation.


#### Display cluster details using the **ibmcloud es cluster** command
{: #ibmcloud_es_cluster_cli}

Run the **ibmcloud es cluster** command to display the details of the cluster, including the Kafka version.

```bash
ibmcloud es cluster [--json]
```
{: codeblock}

**Prerequisites**: None

**Command options**:

--json (optional)
:   Output format in JSON.



#### Update the configuration of a topic using the **ibmcloud es topic-update** command
{: #ibmcloud_es_topic_update_cli}

Run the **ibmcloud es topic-update** command to update the configuration of a topic.

```bash
ibmcloud es topic-update [--name] TOPIC_NAME --config KEY[=VALUE][;KEY[=VALUE]]* [--default]
```
{: codeblock}

**Prerequisites**: None

**Command options**:

--name value, -n value
:   Topic name.

--config KEY[=VALUE], -c KEY[=VALUE]
:   Set a configuration option for the topic as a KEY[=VALUE] pair.
:   If VALUE is not given, the '--default' flag is to be specified to indicate resetting the configuration value back to the default. Multiple '--config' options can be specified. Each '--config' option can specify a semicolon-delimited list of assignments. The following list shows valid configuration keys:

    - cleanup.policy
    - retention.ms
    - retention.bytes
    - segment.bytes
    - segment.ms
    - segment.index.bytes

--default, -d  (optional)
:   Reset each configuration parameter that is specified by using '--config' to its default value.



## Create a topic and select number of partitions by using the Admin REST API
{: #create_topic_api}
{: step}
{: api}

{{site.data.keyword.messagehub}} provides a REST API for administration that you can use to create, delete, list, and update topics.

You can create a Kafka topic by issuing a POST request to the `/admin/topics` path. The body of the request must contain a JSON document. For example:

```json
{
    "name": "topicname",
    "partitions": 1,
    "configs": {
        "retentionMs": 86400000,
        "cleanupPolicy": "delete"
    }
}
```
{: codeblock}


The JSON document must contain a `name` attribute, specifying the name of the Kafka topic to create. The JSON can also specify the number of partitions to assign to the topic (using the `partitions` property). If the number of partitions is not specified, the topic is created with a single partition.

You can also specify an optional `configs` object within the request. This allows the specification of the `retentionMs` property, which controls how long (in milliseconds) Kafka retains messages published to the topic. After this time elapses the messages are automatically deleted to free space. Note that the value of the `retentionMs` property must be specified in a whole number of hours (for example, multiples of 3600000).

For guidance about the settings that you can modify when creating topics, see [topic configuration](/docs/EventStreams?topic=EventStreams-kafka_java_api).

Expected HTTP status codes:

* 202: Topic creation request was accepted.
* 400: Invalid request JSON.
* 403: Not authorized to create topic.
* 422: Semantically invalid request.

If the request to create a Kafka topic succeeds, HTTP status code 202 (Accepted) is returned. If the operation fails, a HTTP status code of 422 (Unprocessable Entity) is returned, and a JSON object containing additional information about the failure is returned as the body of the response.

### Example
{: #create_topic_api_example}

You can exercise the REST endpoint for creating a Kafka topic using the following snippet of curl. You need to supply your own API key or token and specify the correct endpoint for ADMIN API.

```sh
curl -i -X POST -H 'Accept: application/json' -H 'Content-Type: application/json' -H 'Authorization: Bearer ${TOKEN}' --data '{ "name": "newtopic", "partitions": 1}' ${ADMIN_URL}/admin/topics
```
{: codeblock}


### Working with topics
{: #work_topic_api}
{: api}

After you create topics, you can use the Admin REST API to list and delete topics and update topic configuration.

#### List Kafka topics
{: #topic_list_api}

You can list all your Kafka topics by issuing a GET request to the
`/admin/topics` path. 

Expected status code:

* 200: the topic list is returned as JSON in the following format:

```json
[
  {
    "name": "topic1",
    "partitions": 1,
    "retentionMs": 86400000,
    "cleanupPolicy": "delete"
  },
  { "name": "topic2",
    "partitions": 2,
    "retentionMs": 86400000,
    "cleanupPolicy": "delete"
  }
]
```
{: codeblock}

A successful response will have HTTP status code 200 (OK) and contain an
array of JSON objects, where each object represents a Kafka topic and has the following properties:

| Property name     | Description                                             |
|-------------------|---------------------------------------------------------|
| name              | The name of the Kafka topic.                            |
| partitions        | The number of partitions assigned to the Kafka topic.   |
| retentionsMs      | The retention period for messages on the topic (in ms). |
| cleanupPolicy     | The cleanup policy of the Kafka topic.        |
{: caption="Table 1. {{site.data.keyword.messagehub}} topic properties" caption-side="top"}               

##### List topics example
{: #topic_list_example_api}

You can use the following curl command to list all your Kafka topics:

```sh
curl -i -X GET -H 'Accept: application/json' -H 'Authorization: Bearer ${TOKEN}' ${ADMIN_URL}/admin/topics
```
{: codeblock}

#### Delete a Kafka topic
{: #topic_delete_api}

To delete a Kafka topic, issue a DELETE request to the `/admin/topics/TOPICNAME`path (where TOPICNAME is the name of the Kafka topic that you want to delete).

Expected return codes:
- 202: Topic deletion request was accepted.
- 403: Not authorized to delete topic.
- 404: Topic does not exist.
  
A 202 (Accepted) status code is returned if the REST API accepts the delete
request or status code 422 (Unprocessable Entity) if the delete request is
rejected. If a delete request is rejected, the body of the HTTP response contains a [JSON object](#information-returned-when-a-request-fails) which
provides additional information about why the request was rejected.

Kafka deletes topics asynchronously. Deleted topics can still appear in the
response to a [list topics request](#listing-kafka-topics) for a short period of time after the completion of a REST request to delete the topic.

##### Delete topic example
{: #topic_delete_example_api}

The following curl command deletes a topic called `MYTOPIC`:

```sh
curl -i -H 'Content-Type: application/json' -X DELETE -H 'Authorization: Bearer ${TOKEN}' ${ADMIN_URL}/admin/topics/MYTOPIC
```
{: codeblock}

#### Update a topic's configuration
{: #topic_update_api}

To increase a topic's partition number or to update a topic's configuration, issue a`PATCH` request to `/admin/topics/{topic}` with the following body:

```json
{
  "new_total_partition_count": 4,
  "configs": [
    {
      "name": "cleanup.policy",
      "value": "compact"
    }
  ]
}
```
{: codeblock}

The following configuration keys are supported: 'cleanup.policy', 'retention.ms', 'retention.bytes', 'segment.bytes', 'segment.ms', and 'segment.index.bytes'.

You can only increase the partition number, not decrease it.

Expected status codes:
    - 202: Update topic request was accepted.
    - 400: Invalid request JSON/number of partitions is invalid.
    - 404: Topic specified does not exist.
    - 422: Semantically invalid request.

##### Update topic configuration example
{: #topic_update_example_api}

The following curl command updates a topic called `MYTOPIC`, set its `partitions` to 4 and its `cleanup.policy` to be `compact`.

```sh
curl -i -X PATCH -H 'Content-Type: application/json' -H 'Authorization: Bearer ${TOKEN}' --data '{"new_total_partition_count": 4,"configs":[{"name":"cleanup.policy","value":"compact"}]}' ${ADMIN_URL}/admin/topics/MYTOPIC
```
{: codeblock}


_Talk about Creating, listing, updating, and deleting topics, Describing the cluster._
_Bring in information like suggested topic naming strategies_

## Create an IAM service credential by using the console
{: #create_credential_ui}
{: step}
{: ui}

To create a service key by using the {{site.data.keyword.Bluemix_notm}} console:

1. Locate your {{site.data.keyword.messagehub}} service in the **Resource list**.
2. Click your service tile.
3. Click **Service Credentials**.
4. Click **New Credential**. 
5. Complete the details for your new credential like a name and role and click **Add**. A new credential appears in the credentials list.
6. Click this credential by using **View Credentials** to reveal the details in JSON format.

## Create an IAM service credential by using the CLI
{: #create_credential_cli}
{: step}
{: cli}

To create a service key by using the {{site.data.keyword.Bluemix_notm}} CLI, complete the following steps.

1. Locate your service: 
    ```bash
    ibmcloud resource service-instances
    ```
    {: codeblock}

2. Create a service key: 
    ```bash
    ibmcloud resource service-key-create <key_name> <key_role> --instance-name <your_service_name>
    ```
    {: codeblock}

3. Print the service key: 
    ```bash
    ibmcloud resource service-key <key_name>
    ```
    {: codeblock}

    A single set of endpoint details are contained in each service key. For service instances configured to be connected to a single network type, either the {{site.data.keyword.Bluemix_notm}} Public network (the default) or the {{site.data.keyword.Bluemix_notm}} Private network, the service key contains the details relevant to that network type. For instances configured to support both the private and public networks, details for the public network are returned. If you want details for the private network, you must add the `--service-endpoint private` parameter the previous CLI command, as in the following example. 
    {: note}

    ```bash
    ibmcloud resource service-key-create <private-key-name> <role> --instance-name <instance-name> --service-endpoint private
    ```
    {: codeblock}

## Create an IAM service credential by using the API
{: #create_credential_api}
{: step}
{: api}

**How do you create this via the API?**

## Produce data using the console
{: #produce_data_ui}
{: step}
{: ui}

You cannot produce data by using the console. You can produce data only using the [CLI]({#produce_data_cli}) or [API]({#produce_data_cli}).


## Produce data using the CLI
{: #produce_data_cli}
{: step}
{: cli}


You can use the {{site.data.keyword.messagehub}}Kafka console producer tool to produce data. The console tools are in the `bin` directory of your Kafka client download, which you can download from [Apache Kafka downloads](http://kafka.apache.org/downloads){: external}.

You must provide a list of brokers (using the BOOTSTRAP_ENDPOINTS property) and SASL credentials. To provide the SASL credentials to this tool, create a properties file based on the following example:

```config
    sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="USER" password="PASSWORD";
    security.protocol=SASL_SSL
    sasl.mechanism=PLAIN
    ssl.protocol=TLSv1.2
    ssl.enabled.protocols=TLSv1.2
    ssl.endpoint.identification.algorithm=HTTPS
```
{: codeblock}

Replace USER and PASSWORD with the values from your {{site.data.keyword.messagehub}} **Service Credentials** tab in the {{site.data.keyword.Bluemix_notm}} console.

After you create the properties file, you can run the console producer in a terminal as follows:

```bash
   kafka-console-producer.sh --broker-list BOOTSTRAP_ENDPOINTS --producer.config CONFIG_FILE --topic TOPIC_NAME
```
{: codeblock}

Replace the following variables in the example with your own values:

- BOOTSTRAP_ENDPOINTS with the value from your {{site.data.keyword.messagehub}} **Service Credentials** tab in the {{site.data.keyword.Bluemix_notm}} console.
- CONFIG_FILE with the path of the configuration file. 

You can use many of the other options of this tool, except for those that require access to ZooKeeper.For more information about this tool, see [Using Kafka console tools with Event Streams](/docs/EventStreams?topic=EventStreams-kafka_console_tools).



### Configuration settings
{: #producer_config_cli}
{: cli}

For details of settings that you can configure for the producer, for example ```acks``` and ```retries```, see
[configuration settings](/docs/EventStreams?topic=EventStreams-producing_messages#config_settings).

_b. via CLI support different languages - show Java library_

_Include connection details and sample code to connect to the event streams instance_

_Highlight the most important kafka settings for producers are here including delivery semantics, acknowledgements, number of retries, session timeout, heartbeat interval, rebalance strategy (JAVA API supports multiple strategies to reduce rebalance)_

## Produce data using the API
{: #produce_data_api}
{: step}
{: api}

**How do you produce data using the API?**

### Configuration settings
{: #producer_config_api}
{: api}

For details of settings that you can configure for the producer, for example ```acks``` and ```retries```, see
[configuration settings](/docs/EventStreams?topic=EventStreams-producing_messages#config_settings).


_b. via CLI c. via API - support different languages - show Java library)_

_Include connection details and sample code to connect to the event streams instance_

_Highlight the most important kafka settings for producers are here including delivery semantics, acknowledgements, number of retries, session timeout, heartbeat interval, rebalance strategy (JAVA API supports multiple strategies to reduce rebalance)_

## Consume data using the console
{: #consume_data_ui}
{: step}
{: ui}

You cannot consume data by using the console. You can consume data only using the [CLI]({#consume_data_cli}) or [API]({#consume_data_api}).

## Consume data using the CLI
{: #consume_data_cli}
{: step}
{: cli}


You can use the {{site.data.keyword.messagehub}} Kafka console consumer tool to consume data. 

The console tools are in the `bin` directory of your Kafka client download.

You must provide a list of brokers and SASL credentials. After you create the properties file as described in [produce data](#produce_data_cli), run the console consumer in a terminal as follows:

```bash
   kafka-console-consumer.sh --bootstrap-server BOOTSTRAP_ENDPOINTS --consumer.config CONFIG_FILE --topic TOPIC_NAME 
```
{: codeblock}

Replace the following variables in the example with your own values:

- BOOTSTRAP_ENDPOINTS with the value from your {{site.data.keyword.messagehub}} **Service Credentials** tab in the {{site.data.keyword.Bluemix_notm}} console. 
- CONFIG_FILE with the path of the configuration file. 

You can use many of the other options of this tool, except for those that require access to ZooKeeper. For more information about this tool, see [Using Kafka console tools with Event Streams](/docs/EventStreams?topic=EventStreams-kafka_console_tools).

### Configuration settings
{: #consumer_config_cli}
{: cli}

For details of settings that you can configure for the consumer, for example ```group.id``` and ```enable.auto.commit```, see
[configuration settings](/docs/EventStreams?topic=EventStreams-consuming_messages#configuring_consumer_properties).

_b. via CLI c. via API - support different languages - show Java library_

_Include connection details and sample code to connect to the event streams instance_

_Highlight the most important kafka settings for consumers are here including commit offsets, exactly once semantics, consumer groups and liveness_

## Consume data using the API 
{: #consume_data_api}
{: step}
{: api}

**How do you consume data using the API?**

### Configuration settings
{: #consumer_config_api}
{: api}

For details of settings that you can configure for the consumer, for example ```group.id``` and ```enable.auto.commit```, see
[configuration settings](/docs/EventStreams?topic=EventStreams-consuming_messages#configuring_consumer_properties).


b. via CLI c. via API - support different languages - show Java library_

_Include connection details and sample code to connect to the event streams instance_

_Highlight the most important kafka settings for consumers are here including commit offsets, exactly once semantics, consumer groups and liveness_

## Connect {{site.data.keyword.mon_full_notm}} for operational visibility by using the console 
{: #connect_monitoring_ui}
{: step}
{: ui}

_(a. via UI only - walk through steps ), (Explain benefits)_

Use {{site.data.keyword.monitoringshort}} to gain operational visibility into the performance and health of your applications, services, and platforms. {{site.data.keyword.monitoringshort}} offers administrators, DevOps teams, and developers full stack telemetry with advanced features to monitor and troubleshoot, define alerts, and design custom dashboards.
To find out more, see [Monitoring Event Streams metrics by using IBM Cloud Monitoring](/docs/EventStreams?topic=EventStreams-metrics).

After creating an instance
Resource list - select instance- Actions-> Add monitoring



## Connect {{site.data.keyword.mon_full_notm}} for operational visibility by using the CLI 
{: #connect_monitoring_cli}
{: step}
{: cli}

You cannot connect {{site.data.keyword.mon_full_notm}} by using the CLI. Use the [console]({#connect_monitoring_ui}) to complete this task.

## Connect {{site.data.keyword.mon_full_notm}} for operational visibility by using the API
{: #connect_monitoring_api}
{: step}
{: api}

You cannot connect {{site.data.keyword.mon_full_notm}} by using the API. Use the [console]({#connect_monitoring_ui}) to complete this task.


## Connect {{site.data.keyword.at_full}} to audit service activity (using the console only - walk through steps ), (Explain benefits)
{: #activity_tracker_ui}
{: step}
{: ui}

{{site.data.keyword.atracker_short}} allows you to view, manage, and audit service activity to comply with corporate policies and industry regulations.

{{site.data.keyword.at_full_notm}} can have only one instance per location. To view events, you must access the web UI of the {{site.data.keyword.at_full_notm}} service in the same location where your service instance is available. For more information, see [Launch the web UI](/docs/activity-tracker?topic=activity-tracker-getting-started#gs_step4){: external}.

[{{site.data.keyword.cloudaccesstrailshort}} events](/docs/EventStreams?topic=EventStreams-at_events).

## Connect {{site.data.keyword.at_full}} using the CLI to audit service activity
{: #activity_tracker_cli}
{: step}
{: cli}

You cannot connect {{site.data.keyword.atracker_short}} using the CLI. Use the [console]({#activity_tracker_ui}) to complete this task.

## Connect {{site.data.keyword.at_full}} using the API to audit service activity
{: #activity_tracker_api}
{: step}
{: api}

You cannot connect {{site.data.keyword.atracker_short}} using the API. Use the [console]({#activity_tracker_ui}) to complete this task.


## (Optional) Using Kafka Connect or kSQLdb
{: #kafka_connect_ksql}
{: step} 

_Link to additional docs page content, highlight that this is not part of the managed service_

Kafka Connect is part of the Apache Kafka project and allows you to connect external systems to Kafka. It consists of a runtime  that can run connectors to copy data to and from a cluster.

Its key benefits are as follows:

* Scalability: it can easily scale from a single worker to many.
* Reliability: it automatically manages offsets and the lifecycle of connectors
* Extensibility: the community has built connectors for most popular systems.

For more information about how to use it, see [Using Kafka Connect with Event Streams](/docs/EventStreams?topic=EventStreams-kafka_connect).

Kafka Connect is not part of the managed {{site.data.keyword.messagehub}} service.

You can use [KSQL](https://github.com/confluentinc/ksql){: external} with {{site.data.keyword.messagehub}} for stream processing. 
[Using ksqlDB with Event Streams](/docs/EventStreams?topic=EventStreams-ksql_using)



## Getting help
{: #getting_help}
{: step}

For a general overview of how to get help with {{site.data.keyword.messagehub}} and where to get support, see [Getting help and support](/docs/EventStreams?topic=EventStreams-gettinghelp).

[FAQs](/docs/EventStreams?topic=EventStreams-faqs) details answers to some of the common questions about {{site.data.keyword.messagehub}}.

If you're experiencing a problem with {{site.data.keyword.messagehub}}, here's a list of the information you need to gather before you open a case [Reporting a problem to the Event Streams team - Standard and Enterprise plans](/docs/EventStreams?topic=EventStreams-report_problem_enterprise).




For Info to gather if having a problem, Add suggestions for what they need to do if having a problem - or directly link to this page. Include links to FAQ page, Ticket info, slack channel?

