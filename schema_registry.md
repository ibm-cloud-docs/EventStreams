---

copyright:
  years: 2020, 2022
lastupdated: "2022-01-24"

keywords: IBM Event Streams, Schema Registry

subcollection: EventStreams

---

{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}


# {{site.data.keyword.messagehub}} Schema Registry
{: #ES_schema_registry}

## Schemas overview
{: #ES_overview}

Apache Kafka can handle any data, but it does not validate the information in the messages. However, efficient handling of data often requires that it includes specific information in a certain format. Using schemas, you can define the structure of the data in a message, ensuring that both producers and consumers use the correct structure.

Schemas help producers create data that conforms to a predefined structure, defining the fields that need to be present together with the type of each field. This definition then helps consumers parse that data and interpret it correctly. {{site.data.keyword.messagehub}} Enterprise plan supports schemas and includes a Schema Registry for using and managing schemas.

It is common for all of the messages on a topic to use the same schema. The key and value of a message can each be described by a schema.

![Schemas overview diagram.](schema_registry1.svg "Diagram representing how a schema can help define a structure for the key and value pairs of a message"){: caption="Schemas Overview"caption-side="bottom"}

## Schema registry
{: #ES_registry}

Schemas are stored in the {{site.data.keyword.messagehub}} Schema Registry. In addition to storing a versioned history of schemas, it provides an interface for retrieving them.
Each Enterprise plan {{site.data.keyword.messagehub}} instance has its own Schema Registry.

Producers and consumers validate the data against the specified schema stored in the Schema Registry (in addition to going through Kafka brokers). The schemas do not need to be transferred in the messages this way, meaning the messages can be smaller.

![Schema Registry architecture diagram.](schema_registry2.png "Diagram showing a Schema Registry architecture. A producer is sending messages and a consumer is reading messages, while both are retrieving the schema from the Schema Registry"){: caption="Schema registry architecture" caption-side="bottom"}

## Apache Avro data format
{: #ES_apache_avro_data_format}

Schemas are defined using [Apache Avro](https://avro.apache.org), an open-source data serialization technology commonly used with Apache Kafka. It provides an efficient data encoding format, either by using the compact binary format or a more verbose, but human-readable [JSON](https://www.json.org) format.

The {{site.data.keyword.messagehub}} Schema Registry uses Apache Avro data formats. When messages are sent in the Avro format, they contain the data and the unique identifier for the schema used. The identifier specifies which schema in the registry is to be used for the message.

Avro has support for a wide range of data types, including primitive types (null, boolean, int, long, float, double, bytes, and string) and complex types (record, enum, array, map, union, and fixed).

![Avro format diagram.](schema_registry3.svg "Diagram showing a representation of a message sent with the Avro format"){: caption="Avro message format" caption-side="bottom"}

## Serialization and deserialization
{: #ES_serialization_and_deserialization}

A producing application uses a serializer to produce messages conforming to a specific schema. As mentioned earlier, the message contains the data in Avro format, together with the schema identifier.

A consuming application then uses a deserializer to consume messages that have been serialized using the same schema. When a consumer reads a message sent in Avro format, the deserializer finds the identifier of the schema in the message, and retrieves the schema from the Schema Registry to deserialize the data.

This process provides an efficient way of ensuring that data in messages conform to the required structure.

The {{site.data.keyword.messagehub}} Schema Registry supports the [Kafka AVRO serializer and deserializer](https://github.com/confluentinc/schema-registry/tree/master/avro-serializer)
![Serialization and deserialization diagram.](schema_registry3.svg "Diagram showing a representation of where a serializer and deserializer fit into the {{site.data.keyword.messagehub}} architecture"){: caption="Serializer and deserializer" caption-side="bottom"}

## Versions and compatibility
{: #ES_versions_and_compatibility}

Whenever you add a schema, and any subsequent versions of the same schema, {{site.data.keyword.messagehub}} can validate the format automatically and reject the schema if there are any issues. You can evolve your schemas over time to accommodate changing requirements. You simply create a new version of an existing schema, and the Schema Registry ensures that the new version is compatible with the existing version, meaning that producers and consumers using the existing version are not broken by the new version.

Schemas are compared syntactically, meaning that other then minor textual formatting differences, schemas are considered matching only if they are textually the same, including all attribute ordering and descriptive fields. 

![Compatibility and versions diagram.](schema_registry4.svg "Diagram showing a representation of schema versions"){: caption="Compatibility and versions" caption-side="bottom"}

## Enabling the Schema Registry
{: #enabling_schema_registry}

The Schema Registry is enabled by default for {{site.data.keyword.messagehub}} Enterprise plan service instances.
The Schema Registry is not available for other {{site.data.keyword.messagehub}} plans.

## Accessing the Schema Registry
{: #accessing_schema_registry}

To access the Schema Registry, you need the URL of the Schema Registry, as well as a set of credentials that can be used to
authenticate with the registry. Both of these pieces of information can be found by inspecting the service credentials of your service.
To view these in the UI, click on your service instance, select **Service Credentials** in the left-hand navigation pane, then click on
the **View Credentials** link located next to one of the service credentials listed in the table:

![Service credentials diagram.](schema_registry8.png "Diagram showing a representation of the required credential fields for accessing {{site.data.keyword.messagehub}} Schema Registry"){: caption="Kafka credentials block" caption-side="bottom"}

You need the value of `kafka_http_url`, which is also the URL of the Schema Registry, and the value of `apikey` that you can use
as the credential for authenticating with the Schema Registry.

You can also authenticate using an API key that has been granted from a service ID, providing the service ID has a policy
that permits it at least “reader” role access to the {{site.data.keyword.messagehub}} instance. This approach is more flexible and is a better choice
if you are granting access to multiple other people or teams. See the [Managing access to your {{site.data.keyword.messagehub}} resources](/docs/services/EventStreams?topic=eventstreams-security) help topic for more details.

The curl command to use is as follows (where $APIKEY is substituted with your API key, and $URL is substituted with the URL from the
Kafka HTTP URL property of the service credentials):

```text
curl -i –u token:$APIKEY $URL/artifacts
```

Assuming you haven’t already used the Schema Registry, you should see the following output that indicates that there are no schemas
stored in the registry:

```text
HTTP/1.1 200 OK
Date: Thu, 16 Jan 2020 15:45:26 GMT
Content-Type: application/json
Content-Length: 11
Connection: keep-alive
[]
```

## Schema registry REST endpoints
{: #schema_registry_rest_endpoints}

The REST API offers four main capabilities:

1. Creating, reading, and deleting schemas.
2. Creating, reading, and deleting individual versions of a schema.
3. Reading and updating the global compatibility rule for the registry.
4. Creating, reading, updating, and deleting compatibility rules that apply to individual schemas.

For actions that alter the schema version, such as create, update, or delete artifact, artifact versions and rules, an activity tracker event is generated to report the action. For more information, see [{{site.data.keyword.cloudaccesstrailshort}} events](/docs/EventStreams?topic=EventStreams-at_events#events).

### Authentication
{: #authentication}

As described above, you can authenticate to the Schema Registry using an API key. This is supplied as the password portion of a HTTP basic authentication header. Set the username portion of this header to the word “token”. It is also possible to grant a bearer token for a system ID or user and supply this as a credential. To do this specify an HTTP header in the format: “Authorization: Bearer $TOKEN” (where $TOKEN is the bearer token).
For example:

```text
curl –H "Authorization: Bearer $TOKEN" ...
```

### Errors
{: #errors}

If an error condition is encountered, the Schema Registry will return a non-2XX range HTTP status code. The body of the response will contain a JSON object in the following form:

```text
{
    "error_code":404,
    "message":"No artifact with id 'my-schema' could be found."
}
```

The properties of the error JSON object are as follows:

Property name | Description
--- | ---
error_code | The HTTP status code of the response.
message | A description of the cause of the problem.
incident | This field is only included if the error is a result of a problem with the Schema Registry. This value can be used by IBM service to correlate a request to diagnostic information captured by the registry.

### Create a schema
{: #create_schema}

This endpoint is used to store a schema in the registry. The schema data is sent as the body of the POST request. An ID for the schema can be included using the ‘X-Registry-ArtifactId' request header. If this header is not present in the request, an ID will be generated. The content type header must be set to “application/json”.

Example curl request:

```text
curl -u token:$APIKEY -H 'Content-Type: application/json' -H 'X-Registry-ArtifactId: my-schema' $URL/artifacts -d '{"type":"record","name":"Citizen","fields":[{"name": "firstName","type":"string"},{"name":"lastName","type":"string"},{"name":"age","type":"int"},{"name":"phoneNumber","type":"string"}]}'
```

Example response:

```text
{"id":"my-schema","type":"AVRO","version":1,"createdBy":"","createdOn":1579267788258,"modifiedBy":"","modifiedOn":1579267788258,"globalId":75}
```

Creating a schema requires at least both:

- Reader role access to the {{site.data.keyword.messagehub}} cluster resource type.
- Writer role access to the schema resource that matches the schema being created.

An activity tracker event is generated to report the action. For more information, see [{{site.data.keyword.cloudaccesstrailshort}} events](/docs/EventStreams?topic=EventStreams-at_events#events).

### List schemas
{: #list_schemas}

You can generate a list of the IDs of all of the schemas stored in the registry by making a GET request to the /artifacts endpoint.

Example curl request:

```text
curl -u token:$APIKEY $URL/artifacts
```

Example response:

```text
["my-schema"]
```

Listing schemas requires at least:

- Reader role access to the {{site.data.keyword.messagehub}} cluster resource type.

### Delete a schema
{: #delete_schema}

Schemas are deleted from the registry by issuing a DELETE request to the /artifacts/{schema-id} endpoint (where {schema-id} is the ID of the schema). If successful, an empty response and a status code of 204 (no content) is returned.

Example curl request:

```text
curl -u token:$APIKEY –X DELETE $URL/artifacts/my-schema
```

Deleting a schema requires at least both:

- Reader role access to the {{site.data.keyword.messagehub}} cluster resource type.
- Manager role access to the schema resource that matches the schema being deleted.

An activity tracker event is generated to report the action. For more information, see [{{site.data.keyword.cloudaccesstrailshort}} events](/docs/EventStreams?topic=EventStreams-at_events#events).

### Create a new version of a schema
{: #new_schema}

To create a new version of a schema, make a POST request to the /artifacts/{schema-id}/versions endpoint, (where {schema-id} is the ID of the schema). The body of the request must contain the new version of the schema.

If the request is successful, the new schema version is created as the new latest version of the schema, with an appropriate version number, and a response with status code 200 (OK) and a payload containing metadata describing the new version (including the version number), is returned.

Example curl request:

```text
curl -u token:$APIKEY -H 'Content-Type: application/json' $URL/artifacts/my-schema/versions -d '{"type":"record","name":"Citizen","fields":[{"name": "firstName","type":"string"},{"name":"lastName","type":"string"},{"name":"age","type":"int"},{"name":"phoneNumber","type":"string"}]}'
```

Example response:

```text
{"id":"my-schema","type":"AVRO","version":2,"createdBy":"","createdOn": 1579267978382,"modifiedBy":"","modifiedOn":1579267978382,"globalId":83}
```

Creating a new version of a schema requires at least both:

- Reader role access to the {{site.data.keyword.messagehub}} cluster resource type.
- Writer role access to the schema resource that matches the schema getting a new version.

An activity tracker event is generated to report the action. For more information, see [{{site.data.keyword.cloudaccesstrailshort}} events](/docs/EventStreams?topic=EventStreams-at_events#events).

### Get the latest version of a schema
{: #latest_schema}

To retrieve the latest version of a particular schema, make a GET request to the /artifacts/{schema-id} endpoint, (where {schema-id} is the ID of the schema). If successful, the latest version of the schema is returned in the payload of the response.

Example curl request:

```text
curl -u token:$APIKEY $URL/artifacts/my-schema
```

Example response:

```text
{"type":"record","name":"Citizen","fields":[{"name": "firstName","type":"string"},{"name":"lastName","type":"string"},{"name":"age","type":"int"},{"name":"phoneNumber","type":"string"}]}
```

Getting the latest version of a schema requires at least both:

- Reader role access to the {{site.data.keyword.messagehub}} cluster resource type.
- Reader role access to the schema resource that matches the schema being retrieved.

### Getting a specific version of a schema
{: #schema_version}

To retrieve a specific version of a schema, make a GET request to the /artifacts/{schema-id}/versions/{version} endpoint, (where {schema-id} is the ID of the schema, and {version} is the version number of the specific version you need to retrieve). If successful, the specified version of the schema is returned in the payload of the response.

Example curl request

```text
curl -u token:$APIKEY $URL/artifacts/my-schema/versions/3
```

Example response:

```text
{"type":"record","name":"Citizen","fields":[{"name": "firstName","type":"string"},{"name":"lastName","type":"string"},{"name":"age","type":"int"},{"name":"phoneNumber","type":"string"}]}
```

Getting the latest version of a schema requires at least both:

- Reader role access to the {{site.data.keyword.messagehub}} cluster resource type.
- Reader role access to the schema resource that matches the schema being retrieved.

### Listing all of the versions of a schema
{: #list_schemas}

To list all versions of a schema currently stored in the registry, make a GET request to the /artifacts/{schema-id}/versions endpoint, (where {schema-id} is the ID of the schema). If successful, a list of all current version numbers for the schema is returned in the payload of the response.

Example curl request:

```text
curl -u token:$APIKEY $URL/artifacts/my-schema/versions
```

Example response:

```text
[1,2,3,5,6,8,100]
```

Getting the list of available versions of a schema requires at least both:

- Reader role access to the {{site.data.keyword.messagehub}} cluster resource type.
- Reader role access to the schema resource that matches the schema being retrieved.

### Deleting a version of a schema
{: #delete_schema}

Schema versions are deleted from the registry by issuing a DELETE request to the /artifacts/{schema-id}/versions/{version} endpoint (where {schema-id} is the ID of the schema, and {version} is the version number of the schema version). If successful, an empty response, and a status code of 204 (no content) is returned. Deleting the only remaining version of a schema will also delete the schema.

Example curl request:

```text
curl -u token:$APIKEY –X DELETE $URL/artifacts/my-schema/versions/3
```

Deleting a schema version requires at least both:

- Reader role access to the {{site.data.keyword.messagehub}} cluster resource type.
- Manager role access to the schema resource that matches the schema being deleted.

An activity tracker event is generated to report the action. For more information, see [{{site.data.keyword.cloudaccesstrailshort}} events](/docs/EventStreams?topic=EventStreams-at_events#events).

### Updating a global rule
{: #global_rule}

Global compatibility rules can be updated by issuing a PUT request to the /rules/{rule-type} endpoint, (where {rule-type} identifies the type of global rule to be updated - currently the only supported type is COMPATIBILITY), with the new rule configuration in the body of the request. If the request is successful, the newly updated rule config is returned in the payload of the response, together with a status code of 200 (OK).

The JSON document sent in the request body must have the following properties:

Property name | Description
--- | ---
type | Must always be set to the value COMPATIBILITY.
config | Must be set to one of the following values: NONE, BACKWARD, BACKWARD_TRANSITIVE, FORWARD, FORWARD_TRANSITIVE, FULL, or FULL_TRANSITIVE (See the section on [compatibility rules](/docs/EventStreams?topic=EventStreams-ES_schema_registry#applying_compatibility_rules) for details on each of these values).

Example curl request:

```text
curl -u token:$APIKEY –X PUT $URL/rules/COMPATIBILITY -d '{"type":"COMPATIBILITY","config":"BACKWARD"}'
```

Example response:

```text
{"type":"COMPATIBILITY","config":"BACKWARD"}
```

Updating a global rule configuration requires at least:

- Manager role access to the {{site.data.keyword.messagehub}} cluster resource type.

An activity tracker event is generated to report the action. For more information, see [{{site.data.keyword.cloudaccesstrailshort}} events](/docs/EventStreams?topic=EventStreams-at_events#events).

### Getting the current value of a global rule
{: #global_rule}

The current value of a global rule is retrieved by issuing a GET request to the /rules/{rule-type} endpoint, (where {rule-type} is the type of global rule to be retrieved - currently the only supported type is COMPATIBILITY). If the request is successful, the current rule configuration is returned in the payload of the response, together with a status code of 200 (OK).

Example curl request:

```text
curl -u token:$APIKEY $URL/rules/COMPATIBILITY
```

Example response:

```text
{"type":"COMPATIBILITY","config":"BACKWARD"}
```

Getting global rule configuration requires at least:

- Reader role access to the {{site.data.keyword.messagehub}} cluster resource type.

### Creating a per-schema rule
{: #schema_rule}

Rules can be applied to a specific schema, overriding any global rules that have been set, by making a POST request to the /artifacts/{schema-id}/rules endpoint, (where {schema-id} is the ID of the schema), with the type and value of the new rule contained in the body of the request, (currently the only supported type is COMPATIBILITY). If successful, an empty response and a status code of 204 (no content) are returned.

Example curl request:

```text
curl -u token:$APIKEY $URL/artifacts/my-schema/rules -d '{"type":"COMPATIBILITY","config":"FORWARD"}'
```

Creating per-schema rules requires at least:

- Reader role access to the {{site.data.keyword.messagehub}} cluster resource type.
- Manager role access to the schema resource for which the rule will apply.

An activity tracker event is generated to report the action. For more information, see [{{site.data.keyword.cloudaccesstrailshort}} events](/docs/EventStreams?topic=EventStreams-at_events#events).
 
### Getting a per-schema rule
{: #get_rule}

To retrieve the current value of a type of rule being applied to a specific schema, a GET request is made to the /artifacts/{schema-id}/rules/{rule-type} endpoint, (where {schema-id} is the ID of the schema, and {rule-type} is the type of global rule to be retrieved - currently the only supported type is COMPATIBILITY). If the request is successful, the current rule value is returned in the payload of the response, together with a status code of 200 (OK).

Example curl request:

```text
curl -u token:$APIKEY $URL/artifacts/my-schema/rules/COMPATIBILITY
```

Example response:

```text
{"type":"COMPATIBILITY","config":"FORWARD"}
```

Getting per-schema rules requires at least:

- Reader role access to the {{site.data.keyword.messagehub}} cluster resource type.
- Reader role access to the schema resource to which the rule applies.

### Updating a per-schema rule
{: #update_rule}

The rules applied to a specific schema are modified by making a PUT request to the /artifacts/{schema-id}/rules/{rule-type} endpoint, (where {schema-id} is the ID of the schema, and {rule-type} is the type of global rule to be retrieved - currently the only supported type is COMPATIBILITY). If the request is successful, the newly updated rule config is returned in the payload of the response, together with a status code of 200 (OK).

Example curl request:

```text
curl -u token:$APIKEY –X PUT $URL/artifacts/my-schema/rules/COMPATIBILITY -d '{"type":"COMPATIBILITY","config":"BACKWARD"}'
```

Example response:

```text
{"type":"COMPATIBILITY","config":"BACKWARD"}
```

Updating a per-schema rule requires at least:

- Reader role access to the {{site.data.keyword.messagehub}} cluster resource type.
- Manager role access to the schema resource to which the rule applies.

An activity tracker event is generated to report the action. For more information, see [{{site.data.keyword.cloudaccesstrailshort}} events](/docs/EventStreams?topic=EventStreams-at_events#events).

### Deleting a per-schema rule
{: #delete_rule}

The rules applied to a specific schema are deleted by making a DELETE request to the /artifacts/{schema-id}/rules/{rule-type} endpoint,
(where {schema-id} is the ID of the schema, and {rule-type} is the type of global rule to be retrieved - currently the only supported type is COMPATIBILITY). If the request is successful, an empty response is returned, with a status code of 204 (no content).

Example curl request:

```text
curl -u token:$APIKEY –X DELETE $URL/artifacts/my-schema/rules/COMPATIBILITY
```

Deleting a per-schema rule requires at least:

- Reader role access to the {{site.data.keyword.messagehub}} cluster resource type.
- Manager role access to the schema resource to which the rule applies.

An activity tracker event is generated to report the action. For more information, see [{{site.data.keyword.cloudaccesstrailshort}} events](/docs/EventStreams?topic=EventStreams-at_events#events).

## Applying compatibility rules to new versions of schemas
{: #applying_compatibility_rules}

The Schema Registry supports enforcing compatibility rules when creating a new version of a schema. If a request is made to create a new schema version that does not conform to the required compatibility rule, the registry rejects the request. The following rules are supported:

Compatibility Rule | Tested against | Description
--- | --- | ---
NONE | N/A | No compatibility checking is performed when a new schema version is created.
BACKWARD | Latest version of the schema | A new version of the schema can omit fields that are present in the existing version of the schema.
BACKWARD_TRANSITIVE | All versions of the schema | A new version of the schema can add optional fields that are not present in the existing version of the schema.
FORWARD | Latest version of the schema | A new version of the schema can add fields that are not present in the existing version of the schema.
FORWARD_TRANSITIVE | All versions of the schema | A new version of the schema can omit optional fields that are present in the existing version of the schema.
FULL | Latest version of the schema | A new version of the schema can add optional fields that are not present in the existing version of the schema.
FULL_TRANSITIVE | All versions of the schema | A new version of the schema can omit optional fields that are present in the existing version of the schema.

These rules can be applied at two scopes:

1. At a global scope, which is the default that is used when creating a new schema version.
2. At a per-schema level. If a per-schema level rule is defined, it overrides the global default for the particular schema.

By default, the registry has a global compatibility rule setting of `NONE`. Per-schema level rules must be defined, otherwise the schema will default to using the global setting.

## Full API description
{: full_api_description}

For a description of the REST API with examples, see 
[{{site.data.keyword.messagehub}} schema-registry-rest](https://github.com/ibm-messaging/event-streams-docs/tree/master/schema-registry-api){: external}.

You can download the full specification for the API from the [{{site.data.keyword.messagehub}} Schema Registry REST API YAML file](https://github.com/ibm-messaging/event-streams-docs/blob/master/schema-registry-api/openapi.yaml){: external}.
To view the Swagger file, use Swagger tools, for example [Swagger editor](http://editor.swagger.io/#/){: external}.

For details about accessing the Schema Registry using an SDK, see [{{site.data.keyword.messagehub}} Schema Registry REST API](https://github.com/IBM/eventstreams-go-sdk/blob/main/schema_operations.md){: external}.

For information about {{site.data.keyword.messagehub}} resources and data sources on Terraform, see [resources and data sources](https://cloud.ibm.com/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-index-of-terraform-on-ibm-cloud-resources-and-data-sources#ibm-event-streams_rd){: external}.

## Using the Schema Registry with the third party SerDes
{: #using_schema_registry_serdes}

Schema Registry supports the use of the following third party SerDes:

- Confluent SerDes

To configure the Confluent SerDes to use the Schema Registry, you need to specify two properties in the configuration of your Kafka client:

Property name | Value
--- | ---
SCHEMA_REGISTRY_URL_CONFIG | Set this to the URL of the Schema Registry, including your credentials as basic authentication, and with a path of ```/confluent```. For example, if ```$APIKEY``` is the API key to use and ```$HOST``` is the host from the ```kafka_http_url``` field in the **Service Credentials** tab, the value has the form:

```text
https://token:{$APIKEY}@{$HOST}/{confluent}
```
{: screen}

BASIC_AUTH_CREDENTIALS_SOURCE | Set to ```URL```. This instructs the SerDes to use HTTP basic authentication using the credentials supplied in the Schema Registry URL.

You can also optionally provide the following properties to control the schema selection (subject naming strategy):

Property name | Value
--- | ---
VALUE_SUBJECT_NAME_STRATEGY | `TopicNameStrategy`(default), `RecordNameStrategy`, and `TopicRecordNameStrategy` are supported. For example, to specify that the schema for the message value is selected using a `TopicRecordNameStrategy`, you could use the following client properties: configs.put(KafkaAvroSerializerConfig.VALUE_SUBJECT_NAME_STRATEGY, TopicRecordNameStrategy.class.getName());
KEY_SUBJECT_NAME_STRATEGY | `TopicNameStrategy` (default), `RecordNameStrategy`, and `TopicRecordNameStrategy` are supported. See VALUE_SUBJECT_NAME_STRATEGY for an example.

The following diagram shows an example of the properties required to create a Kafka producer, that uses the Confluent SerDes and can be connected to the {{site.data.keyword.messagehub}} service:


![Kafka properties for Confluent Serdes](schema_registry7.png "Diagram showing showing the properties required to create a Kafka producer that uses the Confluent SerDes, and can be connected to the {{site.data.keyword.messagehub}} service"){: caption="Figure 1. Kafka properties for Confluent Serdes" caption-side="bottom"}

If a message is sent using a schema that isn’t in the registry, the SerDes attempts to create the new schema, or version of the schema, in the registry. If this behaviour is not required, it can be disabled by removing the writer permission for schema resources from the application. See [Managing access to the schema registry](/docs/EventStreams?topic=EventStreams-security#managing_access_schemas).

The *normalize* option for schema lookups and registration is not supported.
{: note}

## Using the Schema Registry with third party tools
{: #third_party}

The Schema Registry can be tested with third party tools, such as the `kafka-avro-console-producer.sh` and `kafka-avro-console-consumer.sh`, that allow testing of conformance to schema using the Confluent SerDes.

To run either the producer or the consumer tool, a common properties is required with the connection options for the {{site.data.keyword.messagehub}} Enterprise instance.


```text
sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="token" password="apikey";
security.protocol=SASL_SSL
sasl.mechanism=PLAIN
ssl.protocol=TLSv1.2
ssl.enabled.protocols=TLSv1.2
ssl.endpoint.identification.algorithm=HTTPS
```
{: codeblock}

## Avro console producer and consumer
{: #avro_console_producer }

You can use the Kafka avro console producer and consumer tools with {{site.data.keyword.messagehub}}. You must provide a client properties, as detailed above, and in addition, the connection method and credentials for the Schema Registry are required to be supplied as command line `--property` arguments. There are two connection methods using a credentials source of USER_INFO or of URL detailed below.

To execute using the credentials source method of URL, use the following code:

```text
    ./kafka-avro-console-[producer|consumer] --broker-list $KAFKA_BROKERS_SASL --topic schema-test --property schema.registry.url=$SCHEMA_REGISTRY_URL --property value.schema='{"type":"record","name":"myrecord","fields":[{"name":"f1","type":"string"}]}' --property basic.auth.credentials.source=URL --producer.config $CONFIG_FILE
```
{: codeblock}

Replace the following variables in the example with your own values:
* KAFKA_BROKERS_SASL with the value from your {{site.data.keyword.messagehub}} **Service Credentials** tab in the {{site.data.keyword.Bluemix_notm}} console, as a list of host:port pairs separated with commas (for example, `host1:port1,host2:port2`). 
* SCHEMA_REGISTRY_URL with the `kafka_http_url` value from your {{site.data.keyword.messagehub}} **Service Credentials** tab in the {{site.data.keyword.Bluemix_notm}} console, with the username `token` and apikey, along with the path `/confluent` (for example, `https://{token}:{apikey}@{kafka_http_url}/{confluent}`).
* CONFIG_FILE with the path of the configuration file. 

To execute using the credentials source method of USER_INFO, use the following code:

```text
    ./kafka-avro-console-[producer|consumer] --broker-list $KAFKA_BROKERS_SASL --topic schema-test --property schema.registry.url=$SCHEMA_REGISTRY_URL --property value.schema='{"type":"record","name":"myrecord","fields":[{"name":"f1","type":"string"}]}' --property basic.auth.credentials.source=USER_INFO --property basic.auth.user.info=token:apikey --producer.config $CONFIG_FILE
```
{: codeblock}

Replace the following variables in the example with your own values:
* KAFKA_BROKERS_SASL with the value from your {{site.data.keyword.messagehub}} **Service Credentials** tab in the {{site.data.keyword.Bluemix_notm}} console, as a list of host:port pairs separated with commas (for example, `host1:port1,host2:port2`). 
* SCHEMA_REGISTRY_URL with the `kafka_http_url` value from your {{site.data.keyword.messagehub}} **Service Credentials** tab in the {{site.data.keyword.Bluemix_notm}} console, with the path `/confluent` (for example, `https://{kafka_http_url}/{confluent}`).
* CONFIG_FILE with the path of the configuration file. 

