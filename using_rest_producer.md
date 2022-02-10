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

## Authentication:
{: #rest_produce_authenticate}
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

Use the v2 endpoint `/v2/topics/{topic_name}/record` to send messages of type text, binary, JSON or avro. It allows you to use Event Streams Schema Registry by specifying the schema for avro data type.

<br/>

The following code shows an example of sending a message of text type using curl:

```
curl -v -X POST –H "Authorization: Bearer $TOKEN" -H "Content-Type: application/json" -H "Accept: application/json" -d '{"headers":[{"name":"colour","value":"YmxhY2s="}],"key":{"type":"text","data":"Test Key"},"value":{"type":"text","data":"Test Value"}}' "$<kafka_http_url>/v2/topics/<topic_name>/records"
```
{: codeblock}

## Migrating from existing endpoint to the v2 end point of the REST producer API
Below are the considerations to help you plan the migration: <br>
1. Accessing the REST producer API: <br>
    The v2 endpoint can be accessed in the same way as the existing URL, i.e by obtaining the value of `kafka_http_url` property for the service instance. The path to be used is `/v2/topics/<topic_name>/records`.
    
       Example URL: https://service-instance-adsf1234asdf1234asdf1234-0000.us-south.containers.appdomain.cloud/v2/topics/topic_name/records
3. Authentication: <br>
    The supported authentication mechanism is a bearer token.
    
       Example Header:  –H "Authorization: Bearer $TOKEN"
3. Query Parameter: <br>
    The optional query parameter `serializer` can be provided only when you want the message to conform to a schema. Currently, the only supported value is `confluent`.

       Example URL: https://service-instance-adsf1234asdf1234asdf1234-0000.us-south.containers.appdomain.cloud/v2/topics/topic_name/records?searializer=confluent
4. Headers: <br>
    The Content-Type and the Accept headers should be provided with the value `application/json`.
    
       Example Headers:  –H "Content-Type: application/json" -H "Accept: application/json"
5. Payload: <br>
    The payload for v2 endpoint should be provided in JSON format. The message key, headers and data can be defined in the payload. The headers can be specified in the form of a list, whose values should be base64 encoded. The message key and headers are however optional.
    
       Example Payload:
       {
         "headers": [
         {
          "name": "colour",
          "value": "YmxhY2s="
         },
         "key": {
          "type": "text",
          "data": "Test Key"
         },
         "value": {
          "type": "text",
          "data": "Test Value"
         }
        }
    The maximum size of the payload is limited to 64K.
6. Error Response: <br>
    The error response contains `trace`,  `error message`, `error code`, `more_info` and `target` properties.

       Example error response:
       {
        "trace": "a222e93c-e5f9-435d-b275-5d4919ea87ed",
        "error": {
         "code": "invalid_type",
         "message": "Error parsing JSON request body: 'type' field in 'value' object is required",
         "more_info": "https://cloud.ibm.com/apidocs/event-streams/restproducer",
         "target": {
          "type": "field",
          "name": "type"
         }
        }
       }

## Producing messages conforming to a schema:
The v2 endpoint of REST producer API also allows you to produce a message in such a way that message key and value are conforming to a schema. You can specify different schemas for key and value. The serializer currently supported is `confluent` and the data type supported is `avro`. The schemas are created and stored in {{site.data.keyword.messagehub}} Schema Registry. For more details, see [{{site.data.keyword.messagehub}} Schema Registry](/docs/EventStreams?topic=ES_schema_registry).

The following are the schema naming strategies allowed:

  * Topic naming strategy: The name of the topic is used to derive the schema artifact id. The id would be of form "\<topicName\>-key" for key and "\<topicName\>-value" for value, where "topicName" is the name of topic.

  * Record naming strategy: The name of the record in the schema is used to derive the schema artifact id. The id would be of form "\<recordName\>-key" for key and "\<recordName\>-value" for value, where "recordName" is the name of the record in the schema.

  * TopicRecord naming strategy: Both the name of the topic and record are used to derive the schema artifact id. The id would be of form "\<topicName\>-\<recordName\>-key" for key and "\<topicName\>-\<recordName\>-value" for value, where "topicName" is the name of topic and "recordName" is the name of the record in the schema.

<br/>
The following code shows an example of sending a message conforming to a schema using curl:

```
curl -v -X POST –H "Authorization: Bearer $TOKEN" -H "Accept: application/json" -d '{"value":{"type":"avro","schema":"{\"namespace\": \"com.eventstreams.samples\",\"type\": \"record\",\"name\": \"recordValueName\",\"fields\": [{\"name\": \"valueName\", \"type\": \"string\"}]}","schema_name_strategy":"topic","data":"{\"valueName\": \"sampleValueName\"}"}}' "<kafka_http_url>/v2/topics/<topic_name>/records?serializer=confluent"

```

{: codeblock}
## API reference
{: #rest_api_reference}

For full details of the API, see the 
[{{site.data.keyword.messagehub}} REST Producer API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/apidocs/event-streams/restproducer){: new_window}.
