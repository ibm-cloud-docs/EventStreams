---

copyright:
  years: 2015, 2020
lastupdated: "2022-02-07"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: EventStreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}

# Using the REST producer API
{: #rest_producer_using}


**The REST producer API is available as part of the {{site.data.keyword.messagehub}} Standard and Enterprise plans only.**

{{site.data.keyword.messagehub}} provides a REST API to help connect your existing systems to your {{site.data.keyword.messagehub}} Kafka cluster. Using the API, you can integrate {{site.data.keyword.messagehub}} with any system that supports RESTful APIs.

The REST producer API is a scalable REST interface for producing messages to {{site.data.keyword.messagehub}} over a secure HTTP endpoint. Send event data to {{site.data.keyword.messagehub}}, utilize Kafka technology to handle data feeds, and take advantage of {{site.data.keyword.messagehub}} features to manage your data.

Use the API to connect existing systems to {{site.data.keyword.messagehub}}. Create produce requests from your systems into {{site.data.keyword.messagehub}}, including specifying the message key, headers, and the topics that you want to write messages to.


## Accessing the REST producer API:
{: #rest_produce_access}
You must retrieve the URL and credential details that are needed to connect to the API from a Service credentials object or service key for the service instance. For information about creating these objects, see 
[Connecting to {{site.data.keyword.messagehub}}](/docs/EventStreams?topic=EventStreams-connecting).

The URL for the API's endpoint is provided in the ```kafka_http_url``` property.

Use one of the following methods to authenticate:

* **To authenticate using Basic Auth:**<br/> 
    Use the <code>user</code> and <code>api_key</code> properties of the above objects as the username and password. Place these values into the <code>Authorization</code> header of the HTTP request in the form <code>Basic &lt;base64 encoding of username and password joined by a single colon (:)&gt;</code>.

* **To authenticate using a bearer token:**<br/> 
    To obtain your token using the IBM Cloud CLI, first log in to IBM Cloud then run the following command: 

    ```
    ibmcloud iam oauth-tokens
    ```
    {: codeblock}

    Place this token in the Authorization header of the HTTP request in the form <code>Bearer<token></code>. Both API key or JWT tokens are supported. 

* **To authenticate directly using the api_key:**<br/> 
    Place the key directly as the value of the <code>X-Auth-Token</code> HTTP header.

## Producing messages using the REST producer API
{: #rest_produce_messages}

Use the producer API to write messages to topics. To be able to produce to a topic, you must have the following information available:

* The URL of the {{site.data.keyword.messagehub}} API endpoint, including the port number.
* The topic you want to produce to.
* The API key that gives permission to connect and produce to the selected topic.

<br/>
The following code shows an example of sending a message using curl:

```
curl -v -X POST -H "Authorization: Basic <base64 username:password>" -H "Content-Type: text/plain" -H "Accept: application/json" -d 'test message' "<kafka_http_url>/topics/<topic_name>/records"
```
{: codeblock}

## Producing messages using the v2 endpoint of REST producer API
{: #rest_produce_messages}

The v2 endpoint of REST producer API allows you to produce a message that conforms to a schema. The serializer currently supported is "Confluent". The schemas are created and stored in {{site.data.keyword.messagehub}} Schema Registry. For more details, see [{{site.data.keyword.messagehub}} Schema Registry](/docs/EventStreams?topic=ES_schema_registry).

* **Schema naming strategy:**<br/> 

    The allowed schema naming strategy are Topic, Record and TopicRecord. 

    * Topic naming strategy uses the name of the topic to derive the schema artifact id. The id would be of form "\<topicName\>-key" for key and "\<topicName\>-value" for value, where "topicName" is the name of topic.

    * Record naming strategy uses the name of the record in the schema to derive the schema artifact id. The id would be of form "\<recordName\>-key" for key and "\<recordName\>-value" for value, where "recordName" is the name of the record in the schema.

    * TopicRecord naming strategy uses both name of the topic and record to derive the schema artifact id. The id would be of form "\<topicName\>-\<recordName\>-key" for key and "\<topicName\>-\<recordName\>-value" for value, where "topicName" is the name of topic and "recordName" is the name of the record in the schema.

The v2 endpoint also supports producing messages of type Text, binary or JSON, similar to that of existing API.

<br/>
The following code shows an example of sending a message of Text type using curl:

```
curl -v -X POST -H "Authorization: Basic <base64 username:password>" -H "Content-Type: text/json" -H "Accept: application/json" \
"<kafka_http_url>/v2/topics/<topic_name>/records" \
-d '{
  "headers": [
    {
      "name": "colour",
      "value": "YmxhY2s="
    }
  ],
  "key": {
    "type": "text",
    "data": "Test Key"
  },
  "value": {
    "type": "text",
    "data": "Test Value"
  }
}'
```
{: codeblock}


<br/>
The following code shows an example of sending a message conforming to schema of type avro using curl:

```
curl -v -X POST -H "Authorization: Basic <base64 username:password>" -H "Content-Type: text/json" -H "Accept: application/json" \
"<kafka_http_url>/v2/topics/<topic_name>/records?serializer=confluent" \
-d '{
  "value": {
    "type": "avro",
    "schema": "{\"namespace\": \"com.eventstreams.samples\",\"type\": \"record\",\"name\": \"recordValueName\",\"fields\": [{\"name\": \"valueName\", \"type\": \"string\"}]}",
    "schema_name_strategy": "topic",
    "data": "{\"valueName\": \"sampleValueName\"}"
  }
}' 

```
{: codeblock}


## Migrating from existing endpoint to the v2 end point of the REST producer API
Below are the considerations to help you plan the migration: <br>
1. Accessing the REST producer API: <br>
    The v2 endpoint can be accessed in the same way as the existing URL, see the above section [Accessing REST producer API](/docs/EventStreams?topic=rest_produce_access).
2. V2 endpoint: <br>
    The v2 endpoint to be used to produce the data is `/v2/topics/<topic_name>/records`
3. Query Parameter: <br>
    The query parameter "serializer" is optional. It is required only when you want the message to conform to a schema.
4. Headers: <br>
    The Content-Type header should be provided with the value "application/json".
5. Payload: <br>
    The payload for v2 endpoint should be provided in JSON format. The message payload you have been sending using the existing endpoint should now be specified under "value.data". The data type should also be mentioned under "value.type". The message key and message headers are optional and can be provided under "key" and "headers" respectively.

## Limitations

When using the REST producer API, there is a limitation on the record key and value size. These limitations are as follows:
* Maximum key size is 4 K 
* Maximum value size is 64 K

## API reference
{: #rest_api_reference}

For full details of the API, see the 
[{{site.data.keyword.messagehub}} REST Producer API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/apidocs/event-streams){: new_window}.
