---

copyright:
  years: 2020
lastupdated: "2020-06-18"

keywords: IBM Event Streams, schema registry 

subcollection: EventStreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}


# Event Streams Schema Registry – Early Access Documentation
{: #ES_schema_registry}

## Overview
{: #ES_overview}

This document describes the schema registry capability being developed for the IBM Event Streams managed Kafka service running in 
IBM Cloud. The purpose of the schema registry is to provide a place to store descriptions of the message formats used by your 
producers and consumers. The benefit of storing these descriptions is that you are able to validate that your producing and 
consuming applications will correctly interoperate.
Currently the schema registry is in early access status. This means that a limited function version of the registry is being made 
available to a small group of users for the purpose of gathering feedback, and rapidly iterating on the design of the registry. 
Please note that while the schema registry is in early access, there may be occasions when we will delete all of the schema data 
held within the registry.

## Current features
{: #ES_current_features}

Bold typeface is used to denote features added since last Early Access release:

•	Support for creating, listing and deleting schemas via a REST interface
•	**Support for creating, listing and deleting versions of a schema, via a REST interface**
•	Support for using schema information in Kafka producer and consumer applications via the Confluent AVRO SerDes
•	Support for Apache AVRO as the format used to express schemas
•	**Support for applying constraints on schema compatibility, either at a global scope, or on a per-schema basis**
•	Access to schema registry requires authentication and access is controlled via IAM
•	**Access to individual schemas, and compatibility rules can be controlled via a new IAM schema resource type**
•	**Constraints on maximum schema size (64K), the maximum number of schemas that can be stored in the registry (1000) and the maximum 
number of versions a schema can have (100)**
•	SLA of 99.99% availability, consistent with that of the Event Streams service

## Current limitations
{: #ES_current_limitations}

•	No caching performed for frequently requested schemas
•	Does not publish metrics to Sysdig
•	Does not generate Activity Tracker events
•	There may be other missing functions that you require. Please let us know!
 
## Enabling the schema registry
{: #enabling_schema_registry}

Currently the schema registry is not enabled by default and can only be enabled for Event Streams Enterprise plan service instances. 
To request the enablement of the schema registry, please raise a [support ticket]
(https://cloud.ibm.com/docs/get-support?topic=get-support-getting-customer-support#using-avatar). 
Ensure that you include the CRN of your Event Streams service instance in the ticket. The CRN of the service instance can be found 
using the following IBM Cloud CLI command (where $SERVICENAME is the name of your Event Streams service instance):

```
ibmcloud resource service-instance $SERVICENAME
```

If you have already enabled the schema registry capability for an Event Streams Enterprise plan service instance, 
it will automatically receive updates as new capabilities become available.

## Accessing the schema registry
{: #accessing_schema_registry}

To access the schema registry, you will need the URL of the schema registry as well as a set of credentials that can be used to 
authenticate with the registry. Both of these pieces of information can be found by inspecting the service credentials for your service. 
To view these in the UI, click on your service instance, select “service credentials” in the left-hand navigation pane, then click on 
the “view credentials” link located next to one of the service credentials listed in the table. You should see something like this:
 
You will need the value of kafka_http_url, which is also the URL of the schema registry, and the value of apikey which you can use 
as the credential for authenticating with the schema registry.

It is also possible to authenticate using an API key that has been granted from a service ID, providing the service ID has a policy 
that permits it at least “reader” role access to the Event Streams cluster. This approach is more flexible and is a better choice 
if you are granting access to multiple other people or teams. See the [Managing access to your Event Streams resources]
(https://cloud.ibm.com/docs/services/EventStreams?topic=eventstreams-security) help topic for more details.

You can use cURL to verify that you have the correct URL and API key values. Here’s a screenshot showing successful verification:
 
The cURL command to use is as follows (where $APIKEY is substituted with your API key, and $URL is substituted with the URL from the 
Kafka HTTP URL property of the service credentials):

```
curl -i –u token:$APIKEY $URL/artifacts
```

Assuming you haven’t already used the schema registry, you should see the following output that indicates that there are no schemas 
stored in the registry:

```
HTTP/1.1 200 OK
Date: Thu, 16 Jan 2020 15:45:26 GMT
Content-Type: application/json
Content-Length: 11
Connection: keep-alive
```
[]

## Managing access to schemas
{: #managing_access_schemas}

The authorization model for the Schema Registry is based on IBM Cloud Identity Access Management (IAM), and is intended to be 
consistent with the existing authorization model for Kafka topics, consumer groups etc – see: 
https://cloud.ibm.com/docs/EventStreams?topic=eventstreams-security 

 
## IAM Resources
{: #iam_resources}

This schema registry introduces a new IAM resource type: schema. This can be used as part of a CRN to identify a particular schema. 
For example:

-	A CRN that names a specific schema (test-schema), for a particular instance of an Event Streams service:
  - crn:v1:bluemix:public:messagehub:us-south:a/6db1b0d0b5c54ee5c201552547febcd8:91191e31-5642-4f2d-936f-647332dce3ae:schema:test-schema
- A CRN that describes all of the schemas for a particular instance of the Event Streams service:
  - crn:v1:bluemix:public:messagehub:us-south:a/6db1b0d0b5c54ee5c201552547febcd8:91191e31-5642-4f2d-936f-647332dce3ae:schema:
- While not directly related to the addition of the schema resource type, it is also worth noting that it is possible to apply policies 
to a CRN describing a particular Event Streams instance. For example, policies granted at the scope of this CRN would affect all 
resources (topics, schemas, etc.) belonging to the cluster:
  - crn:v1:bluemix:public:messagehub:us-south:a/6db1b0d0b5c54ee5c201552547febcd8:91191e31-5642-4f2d-936f-647332dce3ae::
 
With the addition of the new schema IAM resource type it is possible to create policies that control access using varying degrees of 
granularity, for example:

-	a specific schema
-	a set of schemas selected via a wildcard expression
-	all of the schemas stored by an instance of IBM Event Streams
-	all of the schemas stored by all of the instances of IBM Event Streams in an account

Event Streams already has the concept of a cluster resource type. This is used to control all access to the service instance, 
with the minimum role of Reader being required to access any Kafka or HTTPS endpoint. This use of the cluster resource type will 
also be applied to the schema registry whereby a minimum role of Reader will be required to access the registry.
 
## IAM Roles
{: #iam_roles}

IAM service access roles are germane to protecting schema resource types. Three service access roles are defined as follows:

-	Reader (perform read-only actions within Event Streams such as viewing resources)
-	Writer (have permissions beyond the reader role, including creating and editing Event Streams resources)
-	Manager (have permissions beyond the writer role to complete privileged actions. In addition, you can create and edit Event Streams 
resources).
 
Also note that IAM roles are cumulative, in that someone granted the writer role on a resource can also perform any action that would 
require the reader role. Likewise, someone with the manager role can also perform actions that would require either the reader or writer 
roles.

The IAM roles (and the resources they must be applied to) are described for each of the REST endpoints provided by the schema registry. 
These are listed later in this document.

### Example Authorization Scenarios
{: #example_authorization_scenarios}

The following table describes some examples of scenarios for interacting with the Event Streams schema registry, together with the 
roles which would be required by the actors involved.

Scenario	Role and resource requirements

The process of managing schemas is handled separately to deploying applications. New schema versions are placed into the registry by a person or process that is separate from the applications that use the schemas	The application would require:
·	Reader role for the cluster resource
·	Reader role for the schema resource

The person or process responsible for adding schemas to the registry would require:
·	Reader role for the cluster resource
·	Writer role for the schema resource
The process for adding a new schema to the registry needs to specify a non-default rule that controls how versions of the schema are allowed to evolve.	The process would require:
·	Reader role for the cluster resource
·	Manager role for the schema resource
Schemas are managed alongside the application code that uses the schema. New schema versions are created at the point an application tries to make use of the new schema version	The application would require:
·	Reader role for the cluster resource
·	Writer role for the schema resource
The global default rule that controls schema evolution is changed	The person or automation would require:
·	Manager role for the cluster resource


 
Applying compatibility rules to new versions of schemas
The schema registry supports enforcing compatibility rules when creating a new version of a schema. If a request is made to create a new schema version that does not conform to the required compatibility rule, then the registry will reject the request. The following rules are supported:
Compatibility Rule	Tested against	Description
NONE	N/A	No compatibility checking is performed when a new schema version is created.

BACKWARD	Latest version of the schema	A new version of the schema can omit fields that are present in the existing version of the schema.
A new version of the schema can add optional fields that are not present in the existing version of the schema.
BACKWARD_TRANSITIVE	All versions of the schema	
FORWARD	Latest version of the schema	A new version of the schema can add fields that are not present in the existing version of the schema.
A new version of the schema can omit optional fields that are present in the existing version of the schema.
FORWARD_TRANSITIVE	All versions of the schema	
FULL	Latest version of the schema	A new version of the schema can add optional fields that are not present in the existing version of the schema.
A new version of the schema can omit optional fields that are present in the existing version of the schema.
FULL_TRANSITIVE	All versions of the schema	

These rules can be applied at two scopes:
1.	At a global scope, which is the default that is used when creating a new schema version
2.	At a per-schema level. If a per-schema level rule is defined, then this overrides the global default for the particular schema.

By default, the registry has a global compatibility rule setting of NONE. Per-schema level rules must be defined otherwise the schema will default to using the global setting.

 
Using the schema registry with the Confluent SerDes
The schema registry has been tested with version 5.3.1 of the Confluent AVRO serializer/deserializer Java library. To configure the Confluent SerDes to use the schema registry, you will need to specify two properties in the configuration of your Kafka client:
Property name	Value
SCHEMA_REGISTRY_URL_CONFIG	Set this to the URL of the schema registry, including your credentials as basic authentication, and with a path of “/confluent”. For example, if $APIKEY is the API key to use and $HOST is the host from the Kafka HTTP URL property in the service credentials, then the value should be in the form:
https://token:$APIKEY@$HOST/confluent
BASIC_AUTH_CREDENTIALS_SOURCE	Set to “URL”. This instructs the SerDes to use HTTP basic authentication using the credentials supplied in the schema registry URL.

Here’s an example showing the properties required to create a Kafka producer, that uses the Confluent SerDes, and can be connected to the Event Streams service:
 
Schema registry REST endpoints
We intend to integrate the schema registry with the Event Streams UI and CLI. However, currently the only interface to the schema registry is via a REST interface. This REST interface may be subject to change as the design of the schema registry is iterated upon.

The REST API offers four main capabilities:
1.	Creating, reading, and deleting schemas.
2.	Creating, reading, and deleting individual versions of a schema
3.	Reading and updating the global compatibility rule for the registry
4.	Creating, reading, updating, and deleting compatibility rules that apply to individual schemas

Authentication
As described above, you can authenticate to the schema registry using an API key. This is supplied as the password portion of a HTTP basic authentication header. Set the username portion of this header to the word “token”. It is also possible to grant a bearer token for a system ID or user and supply this as a credential. To do this specify a HTTP header in the format: “Authorization: Bearer $TOKEN” (where $TOKEN is the bearer token). For example:
curl –H "Authorization: Bearer $TOKEN" ...

Errors
If an error condition is encountered the schema registry will return a non-2XX range HTTP status code. The body of the response will contain a JSON object in the following form:
{
    "error_code":404,
    "message":"No artifact with id 'my-schema' could be found."
}

The properties of the error JSON object are as follows:
Property name	Description
error_code	The HTTP status code of the response
message	A description of the cause of the problem
incident	This field is only included if the error is a result of a problem with the schema registry. This value can be used by IBM service to correlate a request to diagnostic information captured by the registry.

 
Create a schema - POST /artifacts
This endpoint is used to store a schema in the registry. The schema data is sent as the body of the post request. An ID for the schema can be included using the ‘X-Registry-ArtifactId' request header. If this header is not present in the request, then an ID will be generated. The content type header must be set to “application/json”.

Example cURL request:
curl -u token:$APIKEY -H 'Content-Type: application/json' -H 'X-Registry-ArtifactId: my-schema' $URL/artifacts -d '{"type":"record","name":"Citizen","fields":[{"name": "firstName","type":"string"},{"name":"lastName","type":"string"},{"name":"age","type":"int"},{"name":"phoneNumber","type":"string"}]}'

Example response:
{"id":"my-schema","type":"AVRO","version":1,"createdBy":"","createdOn":1579267788258,"modifiedBy":"","modifiedOn":1579267788258,"globalId":75}
  
Creating a schema requires at least both:
•	Reader role access to the Event Streams cluster resource type
•	Writer role access to the schema resource that matches the schema being created

List schemas – GET /artifacts
You can generate a list of the IDs of all of the schemas stored in the registry by making a GET request to the /artifacts endpoint.

Example cURL request:
curl -u token:$APIKEY $URL/artifacts
                  
Example response:
["my-schema"]

Listing schemas requires at least:
•	Reader role access to the Event Streams cluster resource type

Delete a schema – DELETE /artifacts/{schema-id}
Schemas are deleted from the registry by issuing a DELETE request to the /artifacts/{schema-id} endpoint (where {schema-id} is the ID of the schema). If successful an empty response, and a status code of 204 (no content) is returned.

Example cURL request:
curl -u token:$APIKEY –X DELETE $URL/artifacts/my-schema

Deleting a schema requires at least both:
•	Reader role access to the Event Streams cluster resource type
•	Manager role access to the schema resource that matches the schema being deleted

Create a new version of a schema – POST /artifacts/{schema-id}/versions
To create a new version of a schema, make a POST request to the /artifacts/{schema-id}/versions endpoint, (where {schema-id} is the ID of the schema). The body of the request must contain the new version of the schema.
If the request is successful the new schema version is created as the new latest version of the schema, with an appropriate version number, and a response with status code 200 (OK) and a payload containing metadata describing the new version, (including the version number), is returned.

Example cURL request:
curl -u token:$APIKEY -H 'Content-Type: application/json' $URL/artifacts/my-schema/versions -d '{"type":"record","name":"Citizen","fields":[{"name": "firstName","type":"string"},{"name":"lastName","type":"string"},{"name":"age","type":"int"},{"name":"phoneNumber","type":"string"}]}'

Example response:
{"id":"my-schema","type":"AVRO","version":2,"createdBy":"","createdOn": 1579267978382,"modifiedBy":"","modifiedOn":1579267978382,"globalId":83}

Creating a new version of a schema requires at least both:
•	Reader role access to the Event Streams cluster resource type
•	Writer role access to the schema resource that matches the schema getting a new version

Get the latest version of a schema – GET /artifacts/{schema-id}
To retrieve the latest version of a particular schema, make a GET request to the /artifacts/{schema-id} endpoint, (where {schema-id} is the ID of the schema). If successful, the latest version of the schema is returned in the payload of the response.

Example cURL request:
curl -u token:$APIKEY $URL/artifacts/my-schema

Example response:
{"type":"record","name":"Citizen","fields":[{"name": "firstName","type":"string"},{"name":"lastName","type":"string"},{"name":"age","type":"int"},{"name":"phoneNumber","type":"string"}]}

Getting the latest version of a schema requires at least both:
•	Reader role access to the Event Streams cluster resource type
•	Reader role access to the schema resource that matches the schema being retrieved 

Getting a specific version of a schema – GET /artifacts/{schema-id}/versions/{version}
To retrieve a specific version of a schema, make a GET request to the /artifacts/{schema-id}/versions/{version} endpoint, (where {schema-id} is the ID of the schema, and {version} is the version number of the specific version you need to retrieve). If successful, the specified version of the schema is returned in the payload of the response.

Example cURL request:
curl -u token:$APIKEY $URL/artifacts/my-schema/versions/3

Example response:
{"type":"record","name":"Citizen","fields":[{"name": "firstName","type":"string"},{"name":"lastName","type":"string"},{"name":"age","type":"int"},{"name":"phoneNumber","type":"string"}]}

Getting the latest version of a schema requires at least both:
•	Reader role access to the Event Streams cluster resource type
•	Reader role access to the schema resource that matches the schema being retrieved

Listing all of the versions of a schema – GET /artifacts/{schema-id}/versions
To list all versions of a schema currently stored in the registry, make a GET request to the /artifacts/{schema-id}/versions endpoint, (where {schema-id} is the ID of the schema). If successful, a list of all current version numbers for the schema is returned in the payload of the response.

Example cURL request:
curl -u token:$APIKEY $URL/artifacts/my-schema/versions

Example response:
[1,2,3,5,6,8,100]

Getting the list of available versions of a schema requires at least both:
•	Reader role access to the Event Streams cluster resource type
•	Reader role access to the schema resource that matches the schema being retrieved

Deleting a version of a schema – DELETE /artifacts/{schema-id}/versions/{version}
Schema versions are deleted from the registry by issuing a DELETE request to the /artifacts/{schema-id}/versions/{version} endpoint (where {schema-id} is the ID of the schema, and {version} is the version number of the schema version). If successful an empty response, and a status code of 204 (no content) is returned. Deleting the only remaining version of a schema will also delete the schema.

Example cURL request:
curl -u token:$APIKEY –X DELETE $URL/artifacts/my-schema/versions/3

Deleting a schema version requires at least both:
•	Reader role access to the Event Streams cluster resource type
•	Manager role access to the schema resource that matches the schema being deleted

 
Updating a global rule – PUT /rules/{rule-type}
Global compatibility rules can be updated by issuing a PUT request to the /rules/{rule-type} endpoint, (where {rule-type} identifies the type of global rule to be updated - currently the only supported type is COMPATIBILITY), with the new rule configuration in the body of the request. If the request is successful then the newly updated rule config is returned in the payload of the response, together with a status code of 200 (OK).

The JSON document sent in the request body must have the following properties:
Property name	Description
type	Must always be set to the value COMPATIBILITY
config	Must be set to one of the following values: NONE, BACKWARD, BACKWARD_TRANSITIVE, FORWARD, FORWARD_TRANSITIVE, FULL, or FULL_TRANSITIVE (see the earlier section on compatibility rules for details on each of these values) 

Example cURL request:
curl -u token:$APIKEY –X PUT $URL/rules/COMPATIBILITY -d '{"type":"COMPATIBILITY","config":"BACKWARD"}'

Example response:
{"type":"COMPATIBILITY","config":"BACKWARD"}

Updating a global rule configuration requires at least:
•	Manager role access to the Event Streams cluster resource type

 
Getting the current value of a global rule – GET /rules/{rule-type}
The current value of a global rule is retrieved by issuing a GET request to the /rules/{rule-type} endpoint, (where {rule-type} is the type of global rule to be retrieved - currently the only supported type is COMPATIBILITY). If the request is successful then the current rule configuration is returned in the payload of the response, together with a status code of 200 (OK).

Example cURL request:
curl -u token:$APIKEY $URL/rules/COMPATIBILITY

Example response:
{"type":"COMPATIBILITY","config":"BACKWARD"}

Getting global rule configuration requires at least:
•	Reader role access to the Event Streams cluster resource type

Creating a per-schema rule – POST /artifacts/{schema-id}/rules
Rules can be applied to a specific schema, overriding any global rules which have been set, by making a POST request to the /artifacts/{schema-id}/rules endpoint, (where {schema-id} is the ID of the schema), with the type and value of the new rule contained in the body of the request, (currently the only supported type is COMPATIBILITY). If successful an empty response, and a status code of 204 (no content) is returned.

Example cURL request:
curl -u token:$APIKEY $URL/artifacts/my-schema/rules -d '{"type":"COMPATIBILITY","config":"FORWARD"}'

Creating per-schema rules requires at least:
•	Reader role access to the Event Streams cluster resource type
•	Manager role access to the schema resource for which the rule will apply

 
Getting a per-schema rule – GET /artifacts/{schema-id}/rules/{rule-type}
To retrieve the current value of a type of rule being applied to a specific schema, a GET request is made to the /artifacts/{schema-id}/rules/{rule-type} endpoint, (where {schema-id} is the ID of the schema, and {rule-type} is the type of global rule to be retrieved - currently the only supported type is COMPATIBILITY). If the request is successful then the current rule value is returned in the payload of the response, together with a status code of 200 (OK).

Example cURL request:
curl -u token:$APIKEY $URL/artifacts/my-schema/rules/COMPATIBILITY

Example response:
{"type":"COMPATIBILITY","config":"FORWARD"}

Getting per-schema rules requires at least:
•	Reader role access to the Event Streams cluster resource type
•	Reader role access to the schema resource to which the rule applies

Updating a per-schema rule – PUT /artifacts/{schema-id}/rules/{rule-type}
The rules applied to a specific schema are modified by making a PUT request to the /artifacts/{schema-id}/rules/{rule-type} endpoint, (where {schema-id} is the ID of the schema, and {rule-type} is the type of global rule to be retrieved - currently the only supported type is COMPATIBILITY). If the request is successful then the newly updated rule config is returned in the payload of the response, together with a status code of 200 (OK).

Example cURL request:
curl -u token:$APIKEY –X PUT $URL/artifacts/my-schema/rules/COMPATIBILITY -d '{"type":"COMPATIBILITY","config":"BACKWARD"}'

Example response:
{"type":"COMPATIBILITY","config":"BACKWARD"}

Updating a per-schema rule requires at least:
•	Reader role access to the Event Streams cluster resource type
•	Manager role access to the schema resource to which the rule applies
Deleting a per-schema rule – DELETE /artifacts/{schema-id}/rules/{rule-type}
The rules applied to a specific schema are deleted by making a DELETE request to the /artifacts/{schema-id}/rules/{rule-type} endpoint, (where {schema-id} is the ID of the schema, and {rule-type} is the type of global rule to be retrieved - currently the only supported type is COMPATIBILITY). If the request is successful then an empty response is returned, with a status code of 204 (no content).

Example cURL request:
curl -u token:$APIKEY –X DELETE $URL/artifacts/my-schema/rules/COMPATIBILITY

Deleting a per-schema rule requires at least:
•	Reader role access to the Event Streams cluster resource type
•	Manager role access to the schema resource to which the rule applies


________________________________________________________________________
DELETE!!!!


# Using Kafka console tools with {{site.data.keyword.messagehub}}
{: #kafka_console_tools }

Apache Kafka comes with a variety of console tools for simple administration and messaging operations. You can use many of them with {{site.data.keyword.messagehub}}, although {{site.data.keyword.messagehub}} does not permit connection to its ZooKeeper cluster. As Kafka has developed, many of the tools that previously required connection to ZooKeeper no longer have that requirement.
{: shortdesc}

You can find these console tools in the <code>bin</code> directory of your Kafka download. You can download a client from [Apache Kafka downloads ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://kafka.apache.org/downloads){:new_window}.

To provide the SASL credentials to these tools, create a properties file based on the following example:

<pre>
<code>
  sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="USER" password="PASSWORD";
  security.protocol=SASL_SSL
  sasl.mechanism=PLAIN
  ssl.protocol=TLSv1.2
  ssl.enabled.protocols=TLSv1.2
  ssl.endpoint.identification.algorithm=HTTPS
</code>
</pre>
{:codeblock}

Replace USER and PASSWORD with the values from your {{site.data.keyword.messagehub}} **Service Credentials** tab in the {{site.data.keyword.Bluemix_notm}} console.


## Console producer
{: #console_producer }

You can use the Kafka console producer tool with {{site.data.keyword.messagehub}}. You must provide a list of brokers and SASL credentials.

After you've created the properties file as described previously, you can run the console producer in a terminal as follows:

<pre>
<code>
  $ kafka-console-producer.sh --broker-list KAFKA_BROKERS_SASL --producer.config CONFIG_FILE --topic TOPIC_NAME
</code>
</pre>
{:codeblock}

Replace the following variables in the example with your own values:
* KAFKA_BROKERS_SASL with the value from your {{site.data.keyword.messagehub}} **Service Credentials** tab in the {{site.data.keyword.Bluemix_notm}} console, as a list of host:port pairs separated with commas (for example, `host1:port1,host2:port2`). 
* CONFIG_FILE with the path of the configuration file. 

You can use many of the other options of this tool, with the exception of those that require access to ZooKeeper.


## Console consumer
{: #console_consumer }

You can use the Kafka console consumer tool with {{site.data.keyword.messagehub}}. You must provide a bootstrap server and SASL credentials.

After you've created the properties file as described previously, you can run the console consumer in a terminal as follows:

<pre>
<code>
  $ kafka-console-consumer.sh --bootstrap-server KAFKA_BROKERS_SASL --consumer.config CONFIG_FILE --topic TOPIC_NAME 
</code>
</pre>
{:codeblock}

Replace the following variables in the example with your own values:
* KAFKA_BROKERS_SASL with the value from your {{site.data.keyword.messagehub}} **Service Credentials** tab in the {{site.data.keyword.Bluemix_notm}} console, as a list of host:port pairs separated with commas (for example, `host1:port1,host2:port2`). 
* CONFIG_FILE with the path of the configuration file. 

You can use many of the other options of this tool, with the exception of those that require access to ZooKeeper.


## Consumer groups
{: #consumer_groups_tool }

You can use the Kafka consumer groups tool with {{site.data.keyword.messagehub}}. Because {{site.data.keyword.messagehub}} does not permit connection to its ZooKeeper cluster, some of the options are not available.

After you've created the properties file as described previously, you can run the consumer groups tools in a terminal. For example, you can list the consumer groups as follows:

<pre>
<code>
  $ kafka-consumer-groups.sh --bootstrap-server KAFKA_BROKERS_SASL --command-config CONFIG_FILE --list
</code>
</pre>
{:codeblock}

Replace the following variables in the example with your own values:
* KAFKA_BROKERS_SASL with the value from your {{site.data.keyword.messagehub}} **Service Credentials** tab in the {{site.data.keyword.Bluemix_notm}} console, as a list of host:port pairs separated with commas (for example, `host1:port1,host2:port2`). 
* CONFIG_FILE with the path of the configuration file.

Using this tool, you can also display details like the current positions of the consumers, their lag, and client-id for each partition for a group. For example:

<pre>
<code>
  $ kafka-consumer-groups.sh --bootstrap-server KAFKA_BROKERS_SASL --command-config CONFIG_FILE --describe --group GROUP
</code>
</pre>
{:codeblock}

Replace GROUP in the example with the group name that you want to retrieve details for. 

Here is some sample output from running the **kafka-consumer-groups** tool:
<pre>
<code>
GROUP              TOPIC    PARTITION  CURRENT-OFFSET  LOG-END-OFFSET  LAG         CONSUMER-ID      HOST          CLIENT-ID
consumer-group-1   foo        0          264             267            3          client-1-abc    example.com    client-1
consumer-group-1   foo        1          124             124            0          client-1-abc    example.com    client-1
consumer-group-1   foo        2          212             212            0          client-2-def    example.com    client-2
</code>
</pre>
{:codeblock}

From the example above, you can see consumer group `consumer-group-1` has 2 consumer members consuming messages from topic `foo` with 3 partitions. It also shows that the consumer `client-1-abc` that is consuming from partition `0` is 3 messages behind, because the current offset of the consumer is `264` but the offset of the last message on partition `0` is `267`. 

## Topics
{: #topics_tool }

You can use the **kafka-topics** tool with {{site.data.keyword.messagehub}}. Ensure that you use V2.3 of the tool, because it does not require Zookeeper access.

A scenario where you might want to use **kafka-topics** is to find out information about your topics and their configuration in an existing cluster, so that you can recreate them in a new cluster. You can use the information that is output from **kafka-topics** to create the same named topics in the new cluster. For more information about how to create topics, see [Using the administration Kafka Java client API](/docs/EventStreams?topic=EventStreams-kafka_java_api) or the 
[ibmcloud es topic-create command](/docs/EventStreams?topic=EventStreams-cli_reference#ibmcloud_es). Alternatively, you can also use the IBM {{site.data.keyword.messagehub}} console.

Here is some sample output from running the **kafka-topics** tool:

```
~/kafka_2.12-2.3.0 $ bin/kafka-topics.sh --bootstrap-server kafka03-prod01.messagehub.services.us-south.bluemix.net:9093 --command-config vcurr_dal06.properties --describe

Topic:sample-topic	PartitionCount:3	ReplicationFactor:3	 Configs:min.insync.replicas=2,unclean.leader.election.enable=true,retention.bytes=1073741824,segment.bytes=536870912,retention.ms=86400000
    Topic: sample-topic    Partition: 0    Leader: 0    Replicas: 0,2,1    Isr: 0,2,1
    Topic: sample-topic    Partition: 1    Leader: 1    Replicas: 1,2,0	   Isr: 0,2,1
    Topic: sample-topic    Partition: 2    Leader: 2    Replicas: 2,1,0	   Isr: 0,2,1
Topic:testtopic	 PartitionCount:1	 ReplicationFactor:3	Configs:min.insync.replicas=2,unclean.leader.election.enable=true,retention.bytes=1073741824,segment.bytes=536870912,retention.ms=86400000
    Topic: testtopic    Partition: 0    Leader: 0    Replicas: 0,2,1   Isr: 0,2
```
{: codeblock}

From the sample above, you can see that topic `sample-topic` has 3 partitions and a replication factor of 3. The example also shows which broker the leader of each partitions is on and which replicas are in sync (`Isr`). For example, the leader of partition `0`  is on broker `0`, the followers are on brokers `2` and `1` and all 3 replicas are in sync. If you look at the second topic `testtopic`, it has only 1 partition, replicated on brokers `0`, `2` and `1` but the in-sync replica list only shows `0` and `2`. This means the follower on broker `1` is falling behind and is therefore not in the `Isr` list. 


## Kafka Streams reset
{: #kafka_streams_reset }

You can use this tool with {{site.data.keyword.messagehub}} to reset the processing state of a Kafka Streams application, so you can reprocess its input from scratch. Before you run this tool, ensure that your Streams application is fully stopped.

For example:

<pre>
<code>
  $ kafka-streams-application-reset.sh --bootstrap-servers KAFKA_BROKERS_SASL --config-file CONFIG_FILE --application-id APP_ID
</code>
</pre>
{:codeblock}

Replace the following variables in the example with your own values:
* KAFKA_BROKERS_SASL with the value from your {{site.data.keyword.messagehub}} **Service Credentials** tab in the {{site.data.keyword.Bluemix_notm}} console, as a list of host:port pairs separated with commas (like `host1:port1,host2:port2`). 
* CONFIG_FILE with the path of the configuration file. 
* APP_ID with your Streams application ID.

