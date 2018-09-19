---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

<!-- Notes from chat with Charlie 

Different plan for provisioning

Quality of service from each plan

Life of a user through cycle - APIs, feature sets

-->

# About the Alpha program
{: #alpha_about }

The Alpha program provides early access to new features in the {{site.data.keyword.messagehub}} service. The Alpha program is not currently active.

<!--
## Premium plan
{: premium_plan}

The Premium plan is designed for users who have performance and other functional requirements that go beyond the public service. It provides a single-tenant version of the {{site.data.keyword.messagehub}} service where you have sole use of an Apache Kafka cluster. This version allows you to:

* Take full advantage of the capacity and performance of the cluster

* Have greatly increased limits and number of partitions

* Benefit from zero management costs with a fully managed cluster that is automatically maintained and updated

## About your Alpha cluster
{: alpha_cluster}

Your Alpha cluster is deployed with Apache Kafka version 1.1 and is capable of delivering a maximum message throughput of 90 000 KB per second. 

You can create a maximum of 1000 partitions and  each partition can retain a maximum of 1 GB data for up to 30 days. For resilience, data is stored across 3 replicas and the committed offset for each partition is held for a maximum of 7 days.

The following two APIs are supported:

* For messaging, Kafka clients from version 0.10.x and later are supported, including the option to use Kafka Streams, Kafka Connect and KSQL.

* For administration, a REST API is available for creating, deleting, and listing topics.

The Alpha program is available in the US-South region only. Access to clusters is managed using IAM.

## Connecting to your cluster
{: alpha_connect}

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
Only your first five brokers are listed in VCAP_SERVICES. If you have more than five brokers, use a Kafka client to retrieve the details of you other brokers. 

## Connecting a client to the Kafka API

To connect a client to the Kafka API, complete the following steps:

1. Set the clients <code>bootstrap.servers</code> property to a comma-separated list of the brokers listed in <code>kafka_brokers_sasl</code>.

2. Set the clients <code>sasl.jaas.config</code> USERNAME field to your <code>token</code>, and the PASSWORD field to your <code>apikey</code> 

The Kafka client that you use must support the following features:

* Client version 0.10.x or newer

* Authentication using the SASL Plain mechanism

* The Service Name Identification (SNI) extension to the TLS v1.2 protocol

This method of retrieving the endpoint and credential information differs from the existing {{site.data.keyword.messagehub}} service. Apps that currently run against {{site.data.keyword.messagehub}} will require changes to reflect the alternative field names that are required from VCAP_SERVICES and to the username/password fields submitted to Kafka. These changes will not be required in future versions of the Alpha.

## Connecting a client to the REST API

To connect a client to the REST API, complete the following steps:

* The URI for the REST API is provided in the <code>kafka_admin_url</code>

* Set the HTTP <code>Content-Type</code> header to <code>application/json</code>

* Set the HTTP <code>X-Auth-Token</code> header to the value of <code>apikey</code>

For simple steps to get up and running with the Alpha, see [Getting started with the Alpha program](/docs/services/EventStreams/eventstreams120.html).


## Administering {{site.data.keyword.messagehub}}
{: alpha_admin}

The only administration tasks required in a cluster are to create, list, and delete the topics you need. You can administer using one of the following methods:

* The Kafka admin APIs directly from your application. For example for Java, by using the <code>createTopics()</code>, <code>deleteTopics()</code> or <code>listTopics()</code> methods from [AdminClient ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://kafka.apache.org/11/javadoc/index.html?org/apache/kafka/clients/admin/AdminClient.html){:new_window}.

* Interactively by using the Web UI for the service instance available in the IBM Cloud portal.

* The admin REST API provided in the cluster.

You can find further details of the create, list, and delete functions provided by the admin REST API (which is compatible with the existing {{site.data.keyword.messagehub}} admin API) in the full specification for the API available from [admin-rest-api.yaml ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/event-streams-docs/blob/master/admin-rest-api/admin-rest-api.yaml){:new_window}.
To view the swagger file use Swagger tools, for example [Swagger Editor ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://editor.swagger.io/#/){:new_window}.

For a simple example that demonstrates how to create a topic using Curl, see [Getting started with the Alpha program](/docs/services/EventStreams/eventstreams120.html).

In the future, other configuration options will also be available.


## Samples

Coming soon...

For simple steps to get up and running with the Alpha, see [Getting started with the Alpha program](/docs/services/EventStreams/eventstreams120.html).

## Alpha limitations
{: alpha_limitations}

The current limitations of this Alpha program are as follows:

### Not available yet, but coming soon

* Support for multiple availability zones

* User-controlled scaling and load limits

* Integration with the {{site.data.keyword.cloudaccesstrailfull_notm}} service (previously known as AccessTrail) 

### Not currently planned

* Bridges

* REST messaging

* MQ Light APIs
-->







