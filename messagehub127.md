---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Connecting to your cluster
{: #dedicated}

How you connect to your cluster varies according to whether you're using the Standard or Enterprise plan.

## {{site.data.keyword.messagehub}} Standard plan 
{: #vcap}

When your application is bound to the {{site.data.keyword.messagehub}} service, details of the service are stored
in JSON format in the VCAP_SERVICES environment variable for your app. Here is an example:

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


## {{site.data.keyword.messagehub}} Enterprise plan
{: #enterprise_connect}


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










