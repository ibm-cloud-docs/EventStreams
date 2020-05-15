---

copyright:
  years: 2015, 2019
lastupdated: "2019-11-01"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka, migration, REST API

subcollection: EventStreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:deprecated: .deprecated}

# Migrating the REST APIs from the Classic plan
{: #migrate_rest_apis}

The Classic plan is deprecated. From November 1, 2019, you can no longer provision new instances of the Classic Plan. <br/>However, existing instances will continue to be supported.
From June 30, 2020, the Classic Plan will be retired and no longer supported. Any instance of the Classic Plan still provisioned at this date will be deleted. 
{:deprecated}

If you're using the Classic plan, be aware that the new Standard plan introduces changes to the REST APIs. The following information summarizes what these changes are and the recommended actions that you might need to take, if any, to move from the Classic to the Standard or Enterprise plans.

<dl>
<dt>Administration API</dt>
<dd>The API and functionality remains the same, but small changes might be required to the processing of error responses. For details, see [Changes to the Administration API](#migrate_admin_api).
</dd>
<dt>Produce API</dt>
<dd>The core functionality remains the same, but small changes in properties and formats might be required. For details, see [Changes to the Produce API](#migrate_produce_api).
</dd>
<dt>Consume API</dt>
<dd>This API is no longer supported. For alternatives, see [Consume API](#migrate_consume_api).
</dd>
</dl>

## Changes to the Administration API
{: #migrate_admin_api}

The API and functionality are the same, but small changes might be required to the processing of error responses:

For example, an error response on the Classic plan:

```
{
  "errorCode": 403,
  "errorMessage": "Unauthorized"
}
```
{: codeblock}

And an error response on the Standard plan:

```
{
    "error_code": 40403,
    "message": "topic 'ffff' does not exist",
    "incident_id": "a34b19b3-b55d-4937-bef2-0c9fa9390fcb"
}
```
{: codeblock}
<br/>
Additional methods are also available for clients to authenticate. You can now use Basic Auth or a bearer token, in addition to the previously supported method of placing an API key in the X-Auth-Token header.

For further information and examples, see 
[Using the Administration REST API](/docs/EventStreams?topic=EventStreams-admin_api).

## Changes to the Produce API
{: #migrate_produce_api}

The core functionality of the produce API remains the same, but small changes in properties and formats are required. In particular, consider the following:

* **Endpoint URL**<br/>
    The URL of the API is unique to each service instance and must be retrieved from the <code>kafka_http_url</code> property of a service credentials object or service key. Previously this URL was retrieved from the <code>kafka_rest_url</code> property of the application's VCAP_SERVICES.

* **Authentication**<br/>
    In addition to the previously supported method of placing an API key in the X-Auth-Token header, clients can now also authenticate using either Basic Auth or a bearer token. 

* **Methods**<br/>
    Messages are sent by POSTing a request to a single method with the path <code>/topics/&lt;topic_name&gt;/records</code>. This replaces the previous path <code>topics/&lt;topic_name&gt;</code>.

* **Body**<br/>
    Two new content types <code>text/plain</code> and <code>application/json</code> are supported, which allow the message payload to be set directly in the body of the HTTP request. These replace the previous <code>application/vnd.kafka.binary.v1+json</code> binary embedded format. Each message must be sent in its own HTTP request. If a message key is required, this can now be set as either a text or binary value in the <code>key/keyType</code> HTTP request query parameters.

* **Headers**<br/>
    Message properties can be set by formatting as a key-value comma separated list in a <code>headers</code> query parameter in the HTTP request.

* **Errors**<br/>
    The formatting of the body that's returned in error responses has changed; updates might be required if these are processed by an application.

    For example, previously on the Classic plan:

    ```
    {
	    "error_code":415,
	    "message":"HTTP 415 Unsupported Media Type"
    }
    ```
    {: codeblock}

    For example, now on the Standard plan:

    ```
    {
	    "error":{
		    "message":"Unsupported content type",
		    "error_code":415
	    }
    }
    ```
    {: codeblock}

### Full request example

The following example shows a full request and how this has changed between the plans.

Using the Classic plan to send the message 'Hello World':

```
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
```
{: codeblock}

<br/>
The equivalent on the Standard plan is as follows:

```
POST <kafka_http_url>/topics/<topic>/records?key=mykey 
X-Auth-Token: <YourAPIKey> 
Content-Type: text/plain
Accept: application/json

Hello World
```
{: codeblock}

For more information, see [{{site.data.keyword.messagehub}} admin-rest api ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/event-streams-docs/tree/master/admin-rest-api){:new_window}.


## Consume API
{: #migrate_consume_api}

Consuming messages via HTTP is no longer supported. Consequently, the following API calls are no longer available:

<dl>
<dt>GET /topics/(<em>string: topic_name</em>)/partitions/(<em>int: partition_id</em>)/messages?offset=(<em>int</em>)[&count=(<em>int</em>)]</dt>
<dd>Consume messages from one partition of the topic.
</dd>
<dt>POST /consumers/(<em>string: group_name</em>)</dt>
<dd>Create a new consumer instance in the consumer group.
</dd>
<dt>POST /consumers/(<em>string: group_name</em>)/instances/(<em>string: instance</em>)/offsets</dt>
<dd>Commit offsets for the consumer. 
</dd>
<dt>DELETE /consumers/(<em>string: group_name</em>)/instances/(<em>string: instance</em>)</dt>
<dd>Destroy the consumer instance.
</dd>
<dt>GET /consumers/(<em>string: group_name</em>)/instances/(<em>string: instance</em>)/topics/(<em>string: topic_name</em>)</dt>
<dd>Consume messages from a topic.
</dd>
</dl>

To replace this functionality, you can take a number of different approaches. 

* **Kafka client**<br/>
    The core Kafka API is supported on an ever-growing number of [platforms and languages ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cwiki.apache.org/confluence/display/KAFKA/Clients){:new_window}. We also recommend a number of specifically tested clients: [recommended clients](/docs/EventStreams?topic=EventStreams-kafka_clients#kafka_clients). 
    
    If switching is an option, you are recommended to do so as a longer term more scalable, performant approach. Note, the Kafka API is a lower-level API than HTTP, and so exposes some additional complexity. However, a large number of samples and resources are available to help produce a solution, including our own 
[samples ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/event-streams-samples){:new_window}.

If switching to the Kafka Client is not an option, other methods for integrating with {{site.data.keyword.messagehub}} that you could consider include the following:

* **{{site.data.keyword.openwhisk}} Service**<br/>
    You can define serverless actions triggered from messages consumed from Kafka: [{{site.data.keyword.messagehub}} events](/docs/openwhisk?topic=cloud-functions-pkg_event_streams#eventstreams_events) or define web actions triggered from a REST API by [creating serverless REST APIs](/docs/openwhisk?topic=cloud-functions-apigateway).

* ** {{site.data.keyword.appconserviceshort}} Enterprise **<br/>
    You can define integration flows to consume messages from Kafka. For more information, see [Using Kafka nodes with {{site.data.keyword.messagehub}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/en/SSTTDS_11.0.0/com.ibm.etools.mft.doc/bz91055_.htm){:new_window} and [Processing Kafka messages ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/en/SSTTDS_11.0.0/com.ibm.etools.mft.doc/bz91030_.htm){:new_window}.







