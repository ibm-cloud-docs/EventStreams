---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-04"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Connecting to {{site.data.keyword.messagehub}}
{: #connecting}

The way you connect to {{site.data.keyword.messagehub}} varies depending on whether you're using the Standard or Enterprise plan, and also whether you're connecting from a Cloud Foundry application or from any other external client. You need to collect two pieces of information to connect to any of {{site.data.keyword.messagehub}}'s APIs:

* The endpoint URLs for the APIs
* Credentials for authentication

Read the following information for how to obtain these details. The steps can vary subtly so ensure that you complete the appropriate steps for your instance.

## Provision an {{site.data.keyword.messagehub}} instance

As a prerequisite, you must first provision an {{site.data.keyword.messagehub}} service instance for either the Standard or Enterprise plan. Provisioning an {{site.data.keyword.messagehub}} instance might incur a charge. Next, obtain {{site.data.keyword.messagehub}} API connection details by completing the following tasks.

## Standard plan overview
{: #connect_standard}

Services that are provisioned using the Standard Plan are Cloud Foundry services. This means that they are deployed into a Cloud Foundry Organization and Space, and are grouped in the dashboard under the heading **Cloud Foundry Services**. The method you use to connect an application depends on where the application is deployed, that is in Cloud Foundry or outside it.


## Cloud Foundry applications on the Standard plan
{: #connect_standard_cf}

For apps running inside Cloud Foundry, bind your app to the {{site.data.keyword.messagehub}} service instance. When bound, the connection details are made available to the app in JSON format in the VCAP_SERVICES environment variable. You can bind an app and service using either the IBM Cloud console or the IBM Cloud CLI.

Here is an example of VCAP_SERVICES:

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


### Get credentials and connect using the IBM Cloud console
{: #connect_standard_cf_console }

1. Ensure that you're in the intended Cloud Foundry Organization and Space.
2. Locate your Cloud Foundry Application on the dashboard. If you don't yet have a Cloud Foundry application, you can create one by clicking the **Create resource** button.
3. Click your application tile.
4. Click **Connections**.
5. Click **Create Connection**.
6. Select the {{site.data.keyword.messagehub}} service tile that you want to bind to and click **Connect**. You might need to restage your application for the changes to take effect.
7. Click the **Runtime** tab on the left and select the **Environment variables** tab in the center. You can now verify your VCAP_SERVICES information and your application can now access this as environment variables. 


### Get credentials using the IBM Cloud CLI 
{: #connect_standard_cf_cli }

<ol>
<li>Ensure that you're in the intended Cloud Foundry Organization and Space. You can navigate interactively by running the following command:<br/>
<code>ibmcloud target -cf</code>
</li>
<li>Find your app:<br/> <code>ibmcloud app list</code> <br/>
</br>
If you have a manifest file, you can create a new app by running:</br>
<code>ibmcloud app push</code>
</li>
<li>Find your service:</br> 
<code>ibmcloud service list</code>
</li>
<li>Bind your app to the service:</br>
<code>ibmcloud service bind <var class="keyword varname">your_app_name</var> <var class="keyword varname">your_service_name</var></code>
</li>
<li>Verify that the VCAP_SERVICES environment variable is available in your application runtime by running:</br> 
 <code>ibmcloud app env <var class="keyword varname">your_app_name</var></code>. 
</li>
<li>Pass these credentials to your application. Specify <code>token</code> as your user name and the <var class="keyword varname">api_key</var> as your password. Separate <code>token</code> and the <var class="keyword varname">api_key</var> with a colon. For more information, see [Configuring your client](/docs/services/EventStreams/eventstreams063.html).
<p>You might need to restage your application for the changes to take effect.</p></li>
</ol>

## External applications on the Standard plan
{: #connect_standard_external}

For applications running outside Cloud Foundry, credentials are generated by creating a Service Key. When you have obtained a Service Key, manually pass the details of the key to your application using your chosen method.

### Get credentials using the IBM Cloud console
{: #connect_standard_external_console}

1. Ensure that you're in the intended Cloud Foundry Organization and Space.
2. Locate your Cloud Foundry {{site.data.keyword.messagehub}} service on the dashboard.
3. Click your service tile.
4. Click **Service Credentials**.
5. Click **New Credential**.
6. Enter the details for your new credential like a name and click **Add**. A new credential appears in the credentials list.
7. Click this credential using **View credentials** to reveal the details in JSON format.
8. Pass these credentials to your application. Specify <code>token</code> as your user name and the <var class="keyword varname">api_key</var> as your password. Separate <code>token</code> and the <var class="keyword varname">api_key</var> with a colon. For more information, see [Configuring your client](/docs/services/EventStreams/eventstreams063.html).

### Get credentials using the IBM Cloud CLI 
{: #connect_standard_external_cli }

<ol>
<li>Ensure that you're in the intended Cloud Foundry Organization and Space. You can navigate interactively by running the following command:<br>
<code>ibmcloud target -cf</code>
</li>
<li>Find your service:<br>
<code>ibmcloud service list</code>
</li>
<li>You can either create a service key:<br>
<code>ibmcloud service key-create <var class="keyword varname">your_service_name</var> <var class="keyword varname">new_service_key_name</var></code><br>
<br/>
or use an existing service key: <br/>
<code>ibmcloud service keys <var class="keyword varname">your_service_name</var></code> 
</li>
<li>Get the details for the key:</br>
<code>ibmcloud service key-show <var class="keyword varname">your_service_name</var> <var class="keyword varname">service _key_name</var></code></br>
This returns the service key details in JSON format.</li>
<li>Pass these credentials to your application. Specify <code>token</code> as your user name and the <var class="keyword varname">api_key</var> as your password. Separate <code>token</code> and the <var class="keyword varname">api_key</var> with a colon. For more information, see [Configuring your client](/docs/services/EventStreams/eventstreams063.html).</li>
</ol>

 
## Enterprise Plan overview
{: #connect_enterprise}

Services provisioned using the Enterprise Plan are grouped in the dashboard under the heading **Services**. The Enterprise plan is [IAM enabled ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/docs/iam/quickstart.html#getstarted){:new_window}. You don't need to understand IAM to get started but some knowledge is recommended if you want to secure your {{site.data.keyword.messagehub}} service. For more information, see 
[Securing your {{site.data.keyword.messagehub}} resources](/docs/services/EventStreams/eventstreams124.html)

Complete the following steps to bind your application and obtain Service Keys for your service. To be authorized to create topics, your application or Service Key must have a Manager access role.

To connect an application, the method used depends on where the application is deployed, that is in Cloud Foundry or outside it.

## Cloud Foundry applications on the Enterprise plan
{: #connect_enterprise_cf}

Your application must be bound to the {{site.data.keyword.messagehub}} service instance. To bind a Cloud Foundry application to a non-Cloud Foundry service with One Cloud, create a Cloud Foundry service alias first and then reference this alias from your Cloud Foundry application when binding.

When bound, the connection details are then made available to the application in JSON format using the VCAP_SERVICES environment variable. You can bind an application and service using either the IBM Cloud console or the IBM Cloud CLI.

### Bind an application using the IBM Cloud console
{: #connect_enterprise_cf_console}

1. Ensure that you're in the intended Cloud Foundry Organization and Space.
2. Locate your Cloud Foundry Application on the dashboard or create an application by clicking the **Create resource** button.
3. Click your application tile.
4. Click **Connections**.
5. Click **Create Connection**.
6. Select the {{site.data.keyword.messagehub}} service tile that you want to bind to and click **Connect**. 
7. In the **Connect IAM-Enabled Service** window that appears, select an access role from **Access Role for Connection** and a service ID from the **Service ID for Connection** list (you can accept the auto-generated ID). Click **Connect**. 

  This creates a Cloud Foundry service alias for your {{site.data.keyword.messagehub}} service and then binds your application to this alias. 

  Restage your application for the changes to take effect.<br/>
8. Click the **Runtime** tab on the left and select the **Environment variables** tab in the center. You can now verify your VCAP_SERVICES information. Your application can now access these as environment variables. 
 

### Bind an app using the IBM Cloud CLI
{: #connect_enterprise_cf_cli}

<ol>
<li>Ensure that you're in the intended Cloud Foundry Organization and Space. You can navigate interactively by running the following command:<br/>
 <code>ibmcloud target -cf</code></li>
<li>Locate your app:</br>
<code>ibmcloud app list</code><br/>
<br/>
If you have a manifest file, you can create a new app by running:<br/>
<code>ibmcloud app push</code><br/>
<br/>
Because the app is not bound to {{site.data.keyword.messagehub}} yet, the app cannot establish a connection. Therefore, you are recommended to push the application with the <code>--no-start</code> parameter to avoid unnecessary connection failures.</li>
<li>Locate your service:</br>
<code>ibmcloud resource service-instances</code></li>
<li>Create a Cloud Foundry service alias:<br/>
<code>ibmcloud resource service-alias-create <var class="keyword varname">alias_name</var> --instance-name <var class="keyword varname">your_service_name</var></code></li>
<li>Bind your app to the service alias created previously:<br/>
<code>ibmcloud service bind <var class="keyword varname">your_ app_name</var> <var class="keyword varname">alias_name</var></code>.<br/>
<br/>
Alternatively, you can update your manifest file and push the application again.</li>
<li>Verify that the VCAP_SERVICES environment variable is available in your application runtime:<br/>
<code>ibmcloud app env <var class="keyword varname">your_app_name</var></code></li>
<li>Pass these credentials to your application. Specify <code>token</code> as your user name and the <var class="keyword varname">api_key</var> as your password. Separate <code>token</code> and the <var class="keyword varname">api_key</var> with a colon. For more information, see [Configuring your client](/docs/services/EventStreams/eventstreams063.html). 
<p>You might need to restage your application for the changes to take effect.</p></li>
</ol>


## External applications on the Enterprise plan
{: #connect_enterprise_external}

For applications running outside Cloud Foundry, credentials are generated by creating a Service Key. When you obtain the Service Key, manually pass the details of the key to your application using your chosen method.

### Get credentials using the IBM Cloud console
{: #connect_enterprise_external_console}

1. Locate your {{site.data.keyword.messagehub}} service on the dashboard.
2. Click your service tile.
3. Click **Service Credentials**.
4. Click **New Credential**. 
5. Complete the details for your new credential like a name and role and click **Add**. A new credential appears in the credentials list.
6. Click this credential using **View Credentials** to reveal the details in JSON format.
7. Pass these credentials to your application. Specify <code>token</code> as your user name and the <var class="keyword varname">api_key</var> as your password. Separate <code>token</code> and the <var class="keyword varname">api_key</var> with a colon. For more information, see [Configuring your client](/docs/services/EventStreams/eventstreams063.html).
   <br/><br/>Ensure that your application parses the details.

### Get credentials using the IBM Cloud CLI
{: #connect_enterprise_external_cli}

<ol>
<li>Locate your service:<br/>
<code>ibmcloud resource service-instances</code></li>
<li>Create a Service Key:<br/>
<code>ibmcloud resource service-key-create <var class="keyword varname">key_name</var> <var class="keyword varname">key_role</var> --instance-name <var class="keyword varname">your_service_name</var></code></li>
<li>Print the Service Key:<br/>
<code>ibmcloud resource service-key <var class="keyword varname">key_name</var></code></li>
<li>Pass these credentials to your application. Specify <code>token</code> as your user name and the <var class="keyword varname">api_key</var> as your password. Separate <code>token</code> and the <var class="keyword varname">api_key</var> with a colon. For more information, see [Configuring your client](/docs/services/EventStreams/eventstreams063.html).
<p>Ensure that your application parses the details.</p></li>
</ol>

## What to do next
{: #after_connecting}

Now you have connection and credential information, you can choose an {{site.data.keyword.messagehub}} client. Your choice depends on your plan.

* If you're using the Standard plan, see 
[Choosing between the three APIs](/docs/services/EventStreams/eventstreams087.html) for information about which client to choose and how to connect.
* If you're using the Enterprise plan, see [Using the Kafka API](/docs/services/EventStreams/eventstreams050.html).

	The internal Kafka <code>__consumer_offsets</code> topic is visible to you as read-only 
	if you're using the Enterprise plan. You are strongly recommended not to attempt to manage the topic in any way. 

<!--
Charlie said:

"Add some info describing how to take the information made available from above e.g. like the info in the Connecting a client to the Kafka API section of the alpha docs on stage 1? https://console.stage1.bluemix.net/docs/services/EventStreams/eventstreams122.html#alpha_about "
-->







 










