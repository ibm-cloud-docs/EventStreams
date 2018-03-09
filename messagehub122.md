---

copyright:
  years: 2015, 2018
lastupdated: "2018-03-02"

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

The Alpha program provides early access to new features in the {{site.data.keyword.messagehub}} service. The current feature is the introduction of a new plan, the {{site.data.keyword.messagehub}} Premium plan.

## The Premium plan
{: premium_plan}

The Premium plan is designed for users who have performance and other functional requirements that go beyond the public service. It provides a single-tenant version of the {{site.data.keyword.messagehub}} service where you have sole use of an Apache Kafka cluster, allowing you to:

* Take full advantage of the capacity and performance of the cluster

* Have greatly increased limits and number of partitions

* Benefit from zero management costs with a fully managed cluster which is automatically maintained and updated

## About your Alpha cluster

Your Alpha clusters is deployed with Apache Kafka version 1.0.1 and is capable of delivering a maximum message throughput of 90,000 KB/sec. 

A maximum of 1000 partitions can be created, with each partition retaining a maximum of 1 GB data for up to 30 days. For resilience, data is stored across 3 replicas, with the offset data for each partition (holding the position of the last successfully consumed message) being held for a maximum of 7 days.

Two APIs are supported:

* For messaging, Kafka clients from version 0.10.x onwards are supported, including the use of KSQL, Kafka Streams and Kafka Connect.

* For administration, a REST API is available for creating, deleting and listing topics.

The Alpha program is available in the US-South region only, with access to clusters being managed using IAM

## Connecting to your cluster

To connect to an API in the cluster you need its endpoint URL and an apikey for authentication. These details can be retrieved from IAM using one of the following methods:

* For a Cloud Foundry application, click the 'Create connection' button that's in the 'Connections' tab for the app, on the left of the portal. Select the instance of the Message Hub service you'd like to connect to and click 'Connect', accepting the default options. Once complete, select the 'Runtime' tab for the app, then 'environment variables' to show VCAP_SERVICES.

* From the console for an external application, create a service apikey by using the following bx command ```bx resource service-key-create name-of-key Manager --instance-name name-of-your-service```. 

Copy the ```kafka_brokers_sasl```, ```kafka_admin_url``` and ```apikey``` fields from the generated info.

__To connect a client to the Kafka API__

* The clients ```bootstrap.servers``` property should be set to a comma seperated list of the brokers listed in ```kafka_brokers_sasl```

* The clients ```sasl.jaas.config``` USERNAME field should be set to the first eight characters of the ```apikey```, and the PASSWORD field to the remaining characters (this split will not be needed in future versions)

The Kafka client you use must support the following features:

* Client version 0.10.x or newer

* Authentication using the SASL Plain mechanism

* The Service Name Identification (SNI) extension to the TLS v1.2 protocol

NB This method of retrieving the endpoint and credential information differs from the existing Message Hub service. Apps which currently run against Message Hub will require changes to reflect the alternative field names required from VCAP_SERVICES and to the username/password fields submitted to Kafka. These changes will not be required in future versions of the Alpha.

__To connect a client to the REST API__

* The URI for the REST API is provided in the ```kafka_admin_url```

* The HTTP ```Content-Type``` header should be set to ```application/json```

* The HTTP ```X-Auth-Token``` header should be set to the value of ```apikey```

For simple steps to get up and running with the Alpha, see [Getting started with the Alpha program](/docs/services/MessageHub/messagehub120.html).


## Administering Message Hub

The only administration tasks required in a cluster are to create, list and delete the topics you need. This can be achieved in one of two ways, either by using:

* The Kafka client API directly from your application e.g. for Java, by using the ```createTopics()```, ```deleteTopics()``` or ```listTopics()``` functions.

* The admin REST API provided in the cluster.

Further details of the create, list and delete functions provided by the admin REST API (which is compatible with the existing Message Hub admin API). You can download the full specification for the API from [admin-rest-api.yaml ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/message-hub-docs/blob/master/admin-rest-api/admin-rest-api.yaml){:new_window}.
To view the swagger file use Swagger tools, for example [Swagger editor ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://editor.swagger.io/#/){:new_window}.


To invoke the functions requires TLS v1.2 and a valid service api key. For a simple example demonstrating how to create a topic using curl, see [Getting started with the Alpha program](/docs/services/MessageHub/messagehub120.html).

In the future, other configuration options will also be available.


## Samples

Coming soon...for simple steps to get up and running with the Alpha, see [Getting started with the Alpha program](/docs/services/MessageHub/messagehub120.html).

## Alpha limitations

The current limitations of this Alpha program are as follows:

### Not available yet, but coming soon

The current limitations of this Alpha program are as follows:

### Not available yet, but coming soon

* A UI

* Multi availability zone support

* User-controlled scaling and load limits

* Finer grained access controls, including topics

* Integration with the IBM Cloud Activity Tracker service (previously known as AccessTrail) 

### Not currently planned:

* Bridges

* REST messaging

* MQ Light APIs







