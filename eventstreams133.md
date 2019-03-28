---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-28j"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Using the {{site.data.keyword.messagehub}} CLI (Enterprise and Standard+ plans)
{: #cli}

To install and set up the  {{site.data.keyword.messagehub}} CLI on the Enterprise and Standard+ plans, complete the following steps:

1. Install the IBM Cloud CLI. For more information, see [Getting started with the {{site.data.keyword.Bluemix_notm}} CLI](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli){:new_window}.

2. Run the following command to log in to {{site.data.keyword.Bluemix_notm}}:
    ```
    ibmcloud login -a cloud.ibm.com
    ```
    {: pre}

3. Create an {{site.data.keyword.messagehub}} instance on {{site.data.keyword.Bluemix_notm}} using the Enterprise or Standard+ plans. (The CLI does not support the deprecated Standard plan.) Select one of the following methods:

    * To create an instance from the IBM Cloud console, enter this URL in a browser: https://cloud.ibm.com/catalog/services/event-streams

    * To create an instance from the CLI on the Enterprise plan, run the following command:
    ```
    ibmcloud resource service-instance-create 
    <var class="keyword varname">INSTANCE_NAME</var> messagehub 
    ibm.message.hub.enterprise.3nodes.2tb <var class="keyword varname">REGION</var>
    ```
    
    Because Enterprise has its own dedicated resources for each cluster, it requires more time for provisioning, so a new Enterprise instance might take up to 3 hours.
    
    * To create an instance from the CLI on the Standard+ plan, run the following command:

    <pre class="pre">
    ibmcloud resource service-instance-create
    <var class="keyword varname">INSTANCE_NAME</var> messagehub ibm.message.hub.standard.v2
    <var class="keyword varname">REGION</var>
    </pre>
    Provisioning a new Standard+ instance is instantaneous.
    
4. Create a service API key for this instance. 
<br/>
The valid ROLE_NAMEs are: Manager, Writer, and Reader. Their permissions are described in [Managing access to your {{site.data.keyword.messagehub}} resources ](/docs/services/EventStreams?topic=eventstreams-security#security)

    * To create an API key from the IBM Cloud console, enter the Service credentials from the instance page, and click **New Credentials**.

    * To create an API key from the CLI, run this command:
    <pre class="pre">
    ibmcloud resource service-key-create <var class="keyword varname">KEY_NAME</var> <var class="keyword varname">ROLE_NAME</var>
    --instance-name
    <var class="keyword varname">INSTANCE_NAME</var>
    </pre>
5. Install the {{site.data.keyword.messagehub}} CLI plugin, by running this command:
    ```
    ibmcloud plugin install event-streams
    ```
    {: codeblock}

<br/>
For information about the {{site.data.keyword.messagehub}} CLI commands, see [CLI reference for the Enterprise and Standard+ plans](/docs/services/EventStreams?topic=eventstreams-cli_reference#cli_reference).
 

 test
 ```
  ibmcloud target -o <value> -s <value>
  ```
  {: codeblock}






