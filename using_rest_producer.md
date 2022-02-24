---

copyright:
  years: 2015, 2020
lastupdated: "2022-02-23"

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
The supported authentication mechanism is to use a bearer token. To obtain your token using the IBM Cloud CLI, first log in to IBM Cloud, then run the following command: 

```
ibmcloud iam oauth-tokens
```
{: codeblock}

Place this token in the Authorization header of the HTTP request in the form <code>Bearer<token></code>. Both API key or JWT tokens are supported. 

## Producing messages using the REST producer API
{: #rest_produce_messages}

Use the v2 endpoint of the producer API to send messages of type text, binary, JSON, or avro to topics. It allows you to use the {{site.data.keyword.messagehub}} Schema Registry by specifying the schema for the avro data type.

<br/>

The following code shows an example of sending a message of text type using curl:

```
curl -v -X POST \
–H "Authorization: Bearer $token" -H "Content-Type: application/json" -H "Accept: application/json" \
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
}' \
"$kafka_http_url/v2/topics/$topic_name/records"
```
{: codeblock}

For full details of the API reference, see the 
[{{site.data.keyword.messagehub}} REST Producer API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/apidocs/event-streams/restproducer_v2){: new_window}.

## Producing messages conforming to a schema:
The v2 endpoint of REST producer API also allows you to produce a message in a way that message key and value conform to a schema. You can specify different schemas for key and value. The serializer that is currently supported is `confluent` and the data type supported is `avro`. The schemas are created and stored in {{site.data.keyword.messagehub}} Schema Registry. For more details, see [{{site.data.keyword.messagehub}} Schema Registry](/docs/EventStreams?topic=ES_schema_registry).

The following the schema naming strategies are allowed:

  * Topic naming strategy: The name of the topic is used to derive the schema artifact id. The id would be of form "\<topicName\>-key" for key and "\<topicName\>-value" for value, where topicName is the name of topic.

  * Record naming strategy: The name of the record in the schema is used to derive the schema artifact id. The id would be of form 
  "\<composite-recordName\>-key for key and "<composite-recordName\>-value for value. If the schema namespace field is specified, the composite-recordName takes the value of "\<namespace\>.\<recordName\>", otherwise it takes the value of "\<recordName\>.

  * TopicRecord naming strategy: Both the name of the topic and record are used to derive the schema artifact id. The id would be of form "\<topicName\>-\<recordName\>-key" for key and "\<topicName\>-\<composite-recordName\>-value" for value, where topicName is the name of topic. If the schema namespace field is specified, the composite-recordName takes the value of "\<namespace\>.\<recordName\>", otherwise it takes the value of "\<recordName\>.

<br/>

The following code shows an example of sending a message conforming to a schema, that is specified under `schema` field using curl:

```
curl -v -X POST \
–H "Authorization: Bearer $token" -H "Content-Type: application/json" -H "Accept: application/json" \
-d '{
  "value": {
    "type": "avro",
    "schema": "{\"namespace\": \"com.eventstreams.samples\",\"type\": \"record\",\"name\": \"recordValueName\",\"fields\": [{\"name\": \"valueName\", \"type\": \"string\"}]}",
    "schema_name_strategy": "record",
    "data": "{\"valueName\": \"sampleValueName\"}"
  }
}' \
"$kafka_http_url/v2/topics/$topic_name/records?serializer=confluent"
```
{: codeblock}

## Migrating from existing endpoint to the v2 end point of the REST producer API
Several improvements have been made to the v2 endpoint for better usage and to align with the API standards. To make the most of these improvements, you should make changes to the existing applications.

Below are the considerations to help you plan the migration: <br>
1. Accessing the REST producer API: <br>
    The v2 endpoint can be accessed in the same way as the existing URL, that is by obtaining the value of `kafka_http_url` property for the service instance. The path to use is `/v2/topics/<topic_name>/records`.
    
       Example URL: https://service-instance-adsf1234asdf1234asdf1234-0000.us-south.containers.appdomain.cloud/v2/topics/topic_name/records
3. Authentication: <br>
    The supported authentication mechanism is a bearer token. To enhance security, basic auth using API keys is no longer accepted.
    
       Example Header:  –H "Authorization: Bearer $token"
3. Headers: <br>
The Content-Type and the Accept headers must be set to `application/json`.
    
       Example Headers:  –H "Content-Type: application/json" -H "Accept: application/json"
4. Payload: <br>
    The payload for v2 endpoint should be provided in JSON format. The message key, headers, and data can be defined in the payload. The headers can be specified in the form of a list, whose values should be base64 encoded. However, the message key and headers are optional.
    
       Example payload:
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
    One of the following supported data types must be specified for the field type under the key and value object:

    a.  Text: The data provided is validated as plain text format consisting of linear sequence of characters.

    b.  Binary: The data provided is validated as base64 encoded binary format.

    c.  JSON: The data provided is validated as [JSON](https://www.json.org/json-en.html) format.

    d.  Avro: The data is validated as [Apache Avro data format](https://cloud.ibm.com/docs/EventStreams?topic=EventStreams-ES_schema_registry&locale=en#ES_apache_avro_data_format).

5. Error Response: <br>
    The error response contains `trace`,  `error message`, `error code`, `more_info` and, `target` properties.

       Example error response:
       {
        "trace": "a222e93c-e5f9-435d-b275-5d4919ea87ed",
        "error": {
         "code": "invalid_type",
         "message": "'type' field in 'value' object is required ...",
         "more_info": "https://cloud.ibm.com/apidocs/event-streams/restproducer_v2",
         "target": {
          "type": "field",
          "name": "type"
         }
        }
       }


## Limitations

When using the REST producer API, there is a limitation on the maximum size of the message passed as request payload. The maximum size of the payload is limited to 64K.


## API reference
{: #rest_api_reference}
* For full details of the API reference of v2 endpoint, see the 
[{{site.data.keyword.messagehub}} REST Producer v2 API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/apidocs/event-streams/restproducer_v2){: new_window}.


* For full details of the API reference of existing endpoint, see the 
[{{site.data.keyword.messagehub}} REST Producer API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/apidocs/event-streams){: new_window}.
