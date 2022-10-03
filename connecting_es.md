---

copyright:
  years: 2015, 2022
lastupdated: "2022-10-03a"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: EventStreams

---

{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}


# Connecting to {{site.data.keyword.messagehub}}
{: #connecting}

To connect to your {{site.data.keyword.messagehub}} instance, the following information is required:
* The endpoint URLs for the APIs
* Credentials for authentication

Read the following information about how to obtain these details and the connectivity options that you can use. Ensure that you complete the appropriate steps for your instance.
{: #shortdesc}


## Overview
{: #connect_enterprise}

Services that are provisioned using the Lite, Standard, or Enterprise plans are grouped in the dashboard under the heading **Services**. 

All plans use [IAM](docs/account?topic=account-overview){: external} for authentication. You don't need to understand IAM to get started but some knowledge is recommended if you want to secure your {{site.data.keyword.messagehub}} service. For more information, see [Managing access to your {{site.data.keyword.messagehub}} resources](/docs/EventStreams?topic=EventStreams-security). To complete the following steps and be authorized to create topics, your application or Service Key must have a Manager access role. By default, the owner of the account containing the service instance has this role.

By default, {{site.data.keyword.messagehub}} instances are configured to use the {{site.data.keyword.Bluemix_short}} public network, so they are accessible over the public Internet. If required, you can restrict this access by selecting an alternate networking type or restricting the location that connections are accepted from. For more information, see [Restricting Network Access](/docs/EventStreams?topic=EventStreams-restrict_access).

## Connection information
{: #connection_information}

To access a service instance, create a service key. A service key contains the information needed to access the instance including the endpoint details for its APIs and a unique API key credential.

To create a service key using the {{site.data.keyword.Bluemix_notm}} console:

1. Locate your {{site.data.keyword.messagehub}} service on the dashboard.
2. Click your service tile.
3. Click **Service Credentials**.
4. Click **New Credential**. 
5. Complete the details for your new credential like a name and role and click **Add**. A new credential appears in the credentials list.
6. Click this credential using **View Credentials** to reveal the details in JSON format.

To create a service key using the {{site.data.keyword.Bluemix_notm}} CLI:

1. Locate your service: `ibmcloud resource service-instances` 
2. Create a service key: `ibmcloud resource service-key-create <key_name> <key_role> --instance-name <your_service_name>`
3. Print the service key: `ibmcloud resource service-key <key_name>`

A single set of endpoint details are contained in each service key. For service instances configured to be connected to a single network type, either the {{site.data.keyword.Bluemix_notm}} public network (the default) or the {{site.data.keyword.Bluemix_notm}} private network, the service key will contain the details relevant to that network type. For instances configured to support both the private and public networks, details for the public network will be returned. If you want details for the private network, you must add the `--service-endpoint private` parameter the previous CLI command. For example: 
```text
ibmcloud resource service-key-create <private-key-name> <role> --instance-name <instance-name> --service-endpoint private
```
{: codeblock}
{: note}
 
For more information, see [Network types](/docs/EventStreams?topic=EventStreams-restrict_access#network_type).

## Establishing a connection
{: #establishing_connection}

To connect a Kafka application:
* Use the <bootstrap_endpoints> field from the service key as the `bootstrap.servers` property of your kafka application.
* Set the security.protocol property to SASL_SSL and the sasl.mechanism property to PLAIN.
* Use the <user> field from the service key as the username and the <api_key> field from the service key as the password. Ensure that your application parses the details. 
* For more information, see [Configuring your Kafka API client](/docs/EventStreams?topic=EventStreams-kafka_using#kafka_api_client). 

To call an HTTP API:
* Use the <kafka_admin_url> field of the service key as the base URL for HTTP requests. 
* Use the {{site.data.keyword.Bluemix_notm}} CLI `ibmcloud iam oauth-tokens` command to generate an auth token. Place this token in the `Authorization` header of the HTTP request with the value formatted as `Bearer <token>`. Both API key or JWT tokens are supported.
* Further documentation is provided for each API, for example:
    * [REST Admin API](/docs/EventStreams?topic=EventStreams-admin_api)
    * [REST Producer API](/docs/EventStreams?topic=EventStreams-rest_producer_using)
    * [Schema Registry API](/docs/EventStreams?topic=EventStreams-ES_schema_registry#schema_registry_rest_endpoints)

## Network connectivity
{: #network_connectivity}

By default, all {{site.data.keyword.messagehub}} instances are configured to be accessible over the public Internet. If using the Enterprise plan, you can restrict connectivity as follows:

Private networking
:   If your workload is running entirely within the {{site.data.keyword.Bluemix_notm}}, and public access to the service is not required, {{site.data.keyword.messagehub}} instances can instead be configured to be accessible only over the {{site.data.keyword.Bluemix_notm}} private network. This offers increased isolation and does not incur the egress bandwidth charges associated with public traffic. Instances can also be configured to be accessible over both the {{site.data.keyword.Bluemix_notm}} public and private networks.

Context-based restrictions
:   You can define access rules that limit the network locations where connections are accepted from, according to certain characteristics. For example, network type, IP ranges, VPC, or other services.

For more information, see [Restricting network access](docs/EventStreams?topic=EventStreams-restrict_access).

### Accessing an Enterprise instance over the private network from Classic infrastructure
{: #private_network_classic}

To access your Enterprise instance over the private network for workloads deployed on {{site.data.keyword.Bluemix_notm}} classic infrastructure, the Virtual Route Forwarding (VRF) and Service Endpoints features must be enabled in your account. For more information, see [Restricting network access](docs/EventStreams?topic=EventStreams-restrict_access).

### Accessing an Enterprise Instance over the Private Network from a VPC
{: #private_network_vpc}

For workloads deployed in an {{site.data.keyword.Bluemix_notm}} VPC to access your Enterprise instance over the private network, a Virtual Private Endpoint (VPE) must be created in the VPC:
1. In the {{site.data.keyword.Bluemix_notm}} console, click the menu icon and select **VPC Infrastructure** > **Network** > **Virtual private endpoint gateways**. 
2. Create a VPE for your {{site.data.keyword.messagehub}} instance using the guidance in [About virtual private endpoint gateways](/docs/vpc?topic=vpc-about-vpe). 
3. After you create your VPE, it might take a few minutes for the new VPE and pDNS to complete the process and begin working for your VPC. Completion is confirmed when you see an IP address set in the [details view](/docs/vpc?topic=vpc-vpe-viewing-details-of-an-endpoint-gateway&interface=ui) of the VPE. 


### Accessing an Enterprise instance over the private network from outside the {{site.data.keyword.Bluemix_notm}}
{: #private_network_outside_cloud}

You can use solutions like [Direct Link 2.0](https://cloud.ibm.com/docs/dl){: external} to connect an external network, for example in an on-premise data center, directly to the {{site.data.keyword.Bluemix_notm}} private network. For workloads running on an external network you must take the following additional consideration into account to connect successfully to Kafka. Note, these restrictions do not apply to HTTP workloads.

The private endpoint details allocated to your instance (as described in the service key) must be resolvable and routeable from the network that the workload is running in. It is not possible to specify alternate hostname entries in the workloads `bootstrap.servers` properties as a way to route traffic from the external network.

This is because of Kafka's two-step connection process. In the initial step, the hostnames provided in the client's `bootstrap.servers` property are used to establish the first bootstrap connection. However, the server then responds to the client with the actual endpoint hostname details it should use. These hostname details will be the private endpoint details originally allocated to your instance and cannot be changed. Hence, the details must be resolvable and routeable directly from the external network.

For further information, see [Accessing private API endpoints from an on-premises network using IBM Cloud Direct Link](https://cloud.ibm.com/docs/vpc?topic=vpc-end-to-end-private-connectivity&interface=cli){: external}.


## What to do next
{: #after_connecting}

Now you have connection and credential information, you can choose an {{site.data.keyword.messagehub}}. For more information, see [Using the Kafka API](/docs/EventStreams?topic=EventStreams-kafka_using).





<!-- 03/10/22 comment out while I make Charlie's changes
Complete the following steps to bind your application and obtain Service Keys for your service. To be authorized to create topics, your application or Service Key must have a Manager access role.

To connect an application, the method that is used depends on where the application is deployed, that is in Cloud Foundry or deployed outside Cloud Foundry, for example in the Kubernetes Service.

## Provision an {{site.data.keyword.messagehub}} instance
{: #provision_instance}

As a prerequisite, you must first provision an {{site.data.keyword.messagehub}} service instance for either the Standard or Enterprise plan. Next, obtain {{site.data.keyword.messagehub}} API connection details by completing the following tasks.

## Connect applications 
{: #connect_enterprise_external}

For applications that run outside Cloud Foundry, credentials are generated by creating a service key. When you obtain the service key, manually pass the details of the key to your application by using your chosen method.

### Get credentials by using the {{site.data.keyword.Bluemix_notm}} console
{: #connect_enterprise_external_console}

1. Locate your {{site.data.keyword.messagehub}} service on the dashboard.
2. Click your service tile.
3. Click **Service Credentials**.
4. Click **New Credential**. 
5. Complete the details for your new credential like a name and role and click **Add**. A new credential appears in the credentials list.
6. Click this credential using **View Credentials** to reveal the details in JSON format.
7. Pass these credentials to your application. Specify `token` as your user name and the <api_key> as your password. Separate `token` and the <api_key> with a colon. For more information, see [Configuring your Kafka API client](/docs/EventStreams?topic=EventStreams-kafka_using#kafka_api_client).

    Ensure that your application parses the details.

### Get credentials by using the {{site.data.keyword.Bluemix_notm}} CLI
{: #connect_enterprise_external_cli}

1. Locate your service: `ibmcloud resource service-instances`
2. Create a service key: `ibmcloud resource service-key-create <key_name> <key_role> --instance-name <your_service_name>`
3. Print the service key: `ibmcloud resource service-key <key_name>`
4. Pass these credentials to your application. Specify `token` as your username and the <api_key> as your password. Separate `token` and the <api_key> with a colon. For more information, see [Configuring your client](/docs/EventStreams?topic=eventstreams-kafka_api_client).

    Ensure that your application parses the details.

The endpoints in the service key are generated according to the service endpoints settings of the instance. For example, public endpoints are generated for `--service-endpoints=public`, and private endpoints are generated for `--service-endpoints=private`. However, for an instance that has `--service-endpoints=public-and-private`, public endpoints are generated by default. To generate private endpoints in the service key, use the following command: 

```text
ibmcloud resource service-key-create <private-key-name> <role> --instance-name <instance-name> --service-endpoint private
```
{: codeblock}
  
## Connect Cloud Foundry applications
{: #connect_enterprise_cf}

Your application must be bound to the {{site.data.keyword.messagehub}} service instance. To bind a Cloud Foundry application to a non-Cloud Foundry service, create a Cloud Foundry service alias first and then reference this alias from your Cloud Foundry application when binding. 

When bound, the connection details are then made available to the application in JSON format using the VCAP_SERVICES environment variable. You can bind an application and service by using either the [{{site.data.keyword.Bluemix_notm}} console](/docs/EventStreams?topic=EventStreams-connecting#connect_enterprise_cf_console) or the [{{site.data.keyword.Bluemix_notm}} CLI](/docs/EventStreams?topic=EventStreams-connecting#connect_enterprise_cf_cli).

### Bind an application by using the {{site.data.keyword.Bluemix_notm}} console
{: #connect_enterprise_cf_console}

1. Ensure that you are in the intended Cloud Foundry Organization and Space.
2. Locate your Cloud Foundry Application on the dashboard or create an application by clicking **Create resource**.
3. Click your application tile.
4. Click **Connections**.
5. Click **Create Connection**.
6. Select the {{site.data.keyword.messagehub}} service tile that you want to bind to and click **Connect**. 
7. In the **Connect IAM-Enabled Service** window that appears, select an access role from **Access Role for Connection** and a service ID from the **Service ID for Connection** list (you can accept the auto-generated ID). Click **Connect**. 

    This step creates a Cloud Foundry service alias for your {{site.data.keyword.messagehub}} service and then binds your application to this alias.

    Restage your application for the changes to take effect.
8. Click the **Runtime** tab on the left and select the **Environment variables** tab in the center. You can now verify your VCAP_SERVICES information. Your application can now access these variables as environment variables. 

### Bind an application by using the {{site.data.keyword.Bluemix_notm}} CLI
{: #connect_enterprise_cf_cli}

1. Ensure that you are in the intended Cloud Foundry Organization and Space. You can navigate interactively by running the following command:
    `ibmcloud target --cf`
2. Locate your app:
    `ibmcloud app list`

    If you have a manifest file, you can create a new app by running the following command:

    `ibmcloud app push`

    Because the app is not bound to {{site.data.keyword.messagehub}} yet, the app cannot establish a connection. Therefore, push the application with the `--no-start` parameter to avoid unnecessary connection failures.
3. Locate your service:
    `ibmcloud resource service-instances`
4. Create a Cloud Foundry service alias:
    `ibmcloud resource service-alias-create <alias_name> --instance-name <your_service_name>`
5. Bind your app to the service alias created previously:

    `ibmcloud service bind <your_ app_name> <alias_name>`.

    Alternatively, you can update your manifest file and push the application again.
6. Verify that the VCAP_SERVICES environment variable is available in your application runtime:
    `ibmcloud app env <your_app_name>`
7. Pass these credentials to your application. Specify `token` as your username and the <api_key> as your password. Separate `token` and the <api_key> with a colon. For more information, see [Configuring your client](/docs/EventStreams?topic=EventStreams-kafka_api_client). 

    You might need to restage your application for the changes to take effect.


## What to do next
{: #after_connecting}

Now you have connection and credential information, you can choose an {{site.data.keyword.messagehub}} client. For more information, see [Using the Kafka API](/docs/EventStreams?topic=EventStreams-kafka_using).

-->


