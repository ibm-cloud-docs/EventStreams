---

copyright:
  years: 2015, 2019
lastupdated: "2019-11-01"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:deprecated: .deprecated}

# Using the Kafka REST API on the Classic plan 
{: #rest_using_classic}

This version of the Kafka REST API is available as part of the Classic plan only. The Classic plan is deprecated. From November 1, 2019, you can no longer provision new instances of the Classic Plan. <br/>However, existing instances will continue to be supported.
From June 30, 2020, the Classic Plan will be retired and no longer supported. Any instance of the Classic Plan still provisioned at this date will be deleted. 
{:deprecated}

The Kafka REST API provides a RESTful interface to a Kafka
cluster. You can produce and consume messages by using the
API. For more information including the API reference documentation, see [Kafka REST Proxy docs ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.confluent.io/2.0.0/kafka-rest/docs/index.html){:new_window}. Only the binary embedded format is supported for requests and responses in {{site.data.keyword.messagehub}}. The Avro and JSON embedded formats are not supported.
{: shortdesc}

If you are using CURL, you can use an example like the following to produce:
<pre class="pre"><code>
curl -X POST -H "X-Auth-Token:<var class="keyword varname">APIKEY</var>" -H "Content-Type: application/vnd.kafka.binary.v1+json" <var class="keyword varname">kafka-rest endpoint</var>/topics/<var class="keyword varname">topic name</var> -d 

'
{
  "records": [
    {
      "value": "<var class="keyword varname">A base 64 encoded value string</var>"
    }
  ]
}
'
</code></pre>
{: codeblock}
<br/>
<br/>
If you are using CURL, you can use an example like the following to consume:
<pre class="pre"><code>
curl -X GET -H "X-Auth-Token:<var class="keyword varname">APIKEY</var>" -H "Accept: application/vnd.kafka.binary.v1+json" <var class="keyword varname">kafka-rest endpoint</var>/topics/<var class="keyword varname">topic name</var>/partitions/<var class="keyword varname">partition ID</var>/messages?offset=<var class="keyword varname">offset to start from</var>
</code></pre>
{: codeblock}

<br/>
<br/>
For CURL, you can also adapt the code
examples detailed in the [Confluent docs ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.confluent.io/2.0.0/){:new_window} by adding the following line to the command line:
<pre class="pre">-H "X-Auth-Token: <var class="keyword varname">APIKEY</var>"</pre> 
{: codeblock}

<br/>
## How to connect and authenticate
{: #rest_connect_classic}

<!-- info was in eventstreams066.md -->

To connect to {{site.data.keyword.messagehub}}, the Kafka REST API uses the <code>api_key</code> and <code>kafka_rest_url</code>
credentials from the [VCAP_SERVICES environment variable](/docs/EventStreams?topic=eventstreams-connecting#connect_classic_cf_plan).

To authenticate with the {{site.data.keyword.messagehub}} Kafka REST API, you must specify the <code>api_key</code> in the X-Auth-Token header of your requests.


## How to use the API
{: #rest_how_classic}

<!-- info was in eventstreams097.md -->

The {{site.data.keyword.messagehub}} Kafka REST API sample is a Node.js application, which connects to {{site.data.keyword.messagehub}} over the Kafka REST API to produce and consume messages.

The sample code is in the [event-streams-samples GitHub project ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/event-streams-samples/tree/master/kafka-nodejs-console-sample){:new_window}.

Follow the instructions in the [README.md ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/event-streams-samples/tree/master/kafka-nodejs-console-sample){:new_window} file for that project to build and run the sample.

	Th following blog provides a good introduction to the strengths and weaknesses of the Kafka REST API. [A Comprehensive, Open Source REST Proxy for Kafka. ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.confluent.io/blog/a-comprehensive-open-source-rest-proxy-for-kafka/){: new_window}.






