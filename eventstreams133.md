---

copyright:
  years: 2015, 2019
lastupdated: "2019-08-15"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Getting started with the {{site.data.keyword.messagehub}} CLI 
{: #cli}

To install and set up the {{site.data.keyword.messagehub}} CLI on the Lite, Standard, and Enterprise plans, complete the following steps:

## Step 1. Install the {{site.data.keyword.Bluemix_notm}} CLI
{: #step1_install_cli}

For information about how to install the CLI, see [Getting started with the {{site.data.keyword.Bluemix_notm}} CLI](/docs/cli?topic=cloud-cli-getting-started){:new_window}.

## Step 2. Log in to {{site.data.keyword.Bluemix_notm}} 
{: #step2_login}

Run the following command to log in to {{site.data.keyword.Bluemix_notm}}:
```
ibmcloud login -a cloud.ibm.com
```
{: codeblock}


## Step 3. Create an {{site.data.keyword.messagehub}} instance
{: #step3_es_instance}

Create an {{site.data.keyword.messagehub}} instance on {{site.data.keyword.Bluemix_notm}} using the Lite, Standard, or Enterprise plans. (The Classic plan does not support the CLI.) <br/>
Select one of the following methods:

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

## Step 4. Create a service API key for this instance
{: #step4_es_api}

The valid ROLE_NAMEs are: Manager, Writer, and Reader. Their permissions are described in [Managing access to your {{site.data.keyword.messagehub}} resources ](/docs/services/EventStreams?topic=eventstreams-security#security).

* To create an API key from the {{site.data.keyword.Bluemix_notm}} console, enter the Service credentials from the instance page, and click **New Credentials**.

* To create an API key from the CLI, run this command:
  ```
  ibmcloud resource service-key-create <KEY_NAME> <ROLE_NAME> --instance-name <INSTANCE_NAME>
  ```
  {: codeblock}

## Step 5. Install the {{site.data.keyword.messagehub}} CLI plugin
{: #step5_es_cli}

Run the following command:
```
ibmcloud plugin install event-streams
```
{: codeblock}

## Step 6. Initialize the {{site.data.keyword.messagehub}} plugin
{: #step6_es_init}

Before you can run any of the {{site.data.keyword.messagehub}} CLI commands, you must first initialize the plugin. Run the following command then select your {{site.data.keyword.messagehub}} instance:

```
ibmcloud es init
```
{: codeblock}

<br/>
For information about the {{site.data.keyword.messagehub}} CLI commands, see [CLI reference](/docs/services/EventStreams?topic=eventstreams-cli_reference#cli_reference).










