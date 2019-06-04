---

copyright:
  years: 2015, 2019
lastupdated: "2018-11-07"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Connecting to {{site.data.keyword.messagehub}} using the Classic plan 
{: #connecting_classic}

The way you connect to {{site.data.keyword.messagehub}} varies depending on whether you're connecting from a Cloud Foundry application or from any other external client. You need to collect two pieces of information to connect to any of {{site.data.keyword.messagehub}}'s APIs:
{: shortdesc}

* The endpoint URLs for the APIs
* Credentials for authentication

Read the following information for how to obtain these details. The steps can vary subtly so ensure that you complete the appropriate steps for your instance.

## Provision an {{site.data.keyword.messagehub}} instance
{: #provision_classic}

As a prerequisite, you must first provision an {{site.data.keyword.messagehub}} service instance for the Classic plan. Next, obtain {{site.data.keyword.messagehub}} API connection details by completing the following tasks.

## Classic plan overview
{: #connect_classic_plan}

Services that are provisioned using the Classic Plan are Cloud Foundry services. This means that they are deployed into a Cloud Foundry Organization and Space, and are grouped in the dashboard under the heading **Cloud Foundry Services**. The method you use to connect an application depends on where the application is deployed, that is in Cloud Foundry or deployed outside Cloud Foundry, for example in the Kubernetes Service.


## Cloud Foundry applications on the Classic plan
{: #connect_classic_cf_plan}

For apps running inside Cloud Foundry, bind your app to the {{site.data.keyword.messagehub}} service instance. When bound, the connection details are made available to the app in JSON format in the VCAP_SERVICES environment variable. You can bind an app and service using either the IBM Cloud console or the IBM Cloud CLI.

Here is an example of VCAP_SERVICES:

```
{
  "credentials": {
    "mqlight_lookup_url": "https://mqlight-lookup.messagehub.services.us-south.bluemix.net/Lookup?serviceId=584e8436-e7f5-43db-96ac-2864fccae5ae",
    "api_key": <YOUR_API_KEY>,
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
{: #connect_classic_plan_cf_console }

1. Ensure that you're in the intended Cloud Foundry Organization and Space.
2. Locate your Cloud Foundry Application on the dashboard. If you don't yet have a Cloud Foundry application, you can create one by clicking the **Create resource** button.
3. Click your application tile.
4. Click **Connections**.
5. Click **Create Connection**.
6. Select the {{site.data.keyword.messagehub}} service tile that you want to bind to and click **Connect**. You might need to restage your application for the changes to take effect.
7. Click the **Runtime** tab on the left and select the **Environment variables** tab in the center. You can now verify your VCAP_SERVICES information and your application can now access this as environment variables. 


### Get credentials using the IBM Cloud CLI 
{: #connect_classic_plan_cf_cli }

<ol>
<li>Ensure that you're in the intended Cloud Foundry Organization and Space. You can navigate interactively by running the following command:<br/>
<code>ibmcloud target --cf</code>
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
<li>Pass these credentials to your application. Specify <code>token</code> as your user name and the <var class="keyword varname">api_key</var> as your password. Separate <code>token</code> and the <var class="keyword varname">api_key</var> with a colon. For more information, see [Configuring your client](/docs/services/EventStreams?topic=eventstreams-kafka_connect).
<p>You might need to restage your application for the changes to take effect.</p></li>
</ol>

## External applications on the Classic  plan
{: #connect_classic_plan_external}

For applications running outside Cloud Foundry, credentials are generated by creating a Service Key. When you have obtained a Service Key, manually pass the details of the key to your application using your chosen method.

### Get credentials using the IBM Cloud console
{: #connect_classic_plan_external_console}

1. Ensure that you're in the intended Cloud Foundry Organization and Space.
2. Locate your Cloud Foundry {{site.data.keyword.messagehub}} service on the dashboard.
3. Click your service tile.
4. Click **Service Credentials**.
5. Click **New Credential**.
6. Enter the details for your new credential like a name and click **Add**. A new credential appears in the credentials list.
7. Click this credential using **View credentials** to reveal the details in JSON format.
8. Pass these credentials to your application. Specify <code>token</code> as your user name and the <var class="keyword varname">api_key</var> as your password. Separate <code>token</code> and the <var class="keyword varname">api_key</var> with a colon. For more information, see [Configuring your client](/docs/services/EventStreams?topic=eventstreams-kafka_connect).

### Get credentials using the IBM Cloud CLI 
{: #connect_classic_plan_external_cli }

<ol>
<li>Ensure that you're in the intended Cloud Foundry Organization and Space. You can navigate interactively by running the following command:<br>
<code>ibmcloud target --cf</code>
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
<li>Pass these credentials to your application. Specify <code>token</code> as your user name and the <var class="keyword varname">api_key</var> as your password. Separate <code>token</code> and the <var class="keyword varname">api_key</var> with a colon. For more information, see [Configuring your client](/docs/services/EventStreams?topic=eventstreams-kafka_connect).</li>
</ol>
 
## What to do next
{: #after_connecting_next}

Now you have connection and credential information, you can choose an {{site.data.keyword.messagehub}} client. See 
[Choosing between the three APIs](/docs/services/EventStreams?topic=eventstreams-choose_api_classic) for information about which client to choose and how to connect.










 










