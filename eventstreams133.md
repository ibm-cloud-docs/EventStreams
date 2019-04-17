---

copyright:
  years: 2015, 2019
lastupdated: "2019-04-17f"

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

To install and set up the {{site.data.keyword.messagehub}} CLI on the Standard and Enterprise plans, complete the following steps:

1. Install the {{site.data.keyword.Bluemix_notm}} CLI. For more information, see [Getting started with the {{site.data.keyword.Bluemix_notm}} CLI](/docs/cli?topic=cloud-cli-ibmcloud-cli#ibmcloud-cli){:new_window}.

2. Run the following command to log in to {{site.data.keyword.Bluemix_notm}}:
    ```
    ibmcloud login -a cloud.ibm.com
    ```
    {: codeblock}

3. Create an {{site.data.keyword.messagehub}} instance on {{site.data.keyword.Bluemix_notm}} using the Enterprise or Standard plans. (The Classic plan does not support the CLI.) 
Select one of the following methods:

  ## {{site.data.keyword.Bluemix_notm}} console
  To create an instance from the {{site.data.keyword.Bluemix_notm}} console, go to the {{site.data.keyword.messagehub}} entry in the
  [catalog ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/catalog/services/event-streams){:new_window}.

  ## CLI on the Enterprise plan
  To create an instance from the CLI on the Enterprise plan, run a command like the following:
    ```
   ibmcloud resource service-instance-create <INSTANCE_NAME> <SERVICE_NAME> <SERVICE_PLAN> <REGION>
    ```
   {: codeblock}
    
    Because Enterprise has its own dedicated resources for each cluster, it requires more time for provisioning so a new Enterprise instance might take up to 3 hours.

  ## CLI on the Standard plan    
  To create an instance from the CLI on the Standard plan, run the following command:

  ```
  ibmcloud resource service-instance-create <INSTANCE_NAME> <SERVICE_NAME> <SERVICE_PLAN> <REGION>
    ```
    {: codeblock}

    Provisioning a new Standard instance is instantaneous because the underlying resources are already set up.

      ```
    curl -sL https://ibm.biz/idt-installer | bash
    ```
    {: codeblock}
    
4. Create a service API key for this instance. 
<br/>
The valid ROLE_NAMEs are: Manager, Writer, and Reader. Their permissions are described in [Managing access to your {{site.data.keyword.messagehub}} resources ](/docs/services/EventStreams?topic=eventstreams-security#security)

    * To create an API key from the IBM Cloud console, enter the Service credentials from the instance page, and click **New Credentials**.

    * To create an API key from the CLI, run this command:
  ```
  ibmcloud resource service-key-create <KEY_NAME> <ROLE_NAME> --instance-name <INSTANCE_NAME>
```
 {: codeblock}

5. Install the {{site.data.keyword.messagehub}} CLI plugin, by running this command:
    ```
    ibmcloud plugin install event-streams
    ```
    {: codeblock}

<br/>
For information about the {{site.data.keyword.messagehub}} CLI commands, see [CLI reference](/docs/services/EventStreams?topic=eventstreams-cli_reference#cli_reference).


## Step 1. Run the installation command
{: #step1-install-idt}

* For Mac and Linux, run the following command:
  ```
  curl -sL https://ibm.biz/idt-installer | bash
  ```
  {: codeblock}

* For Windows 10 Pro, run the following command as an administrator:
  ```
  Set-ExecutionPolicy Unrestricted; iex(New-Object Net.WebClient).DownloadString('http://ibm.biz/idt-win-installer')
  ```
  {: codeblock}

  ```
  ibmcloud resource service-instance-create <INSTANCE_NAME> <SERVICE_NAME> <SERVICE_PLAN> <REGION>
    ```
  {: codeblock}

  Right-click the Windows PowerShell icon, and select **Run as administrator**.
  {: tip}






