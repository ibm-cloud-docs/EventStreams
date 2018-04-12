---

copyright:
  years: 2015, 2018
lastupdated: "2017-10-05"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Known restrictions
{: #restrictions}


## Topics and partitions
{: #topics_partitions}

*  Topic names are restricted to a maximum of 100 characters.
*  The default number of partitions for a topic is one.
*  Each {{site.data.keyword.Bluemix_notm}} space has a limit of 100 partitions. To create
   more partitions, you must use a new {{site.data.keyword.Bluemix_notm}} space.

## Message retention
{: #message_retention}

By default, messages are retained in Kafka for up to 24 hours and
each partition is capped at 1 GB. If the 1 GB cap is reached, the
oldest messages are discarded to stay within the limit.

You can change the time limit for message retention when you
create a topic using either the user interface or the
administration API. The time limit is a minimum of an hour and a
maximum of 30 days.

## Creating and deleting topics in Kafka
{: #create_delete}

In Kafka, topic creation and deletion are asynchronous operations
that might take some time to complete. You are recommended to
avoid usage patterns that rely on the rapid creation and deletion
of topics, or on the rapid deletion and re-creation of topics.

## Kafka REST API
{: #trouble_rest}

*  Only the binary embedded format is supported for requests and
   responses. The Avro and JSON embedded formats are not supported.
*  Concurrent requests are not supported for a consumer instance.
   Read, commit, or delete requests corresponding to a consumer
   instance should be sent only after a response is received for
   any outstanding requests of that instance.

## Kafka REST API rate limitation
{: #kafka_rate}

Applications using the Kafka REST API can be subject to rate
limiting for each ApiKey. When this limiting occurs, the API
responds with the following HTTP error:

<code>429 Too Many Requests</code>
{:screen}

If you see this error, wait and submit the request again.

<!--12/04/18 - Karen: same info duplicated at messagehub108 -->
## Kafka REST API daily restart
{: #rest_restart}

The Kafka REST API restarts once a day for a short period of
time. During this period, the Kafka REST API might become
unavailable. If this happens, you are recommended to retry your
request. After the REST API has restarted, you will have to
recreate your Kafka consumer instances. If this is the case, the
REST API returns the following JSON:

```'{"error_code":40403,"message":"Consumer instance not found."}'
```
{:screen}

## Kafka high-level consumer API
{: #kafka_consumer}

You cannot use the Apache Kafka 0.8.2 simple or high-level
consumer API with {{site.data.keyword.messagehub}}. Instead, you can use the earliest supported Kafka consumer API, which is 0.9.
