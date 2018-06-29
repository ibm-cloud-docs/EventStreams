---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-29"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Connecting to Message Hub
{: #connect_messagehub}

How you connect to your cluster varies according to whether you're using the Standard or Enterprise plan, and also whether you're connecting from a Cloud Foundry application or from any other external client. You need to collect two pieces of information to connect to any of our APIs:

* The endpoint URLs for the APIs
* Credentials for authentication

Read the following information for how to obtain these details. The steps can vary subtly and you should follow the appropriate steps below for your instance.

## Provision a Message Hub instance

As a prerequisite, you must first provision a Message Hub service instance for either the Standard or Enterprise plan. Provisioning a Message Hub instance might incur a charge. Next, obtain Message Hub API connection details by completing the following tasks:

## Standard plan
{: #connect_standard}

Services that are provisioned using the Standard Plan are Cloud Foundry services. This means that they are deployed into a Cloud Foundry organization and space, and are grouped in the dashboard under the heading **Cloud Foundry Services**. The method you use to connect an application depends on where the application is deployed.


### Cloud Foundry applications
{: #connect_standard_cf}

For applications running inside Cloud Foundry, bind your application to the Message Hub service instance. When bound, the connection details are then made available to the application in JSON format in the VCAP_SERVICES environment variable. You can bind an application and service using either the IBM Cloud console or the IBM Cloud CLI.

Here is an example:

```
{
  "credentials": {
    "mqlight_lookup_url": "https://mqlight-lookup.messagehub.services.us-south.bluemix.net/Lookup?serviceId=584e8436-e7f5-43db-96ac-2864fccae5ae",
    "api_key": "d9JSx1SYsmLzNRbbgUFneDm2DtkedlVeViObYJIvrPAf2kJA",
    "kafka_admin_url": "https://kafka-admin.messagehub.services.us-south.bluemix.net:443",
    "kafka_rest_url": "https://kafka-rest.messagehub.services.us-south.bluemix.net:443",
    "kafka_brokers_sasl": [
      "kafka01.messagehub.services.us-south.bluemix.net:9093",
      "kafka02.messagehub.services.us-south.bluemix.net:9093",
      "kafka03.messagehub.services.us-south.bluemix.net:9093",
      "kafka04.messagehub.services.us-south.bluemix.net:9093",
      "kafka05.messagehub.services.us-south.bluemix.net:9093"
    ],
    "user": "d9JSx1SYsmLzNRbb",
    "password": "gUFneDm2DtkedlVeViObYJIvrPAf2kJA"
  }
}
```

{: codeblock}

The environment variable's content is the same, regardless of the API that you use to connect to {{site.data.keyword.messagehub}}. Your {{site.data.keyword.Bluemix_notm}} app selects the appropriate credentials from the VCAP_SERVICES environment variable, depending on the interface in
 use.
 
Only your first five brokers are listed in VCAP_SERVICES. If you have more than five brokers, use a Kafka client to retrieve the details of your other brokers. 


#### IBM Cloud console

1. Ensure that you're in the intended Cloud Foundry organization and space.
2. Locate your Cloud Foundry Application on the Dashboard. If you don't yet have a Cloud Foundry application, you can create one by clicking the **Create Resource** button.
3. Click your application tile.
4. Select **Connections**.
5. Click **Create Connection**.
6. Select the Message Hub service tile you would like to bind to and click **Connect**. You might need to restage your application for the changes to take effect.
7. Click the **Runtime** tab on the left and select the **Environment variables** tab in the center. You can now verify your VCAP_SERVICES information. 

	Your app can now access these as environment variables. 

#### IBM Cloud CLI test1

<ol>
<li>Ensure that you're in the intended Cloud Foundry organization and space. You can navigate interactively by running the following command: 
<code>ibmcloud target -cf</code>
</li>
<li>Find your app by running the following command: ```ibmcloud app list```.
<p>If you have a manifest file, you can create a new app by running <code>ibmcloud app push</code></p>
</li>
<li>Find your service: 
<code>ibmcloud service list</code>
</li>
<li>Bind your app to the service:
<code>ibmcloud service bind <var class="keyword varname">your_app_name</var> <var class="keyword varname">your_service_name</var></code>
</li>
<li>Verify that the VCAP_SERVICES environment variable is available in your application runtime. You can do this by calling 
<code>ibmcloud app env <var class="keyword varname">your app name</var></code>. 
</li>
<li>Pass these credentials to your application.
<p>You might need to restage your application for the changes to take effect.</p></li>
</ol>

### External applications on Standard plan
{: #connect_standard_external}

For applications running outside Cloud Foundry, credentials are generated by creating a Service Key. When you have obtained a Service Key, manually pass the details of the key to your application using your chosen method.

#### IBM Cloud console

1. Ensure that you're in the intended Cloud Foundry organization and space.
2. Locate your Cloud Foundry Message Hub service on the Dashboard.
3. Click on your service tile.
4. Select **Service Credentials**.
5. Click **New Credential**.
6. Enter the details for your new credential such as name and click **Add**. A new credential appears in the credentials list.
7. By clicking on this credential (**View credential**), the details are revealed in JSON format.
8. Pass these credentials to your application.

#### IBM Cloud CLI test2

<ol>
<li>Ensure that you're in the intended Cloud Foundry organization and space. You can navigate interactively by running the following command:<br>
<code>ibmcloud target -cf</code>
</li>
<li>Find your service:<br>
<code>ibmcloud service list</code>
</li>
<li>You can either create a service key as follows:<br>
<code>ibmcloud service key-create <var class="keyword varname">your service's name</var> <var class="keyword varname">name of new service key</var></code><br>
or or use an existing service key with the following command: 
<code>ibmcloud service keys <var class="keyword varname">your service's name</var></code> <code>ibmcloud service key-show <var class="keyword varname">your service's name</var> <var class="keyword varname">name of service key</var><code>
This returns the service key details in JSON format.</li>
<li>Pass these credentials to your application. </li>
</ol>


## Enterprise Plan
{: #connect_enterprise}

Services provisioned using the Enterprise Plan are grouped in the dashboard under the heading **Services**. The Enterprise plan is IAM enabled (https://console.bluemix.net/docs/iam/quickstart.html#getstarted). You don't need to understand IAM to get started but some knowledge is recommended, if you want to secure your Message Hub service https://console.bluemix.net/docs/services/MessageHub/messagehub124.html#security.

Complete the following steps to bind your application and obtain Service Keys for your service. To be authorized to create topics, your application or Service Key has to have a Manager access role.

To connect an application, the method used depends on where the application is deployed.

### Cloud Foundry applications

Your application must be bound to the Message Hub service instance. To bind a Cloud Foundry Application to a non-Cloud Foundry Service with One Cloud, create a Cloud Foundry Service Alias first and then reference this alias from your Cloud Foundry Application when binding.

When bound, the connection details are then made available to the application in JSON format using the VCAP_SERVICES environment variable. You can bind an application and service using either the IBM Cloud console or the IBM Cloud CLI.

#### IBM Cloud console

1. Ensure that you're in the intended Cloud Foundry organization and space.
2. Locate your Cloud Foundry Application on the Dashboard or create an application by clicking the **Create Resource** button.
3. Click your application tile.
4. Select **Connections**.
5. Click **Create Connection**.
6. Select the Message Hub service tile that you want to bind to and click **Connect**.
7. The previous step creates a Cloud Foundry Service Alias for your Message Hub service and then binds your application to this alias. On the IBM Cloud console, this happens automatically but on the IBM Cloud CLI, this is a required separate manual step. You might need to restage your application for the changes to take effect.
8. Click the **Runtime** tab on the left and select the **Environment variables** tab in the center. You can now verify your VCAP_SERVICES information. Your app can now access these as environment variables. 
 

#### IBM Cloud CLI

1. Ensure that you're in the intended Cloud Foundry organization and space. You can navigate interactively by running the following command: ```ibmcloud target -cf```
2. Locate your app by running the following command: ```ibmcloud app list```. If you have a manifest file, you can create a new app by running: ```ibmcloud app push```. Because the app is not bound to Message Hub yet, the app cannot to establish a connection. Therefore, you are recommended to push the application with the ```--no-start``` parameter to avoid unnecessary connection failures.
3. Locate your service using the following command: ```ibmcloud resource service-instances```
4. Create a Cloud Foundry Service Alias: ```ibmcloud resource service-alias-create <var class="keyword varname">alias_name</var> --instance-name <var class="keyword varname">your service's name</var>```
5. Bind your app to the Service Alias created above: ```ibmcloud service bind <var class="keyword varname">your app's name</var> <var class="keyword varname">alias_name</var>```. Alternatively you can update your manifest file and push the application again.
6. Verify that the VCAP_SERVICES environment variable is available in your application runtime. You can do this by running the following command:  ```ibmcloud app env <var class="keyword varname">your app's name</var>```. 
7. Pass these credentials to your application.<br/>

You might need to restage your application for the changes to take effect.

### External applications on Enterprise plan
{: #connect_enterprise_external}

For applications running outside Cloud Foundry, credentials are generated by creating a Service Key. When you obtain the Service Key, manually pass the details of the key to your application using your chosen method.

#### IBM Cloud console

1. Locate your Message Hub service on the Dashboard.
2. Click your service tile.
3. Select **Service Credentials**.
4. Click **New Credential**. 
5. Complete the details for your new credential such as name, role and click **Add**. A new credential appears in the credentials list.
6. By clicking on this credential (**View Credential**), the details are revealed in JSON format.
7. Pass these credentials to your application. Ensure your application parses the details.

#### IBM Cloud CLI

1. Locate your service: ```ibmcloud resource service-instances```
2. Create a Service Key: ```ibmcloud resource service-key-create <var class="keyword varname">key_name</var> <var class="keyword varname">key_role</var> --instance-name <var class="keyword varname">your_service_name</var>```
3. Print the Service Key: ```ibmcloud resource service-key <var class="keyword varname">key_name</var>```
4. Pass these credentials to your application. Make sure your application parses the details.


### What to do next
Pick client



Charlie said:

"Add some info describing how to take the information made available from above e.g. like the info in the Connecting a client to the Kafka API section of the alpha docs on stage 1? https://console.stage1.bluemix.net/docs/services/MessageHub/messagehub122.html#alpha_about "

















-------------------------------------------------------------------

## {{site.data.keyword.messagehub}} Enterprise plan
{: #connect_old notoc}


To connect to an API in the cluster you need its endpoint URL and an apikey for authentication. You can retrieve these details from IAM using one of the following methods:

### Cloud Foundry application
For a Cloud Foundry application:
1. In the **Connections** tab for the app (on the left), click the **Create connection** button. 
2. Select the instance of the {{site.data.keyword.messagehub}} service that you want to connect to and click **Connect**. Accept the default options. 
3. When the connection is complete, click the **Runtime** tab for the app, then click **Environment variables** to show **VCAP_SERVICES**.

### Console for an external application
From the console for an external application, create a service apikey by using the following **ibmcloud** command: 

```
ibmcloud resource service-key-create name-of-key Manager --instance-name name-of-your-service
``` 

Copy the <code>kafka_brokers_sasl</code>, <code>kafka_admin_url</code>, and <code>apikey</code> fields from the generated information.
Only your first five brokers are listed in VCAP_SERVICES. If you have more than five brokers, use a Kafka client to retrieve the details of your other brokers. 










