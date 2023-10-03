---

copyright:
  years: 2023
lastupdated: "2023-10-03"

keywords: quick setup guide

subcollection: EventStreams

content-type: tutorial
services: eventstreams
account-plan:
completion-time: 45m

---

{{site.data.keyword.attribute-definition-list}}
{:ui: .ph data-hd-interface="ui"}
{:cli: .ph data-hd-interface="cli"}
{:api: .ph data-hd-interface="api"}

# Quick Setup Guide for {{site.data.keyword.messagehub}} for {{site.data.keyword.cloud_notm}}
{: #quick-setup-guide}
{: toc-content-type="tutorial"}
{: toc-services="eventstreams"}
{: toc-completion-time="45m"}

This tutorial guides you through starting to use {{site.data.keyword.messagehub}} by provisioning an instance, creating a topic and a credential then producing and consuming data. Additionally, you'll learn how to connect Cloud Monitoring and Activity Tracker and optionally how to use Kafka Connect or kSQLdb. Finally, you'll also find out how you can get help with {{site.data.keyword.messagehub}}.
{: shortdesc}

* [Prerequisites](#prereqs)
* [Step 1: Choose your plan](#choose_plan)
* [Step 2: Provision an {{site.data.keyword.messagehub}} instance using the console](#provision_instance_ui){: ui}
* [Step 2: Provision an {{site.data.keyword.messagehub}} instance using the CLI](#provision_instance_cli){: cli}
* [Step 2: Provision an {{site.data.keyword.messagehub}} instance using the API](#provision_instance_api){: api}
* [Step 3: Create a topic and partitions using the console](#create_topic_ui){: ui} 
* [Step 3: Create a topic and partitions using the CLI](#create_topic_cli){: cli}
* [Step 3: Create a topic and partitions using the API](#create_topic_api){: api}
* [Step 4: Create an IAM service credential using the console](#create_credential_ui){: ui} 
* [Step 4: Create an IAM service credential using the CLI](#create_credential_cli){: cli}
* [Step 4: Create an IAM service credential using the API](#create_credential_api){: api}
* [Step 5: Produce data using the console](#produce_data_ui){: ui}
* [Step 5: Produce data using the CLI](#produce_data_cli){: cli}
* [Step 5: Produce data using the API](#produce_data_api){: api}
* [Step 6: Consume data using the console](#consume_data_ui){: ui}
* [Step 6: Consume data using the CLI](#consume_data_cli){: cli}
* [Step 6: Consume data using the API](#consume_data_api){: api}
* [Step 7: Connect IBM Cloud Monitoring](#connect_monitoring)
* [Step 8: Connect Activity Tracker](#activity_tracker)
* [Step 9: (Optional) Using Kafka Connect or kSQLdb](#kafka_connect_ksql)
* [Step 10: If you need more help](#getting_help)


## Prerequisites
{: #prereqs}
{: step}

Before you get started, we highly recommend you read the following information to better understand Apache Kafka, which {{site.data.keyword.messagehub}} is built on:
* [Apache Kafka concepts](/docs/EventStreams?topic=EventStreams-apache_kafka)
* [Apache Kafka fundamentals](https://developer.ibm.com/articles/event-streams-kafka-fundamentals/?mhsrc=ibmsearch_a&mhq=event%20streams)


## Choose your plan 
{: #choose_plan}
{: step}

To help you decide which plan to choose, see [Choosing your plan](/docs/EventStreams?topic=EventStreams-plan_choose){: external} for more information.

* The Lite plan offers access to a single partition in a multi-tenant {{site.data.keyword.messagehub}} cluster free of charge.	

* The Standard plan offers pay as you go access to the multi-tenant {{site.data.keyword.messagehub}} service. Charged on a per partition-hour basis with an additional per GB charge for outbound data consumption.

* The Enterprise plan offers pay as you go access to an isolated single-tenant {{site.data.keyword.messagehub}} service. It also offers customer-managed encryption, private endpoints, and a selection of throughput and storage options. 

_Direct to choosing your plan page, give a high level summary of the plans? and highlight that Enterprise plan allows for customer managed encryption and private end points and different throughput/storage options - the intent here is to upsell_
_Encourage users to familiarise themselves with Apache Concepts docs page_

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
   
    Because Enterprise has its own dedicated resources for each cluster, it requires more time for provisioning so a new Enterprise instance might take up to 3 hours.


    * To create an instance from the CLI on the Standard plan, run the following command:

    ```text
    ibmcloud resource service-instance-create <INSTANCE_NAME> messagehub standard <REGION>
    ```
    {: codeblock}

    Provisioning a new Standard instance is instantaneous because the underlying resources are already set up.


## Provision an {{site.data.keyword.messagehub}} instance by using the API
{: #provision_instance_api}
{: step}
{: api}

**Which API should we focus on?**


## Create a topic and select number of partitions by using the console
{: #create_topic_ui}
{: step}
{: ui}

1. From your newly provisioned instance in the [**Catalog**](https://cloud.ibm.com/catalog/event-streams){: external}, navigate to **Topics** from the menu on the left.
2. Click the **Create topic** button and an enter a topic name. Click **Next**. Topic names are restricted to a maximum of 100 characters.
3. Select the number of partitions. Click **Next**.

    One or more partitions make up a topic. A partition is an ordered list of messages. 1 partition is sufficient for getting started, but production systems often have more.

    Partitions are distributed across the brokers in order to increase the scalability of your topic. You can also use them to distribute messages across the members of a consumer group.

    *Talk about Creating, listing, updating, and deleting topics, Describing the cluster.
    Bring in information like suggested topic naming strategies*

4. Set the message retention period. Click **Create topic**.

    This is how long messages are retained before they are deleted.

    If your messages are not read by a consumer within this time, they will be missed.

### Working with topics
{: #work_topic_ui}
{: ui}

_Talk about Creating, listing, updating, and deleting topics, Describing the cluster_
_Bring in information like suggested topic naming strategies_

From instance in the [**Catalog**](https://cloud.ibm.com/catalog/event-streams){: external}, navigate to **Topics** from the menu on the left.

From the **Topics page**, you can view the following information about your topics: 
**Name**, **Partitions**, **Retention time**, **Retention size**, **Cleanup policy**, and **Stream landing**.

To delete a topic, from the **Topics page**, click the three dots to the very right of the topic name and click **Delete this topic**. 



## Create a topic and select number of partitions by using the CLI 
{: #create_topic_cli}
{: step}
{: cli}

Run the [**ibmcloud es topic-create** command](docs/EventStreams?topic=EventStreams-cli_reference#ibmcloud_es) to create a new topic with one partition. For example:

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

You can use the CLI to create, list, update the configuration of, and delete topics. You can also use the CLI to view details about your cluster.

_Talk about Creating, listing, updating, and deleting topics, Describing the cluster_

_Bring in information like suggested topic naming strategies_

#### List a topic using the **ibmcloud es topics** command
{: #ibmcloud_es_topics_cli}

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

#### Update the configuration of a topic using the **ibmcloud es topic-update** command
{: #ibmcloud_es_topic_update_cli}

Update the configuration for a topic.

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

Display the details of the cluster, including the Kafka version.

```bash
ibmcloud es cluster [--json]
```
{: codeblock}

**Prerequisites**: None

**Command options**:

--json (optional)
:   Output format in JSON.


## Create a topic and select number of partitions by using the API
{: #create_topic_api}
{: step}
{: api}

**Which API should we focus on?**

You can create a Kafka topic by issuing a POST request to the /admin/topics path. The body of the request must contain a JSON document, for example:

    ```
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

The JSON document must contain a name attribute, specifying the name of the Kafka topic to create. The JSON may also specify the number of partitions to assign to the topic (using the partitions property). If the number of partitions is not specified then the topic will be created with a single partition.

You can also specify an optional configs object within the request. This allows the specification of the retentionMs property which controls how long (in milliseconds) Kafka will retain messages published to the topic. After this time elapses the messages will automatically be deleted to free space. Note that the value of the retentionMs property must be specified in a whole number of hours (e.g. multiples of 3600000).

Expected HTTP status codes:

* 202: Topic creation request was accepted.
* 400: Invalid request JSON.
* 403: Not authorized to create topic.
* 422: Semantically invalid request.

If the request to create a Kafka topic succeeds, HTTP status code 202 (Accepted) is returned. If the operation fails then a HTTP status code of 422 (Unprocessable Entity) is returned, and a JSON object containing additional information about the failure is returned as the body of the response.
Example

The REST endpoint for creating a Kafka topic can be exercised using the following snippet of curl. You will need to supply your own API key or token and specify the correct endpoint for ADMIN API.

    ```
    curl -i -X POST -H 'Accept: application/json' -H 'Content-Type: application/json' -H 'Authorization: Bearer ${TOKEN}' --data '{ "name": "newtopic", "partitions": 1}' ${ADMIN_URL}/admin/topics
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

## Create an IAM service credential by using the resource controller API
{: #create_credential_api}
{: step}
{: api}

## Produce data using the console
{: #produce_data_ui}
{: step}
{: ui}

You can produce data only using the [CLI]({#produce_data_cli}) or [API]({#produce_data_cli}).


## Produce data using the CLI
{: #produce_data_cli}
{: step}
{: cli}

_b. via CLI c. via API - support different languages - show Java library_

_Include connection details and sample code to connect to the event streams instance_

_Highlight the most important kafka settings for producers are here including delivery semantics, acknowledgements, number of retries, session timeout, heartbeat interval, rebalance strategy (JAVA API supports multiple strategies to reduce rebalance)_

## Produce data using the API
{: #produce_data_api}
{: step}
{: api}

_b. via CLI c. via API - support different languages - show Java library)_

_Include connection details and sample code to connect to the event streams instance_

_Highlight the most important kafka settings for producers are here including delivery semantics, acknowledgements, number of retries, session timeout, heartbeat interval, rebalance strategy (JAVA API supports multiple strategies to reduce rebalance)_

## Consume data using the console
{: #consume_data_ui}
{: step}
{: ui}

You cannot consume data by using the console. You can consume data only using the [CLI]({#consume_data_cli}) or [API]({#consume_data_cli}).

## Consume data using the CLI
{: #consume_data_cli}
{: step}
{: cli}

_a. UI Not available b. via CLI c. via API - support different languages - show Java library_

_Include connection details and sample code to connect to the event streams instance_

_Highlight the most important kafka settings for consumers are here including commit offsets, exactly once semantics, consumer groups and liveness_

## Consume data using the API 
{: #consume_data_api}
{: step}
{: api}

_a. UI Not available b. via CLI c. via API - support different languages - show Java library_

_Include connection details and sample code to connect to the event streams instance_

_Highlight the most important kafka settings for consumers are here including commit offsets, exactly once semantics, consumer groups and liveness_

## Connect IBM Cloud Monitoring for Operational Visibility by using the console 
{: #connect_monitoring}
{: step}
{: ui}

_(a. via UI only - walk through steps ), (Explain benefits)_

Use {{site.data.keyword.monitoringshort}} to gain operational visibility into the performance and health of your applications, services, and platforms. It offers administrators, DevOps teams, and developers full stack telemetry with advanced features to monitor and troubleshoot, define alerts, and design custom dashboards.
[Monitoring Event Streams metrics by using IBM Cloud Monitoring](/docs/EventStreams?topic=EventStreams-metrics).

You can only use the console for this capability.

## Connect {{site.data.keyword.cloudaccesstrailshort}} to audit service activity (using the console - walk through steps ), (Explain benefits)
{: #activity_tracker}
{: step}
{: ui}

{{site.data.keyword.at_full_notm}} can have only one instance per location. To view events, you must access the web UI of the {{site.data.keyword.at_full_notm}} service in the same location where your service instance is available. For more information, see [Launch the web UI](/docs/activity-tracker?topic=activity-tracker-getting-started#gs_step4){: external}.

[{{site.data.keyword.cloudaccesstrailshort}} events](/docs/EventStreams?topic=EventStreams-at_events)

## (Optional) Using Kafka Connect or kSQLdb
{: #kafka_connect_ksql}
{: step} 

_Link to additional docs page content, highlight that this is not part of the managed service_

Kafka Connect is part of the Apache Kafka project and allows you to connect external systems to Kafka. It consists of a runtime  that can run connectors to copy data to and from a cluster.
[Using Kafka Connect with Event Streams](/docs/EventStreams?topic=EventStreams-kafka_connect)

Kafka Connect is not part of the managed {{site.data.keyword.messagehub}} service.

You can use [KSQL](https://github.com/confluentinc/ksql){: external} with {{site.data.keyword.messagehub}} for stream processing. 
[Using ksqlDB with Event Streams](/docs/EventStreams?topic=EventStreams-ksql_using)



## Getting help
{: #getting_help}
{: step}

[Getting help and support](/docs/EventStreams?topic=EventStreams-gettinghelp)

[FAQs](/docs/EventStreams?topic=EventStreams-faqs) 

[Reporting a problem to the Event Streams team - Standard and Enterprise plans](/docs/EventStreams?topic=EventStreams-report_problem_enterprise)




For 
Info to gather if having a problem, Add suggestions for what they need to do if having a problem - or directly link to this page. Include links to FAQ page, Ticket info, slack channel?

