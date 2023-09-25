---

copyright:
  years: 2023
lastupdated: "2023-08-21"

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

This tutorial guides you through how to start using {{site.data.keyword.messagehub}} by provisioning an instance, creating a topic and a credential then producing and consuming data. Additionally, you'll learn how to connect Cloud Monitoring and Activity Tracker and optionally how to use Kafka Connect or kSQLdb. Finally, you'll also find out how you can get help with {{site.data.keyword.messagehub}}.
{: shortdesc}

* [Prerequisites](#prereqs)
* [Step 1: Choose your plan](#choose_plan)
* [Step 2: Provision an {{site.data.keyword.messagehub}} instance](#provision_instance_ui)
* [Step 3: Create a topic](#create_topic) 
* [Step 4: Create an IAM service credential](#create_credential)
* [Step 5: Produce data](#produce_data)
* [Step 6: Consume data](#consume_data)
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

* The Enterprise plan offers pay as you go access to an isolated single-tenant {{site.data.keyword.messagehub}} service. It also offers customer managed encryption, private endpoints, and a selection of throughput and storage options. 

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
{: #create_topic}
{: step}
{: ui}

1. From your newly provisioned instance in the [**Catalog**](https://cloud.ibm.com/catalog/event-streams){: external}, navigate to **Topics** from the menu on the left.
2. Click the **Create topic** button and an enter a topic name. Click **Next**.
3. Select the number of partitions. Click **Next**.

    One or more partitions make up a topic. A partition is an ordered list of messages. 1 partition is sufficient for getting started, but production systems often have more.

    Partitions are distributed across the brokers in order to increase the scalability of your topic. You can also use them to distribute messages across the members of a consumer group.

    *Talk about Creating, listing, updating, and deleting topics, Describing the cluster.
    Bring in information like suggested topic naming strategies*

4. Set the message retention period. Click **Create topic**.

    This is how long messages are retained before they are deleted.

    If your messages are not read by a consumer within this time, they will be missed.

## Create a topic and select number of partitions by using the CLI 
{: #create_topic}
{: step}
{: cli}


_Talk about Creating, listing, updating, and deleting topics, Describing the cluster_
_Bring in information like suggested topic naming strategies_

## Create a topic and select number of partitions by using the API
{: #create_topic}
{: step}
{: api}

**Which API should we focus on?**

    Creating a Kafka topic

You can create a Kafka topic by issuing a POST request to the /admin/topics path. The body of the request must contain a JSON document, for example:

{
    "name": "topicname",
    "partitions": 1,
    "configs": {
        "retentionMs": 86400000,
        "cleanupPolicy": "delete"
    }
}

The JSON document must contain a name attribute, specifying the name of the Kafka topic to create. The JSON may also specify the number of partitions to assign to the topic (using the partitions property). If the number of partitions is not specified then the topic will be created with a single partition.

You can also specify an optional configs object within the request. This allows the specification of the retentionMs property which controls how long (in milliseconds) Kafka will retain messages published to the topic. After this time elapses the messages will automatically be deleted to free space. Note that the value of the retentionMs property must be specified in a whole number of hours (e.g. multiples of 3600000).

Expected HTTP status codes:

    202: Topic creation request was accepted.
    400: Invalid request JSON.
    403: Not authorized to create topic.
    422: Semantically invalid request.

If the request to create a Kafka topic succeeds then HTTP status code 202 (Accepted) is returned. If the operation fails then a HTTP status code of 422 (Unprocessable Entity) is returned, and a JSON object containing additional information about the failure is returned as the body of the response.
Example

The REST endpoint for creating a Kafka topic can be exercised using the following snippet of curl. You will need to supply your own API key or token and specify the correct endpoint for ADMIN API.

    ```
    curl -i -X POST -H 'Accept: application/json' -H 'Content-Type: application/json' -H 'Authorization: Bearer ${TOKEN}' --data '{ "name": "newtopic", "partitions": 1}' ${ADMIN_URL}/admin/topics
    ```
    {: codeblock}

_Talk about Creating, listing, updating, and deleting topics, Describing the cluster._
_Bring in information like suggested topic naming strategies_

## Create an IAM service credential by using the console
{: #create_credential}
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
{: #create_credential}
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
{: #create_credential}
{: step}
{: api}

## Produce data
{: #produce_data}
{: step}

    (a. UI Not available b. via CLI c. via API - support different languages - show Java library)

    Include connection details and sample code to connect to the event streams instance

    Highlight the most important kafka settings for producers are here including delivery semantics, acknowledgements, number of retries, session timeout, heartbeat interval, rebalance strategy (JAVA API supports multiple strategies to reduce rebalance)

## Consume data (a. UI Not available b. via CLI - support different languages - show Java library)
{: #consume_data}
{: step}
{: cli}

    (a. UI Not available b. via CLI c. via API - support different languages - show Java library)

    Include connection details and sample code to connect to the event streams instance

    Highlight the most important kafka settings for consumers are here including commit offsets, exactly once semantics, consumer groups and liveness,

## Consume data (a. UI Not available - support different languages - show Java library)
{: #consume_data}
{: step}
{: api}

    (a. UI Not available b. via CLI c. via API - support different languages - show Java library)

    Include connection details and sample code to connect to the event streams instance

    Highlight the most important kafka settings for consumers are here including commit offsets, exactly once semantics, consumer groups and liveness,

## Connect IBM Cloud Monitoring for Operational Visibility by using the console (a. via UI only - walk through steps ), (Explain benefits)
{: #connect_monitoring}
{: step}

Use {{site.data.keyword.monitoringshort}} to gain operational visibility into the performance and health of your applications, services, and platforms. It offers administrators, DevOps teams, and developers full stack telemetry with advanced features to monitor and troubleshoot, define alerts, and design custom dashboards.
[Monitoring Event Streams metrics by using IBM Cloud Monitoring](/docs/EventStreams?topic=EventStreams-metrics)

## Connect {{site.data.keyword.cloudaccesstrailshort}} to audit service activity (using the console - walk through steps ), (Explain benefits)
{: #activity_tracker}
{: step}

{{site.data.keyword.at_full_notm}} can have only one instance per location. To view events, you must access the web UI of the {{site.data.keyword.at_full_notm}} service in the same location where your service instance is available. For more information, see [Launch the web UI](/docs/activity-tracker?topic=activity-tracker-getting-started#gs_step4){: external}.

[{{site.data.keyword.cloudaccesstrailshort}} events](/docs/EventStreams?topic=EventStreams-at_events)

## (Optional) Using Kafka Connect or kSQLdb
{: #kafka_connect_ksql}
{: step} 

Link to additional docs page content, highlight that this is not part of the managed service

Kafka Connect is part of the Apache Kafka project and allows connecting external systems to Kafka. It consists of a runtime  that can run connectors to copy data to and from a cluster.
[Using Kafka Connect with Event Streams](/docs/EventStreams?topic=EventStreams-kafka_connect)

You can use [KSQL](https://github.com/confluentinc/ksql){: external} with {{site.data.keyword.messagehub}} for stream processing. 
[Using ksqlDB with Event Streams](/docs/EventStreams?topic=EventStreams-ksql_using)



## Help section.
{: #getting_help}
{: step}

[Getting help and support](/docs/EventStreams?topic=EventStreams-gettinghelp)

[FAQs](/docs/EventStreams?topic=EventStreams-faqs) 

[Reporting a problem to the Event Streams team - Standard and Enterprise plans](/docs/EventStreams?topic=EventStreams-report_problem_enterprise)




For 
Info to gather if having a problem, Add suggestions for what they need to do if having a problem - or directly link to this page. Include links to FAQ page, Ticket info, slack channel?

-------------------------------------------------------

To understand more about how {{site.data.keyword.messagehub}} works, see [{{site.data.keyword.messagehub}} overview](/docs/EventStreams?topic=EventStreams-about). 

To access {{site.data.keyword.messagehub}} samples, see our primary sample repository at [{{site.data.keyword.messagehub}} samples](https://github.com/IBM/eventstreams-samples){: external}.  Other {{site.data.keyword.messagehub}} samples, including samples for Node.js and Python, are available at the previous [{{site.data.keyword.messagehub}} repository](https://github.com/ibm-messaging/event-streams-samples){: external}.

![Get started with {{site.data.keyword.messagehub_full}}](https://video.ibm.com/embed/channel/23952663/video/event-streams-intro){: video output="iframe" data-script="none" id="youtubeplayer" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen}

## Prerequisites backup
{: #getting_started_prereqs1}

1. **If you don't already have one, create an {{site.data.keyword.messagehub}} service instance.**

   a. Log in to the {{site.data.keyword.cloud_notm}} console.
  
   b. Click the [**{{site.data.keyword.messagehub}} service**](https://cloud.ibm.com/catalog/event-streams){: external} in the **Catalog**.
  
   c. Select the **Lite plan** on the service instance page.
  
   d. Enter a name for your service. You can use the default value.
  
   e. Click **Create**. The {{site.data.keyword.messagehub}} **Getting started** page opens. 

2. **If you don't already have them, install the following prerequisites:**
	
	- [Git](https://git-scm.com/){: external}
	- Java™  8 or higher 

## Tutorial steps
{: #getting_started_steps}

1. In the {{site.data.keyword.cloud_notm}} console (UI), go to your **Resource list**, select your {{site.data.keyword.messagehub}} resource, and click the **Get started with a sample application** tile.

2. Complete the **Configure and run starter application** steps:

     a. Click the **Download .JAR from GitHub** button to download the latest .JAR release. 
     
     b. Click the **Generate properties** button to generate and download the properties file. The **Topic** panel opens.
     
     c. Enter a name for a **New topic** that you want to create. Or, click **Existing topic** to select an existing topic that you want to use. 
     
     If you are on the Lite plan and a topic already exists, the **New topic** button is disabled. {: note}
     
     d. Select the **Service credential** that you want to use, or select **Create new** to create a new one. 
     
     e. Click the **Generate and download** button. The `kafka.properties` file is downloaded to your local machine. It contains the necessary configuration to connect to {{site.data.keyword.messagehub}}. You can open it in a text editor to see how it works.
     
     f. The panel shows your selected configuration. Clicking the **Regenerate** button starts the process again. Clicking the **Download** button downloads the properties file again.
     
3. Navigate to the folder that contains the downloaded .JAR file by using the command line or a terminal and run the command. Replace the value `<path-to-properties>` with the file path to the `kafka.properties` file.

4. When the application starts, click the **localhost:8080** link to open the starter app and see messages flowing through the topic.

## Next steps
{: #next_steps}

Now that you ran the starter application, you can try other [{{site.data.keyword.messagehub}} samples](https://github.com/ibm-messaging/event-streams-samples){: external}. Explore [other ways to connect](/docs/EventStreams?topic=EventStreams-kafka_connect){: external} to the {{site.data.keyword.messagehub}} service or find out more about 
[{{site.data.keyword.messagehub}} on {{site.data.keyword.satellitelong_notm}}](/docs/EventStreams?topic=EventStreams-satellite_about){: external}, a hybrid environment that combines public cloud services running in your secure private cloud.

To watch a video that walks you through getting a Java sample to run, see [Getting started with IBM {{site.data.keyword.messagehub}}](https://www.youtube.com/watch?v=XyNy7TcfJOc).{: external}