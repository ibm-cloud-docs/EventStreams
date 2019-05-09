---

copyright:
  years: 2015, 2019
lastupdated: "2019-05-09g"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}

# Using the REST producer API
{: #rest_producer_using}


<br/>
**Rewrite to apply to new REST produce only interface.**
{: note}

{{site.data.keyword.messagehub}}  provides a REST API to help connect your existing systems to your {{site.data.keyword.messagehub}} Kafka cluster. Using the API, you can integrate Event Streams with any system that supports RESTful APIs.

The REST producer API is a scalable REST interface for producing messages to {{site.data.keyword.messagehub}}  over a secure HTTP endpoint. Send event data to {{site.data.keyword.messagehub}} , utilize Kafka technology to handle data feeds, and take advantage of {{site.data.keyword.messagehub}} features to manage your data.

Use the API to connect existing systems to Event Streams. Create produce requests from your systems into {{site.data.keyword.messagehub}} , including specifying the message key, headers, and the topics you want to write messages to.


## Producing messages using REST
{: #rest_produce_messages}

Use the producer API to write messages to topics. To be able to produce to a topic, you must have the following available:

* The URL of the {{site.data.keyword.messagehub}} API endpoint, including the port number.
* The topic you want to produce to.
* The API key that gives permission to connect and produce to the selected topic.
* The {{site.data.keyword.messagehub}} certificate.

To retrieve the full URL for the {{site.data.keyword.messagehub}} API endpoint:

1. Ensure that you have installed the [{{site.data.keyword.messagehub}} CLI](/docs/services/EventStreams?topic=eventstreams-cli).
2. Log in to your cluster as an administrator by using the IBM Cloud Private CLI:

    ```
    cloudctl login -a https://<Cluster Master Host>:<Cluster Master API Port>
    ```
    {: codeblock}

    The master host and port for your cluster are set during the installation of IBM Cloud Private.
3. Run the following command to initialize the {{site.data.keyword.messagehub}} CLI: 
    ```
    cloudctl es init
    ```
    {: codeblock}
    If you have more than one {{site.data.keyword.messagehub}} instance installed, select the one where the topic you want to produce to is.
    Details of your {{site.data.keyword.messagehub}} installation are displayed.
4. Copy the full URL from the {{site.data.keyword.messagehub}} API endpoint field, including the port number.

<br/>
To create a topic and generate an API key with produce permissions, and to download the certificate:

1. If you have not previously created the topic, create it now:

    ```
    cloudctl es topic-create --name <topic_name> --partitions 1 --replication-factor 3
    ```
    {: codeblock}
2. Create a service ID and generate an API key:

    ```
    cloudctl es iam-service-id-create --name <serviceId_name> --role editor --topic <topic_name>
    ```
    {: codeblock}

    For more information about roles, permissions, and service IDs, see [Managing access to your {{site.data.keyword.messagehub}} resources](/docs/services/EventStreams?topic=eventstreams-security).
3. Copy the API key returned by the previous command.
4. Download the certificate for {{site.data.keyword.messagehub}}:

    ```
    cloudctl es certificates --format pem
    ```
    {: codeblock}

<br/>
You have now gathered all the details required to use the producer API. You can use the usual languages for making the API call. For example, to use cURL to produce messages to a topic with the producer API, run the curl command as follows:

```
curl -v -X POST -H "Authorization: Bearer <api_key>" -H "Content-Type: text/plain" -H "Accept: application/json" -d 'test message' --cacert es-cert.pem "<api_endpoint>/topics/<topic_name>/records"
```
{: codeblock}

Where:

* ```<api_key>``` is the API key that you generated earlier.
* ```<api_endpoint>``` is the full URL copied from the Event Streams API endpoint field earlier (format ```https://<host>:<port>```).
* ```<topic_name>``` is the name of the topic you want to produce messages to.

For full details of the Rest Producer API, see the 
[{{site.data.keyword.messagehub}} API reference yaml file ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.ibm.com/mhub/rest-producer/blob/master/openapi.yaml){:new_window}.


OLD
------------------------
## Producing messages using REST
{: #rest_producing_messages}

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
examples detailed in the [Confluent docs ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://docs.confluent.io/2.0.0/){:new_window} by adding the following line to the command line:
<pre class="pre">-H "X-Auth-Token: <var class="keyword varname">APIKEY</var>"</pre>
{: codeblock}

<br/>
## How to connect and authenticate
{: #rest_connect}

<!-- info was in eventstreams066.md -->

To connect to {{site.data.keyword.messagehub}}, the Kafka REST API uses the <code>api_key</code> and <code>kafka_rest_url</code>
credentials from the [VCAP_SERVICES environment variable](/docs/services/EventStreams?topic=eventstreams-connecting#connect_standard_cf).

To authenticate with the {{site.data.keyword.messagehub}} Kafka REST API, you must specify the <code>api_key</code> in the X-Auth-Token header of your requests.


## How to use the API
{: #rest_how}

<!-- info was in eventstreams097.md -->

The {{site.data.keyword.messagehub}} Kafka REST API sample is a Node.js application, which connects to {{site.data.keyword.messagehub}} over the Kafka REST API to produce and consume messages.

The sample code is in the [event-streams-samples GitHub project ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/event-streams-samples/tree/master/kafka-nodejs-console-sample){:new_window}.

Follow the instructions in the [README.md ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/event-streams-samples/tree/master/kafka-nodejs-console-sample){:new_window} file for that project to build and run the sample.

------------






