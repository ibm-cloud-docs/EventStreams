---

copyright:
  years: 2015, 2019
lastupdated: "2019-07-08"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka, migration, REST API

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Migrating the REST APIs {{site.data.keyword.messagehub}} from the Classic plan
{: #migrate_rest_apis}

The new Standard plan introduces changes in the REST APIs for users coming from the Classic plan. The following information summarizes what these changes are and the recommended actions, if any, to move from the Classic to Standard or Enterprise plans:

<dl>
<dt>Admin API</dt>
<dd>The API and functionality remains the same, but small changes might be required to the processing of error responses.
</dd>
<dt>Produce API</dt>
<dd>The core functionality remains the same, but small changes in properties and formats may be required.
</dd>
<dt>Consume API</dt>
<dd>No longer supported
</dd>
</dl>

The following sections provide details of the changes:

## Admin
{: #migrate_admin_api}

The API and functionality remains the same, but small changes might be required to the processing of error responses:

On the Classic plan:

```
{
  "errorCode": 403,
  "errorMessage": "Unauthorized"
}
```

On the Standard plan:

{
    "error_code": 40403,
    "message": "topic 'ffff' does not exist",
    "incident_id": "a34b19b3-b55d-4937-bef2-0c9fa9390fcb"
}

Also note, additional methods are available for clients to authenticate. You can now use Basic Auth or a bearer token in addition to the previously supported method of placing an API key in the X-Auth-Token header.

For further information and examples, see 
[Using the Administration REST API](//docs/services/EventStreams?topic=eventstreams-admin_api)

## Produce
{: #migrate_produce_api}

The core functionality of the produce API remains the same, but small changes in properties and formats are required. In particular, consider the following:

* Endpoint URL - The URL of the API is unique to each service instance and must be retrieved from the 'kafka_http_url' property of a service credentials object or service key. Previously this would have been retrieved from the 'kafka_rest_url' property of the applications VCAP_SERVICES.

* Authentication - In addition to the previously supported method of placing an API key in the X-Auth-Token header, clients can now also authenticate using either basic auth or a bearer token 

* Methods - Messages are sent by POSTing a request to a single method with the path '/topics/<topic_name>/records'. This replaces the previous path 'topics/<topic_name>'

* Body - Two new content types 'text/plain' and 'application/json' are supported which allow the message payload to be set directly in the body of the HTTP request. This replaces the previous 'application/vnd.kafka.binary.v1+json' binary embedded format. Each message must be sent in its own HTTP request. If a message key is required, this can now be set as either a text or binary value in the 'key/keyType' HTTP request query parameters.

* Headers - Message properties can now be set by formatting as a key:value comma separated list in a 'headers' query parameter in the HTTP request

* Errors - The formatting of the body returned in error responses has changed, updates may be required if these are processed by an application

Previously, from the Classic plan:

{
	"error_code":415,
	"message":"HTTP 415 Unsupported Media Type"
}

Now, for the Standard plan:

{
	"error":{
		"message":"Unsupported content type",
		"error_code":415
	}
}


The following gives an example of a full request, and how this has changed between the plans:

Previously, using the Classic plan to send the message 'Hello world'

POST <kafka_rest_url>/topics/<topic>
X-Auth-Token: <YourAPIKey>
Content-Type: application/vnd.kafka.binary.v1+json
Accept: application/vnd.kafka.v1+json, application/vnd.kafka+json, application/json

{
  "records": [
    {
      "key": "myKey",
      "value": "SGVsbG8gV29ybGQK"
    }
  ]
}

Now, on the Standard plan the equivalent would be:

POST <kafka_http_url>/topics/<topic>/records?key=mykey
X-Auth-Token: <YourAPIKey>
Content-Type: text/plain
Accept: application/json

Hello World


Further information is available here: <link to REST Produce docs>


## Consume
{: #migrate_consume_api}

Consuming messages via HTTP is no longer supported, this means the following API calls are no longer available:

GET /topics/(string: topic_name)/partitions/(int: partition_id)/messages?offset=(int)[&count=(int)]
Consume messages from one partition of the topic.

POST /consumers/(string: group_name)
Create a new consumer instance in the consumer group.

POST /consumers/(string: group_name)/instances/(string: instance)/offsets
Commit offsets for the consumer. 

DELETE /consumers/(string: group_name)/instances/(string: instance)
Destroy the consumer instance.

GET /consumers/(string: group_name)/instances/(string: instance)/topics/(string: topic_name)
Consume messages from a topic.


To replace this functionality, a number of different approaches can be taken. 

Kafka Client - The core Kafka API is supported on a an ever growing number of platforms and languages https://cwiki.apache.org/confluence/display/KAFKA/Clients we also recommend a number which are specifically tested https://cloud.ibm.com/docs/services/EventStreams?topic=eventstreams-kafka_clients#kafka_clients. If switching is an option, this is recommended as a longer term more scalable, performant approach. Note, the Kafka API is a lower level API then HTTP, and so will expose some additional complexity, however a large number of samples and resources are available to help produce a solution, including our own samples <link to docs>

If switching to the Kafka Client is not an option then other methods for integrating with {{site.data.keyword.messagehub}} to consider include. 

IBM Cloud Functions Service - Serverless actions can be defined, triggered from messages consumed from Kafka https://cloud.ibm.com/docs/openwhisk?topic=cloud-functions-pkg_event_streams#eventstreams_events or define web actions triggered from a REST API https://cloud.ibm.com/docs/openwhisk?topic=cloud-functions-apigateway

IBM App Connect Enterprise - Integration flows can be defined to consume messages from Kafka https://www.ibm.com/support/knowledgecenter/en/SSTTDS_11.0.0/com.ibm.etools.mft.doc/bz91055_.htm   https://www.ibm.com/support/knowledgecenter/en/SSTTDS_11.0.0/com.ibm.etools.mft.doc/bz91030_.htm

Open Source - A number of Open Source REST APIs are available and may provide a suitable alternative





