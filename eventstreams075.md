---

copyright:
  years: 2015, 2019
lastupdated: "2019-04-04"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}

# Using the MQ Light API on the Classic plan
{: #mql_using}

** The MQ Light API is available as part of the Classic plan only.**
<br/>

The {{site.data.keyword.mql}} API is provided for backward compatibility with the earlier {{site.data.keyword.mql}} service. The API provides an AMQP-based messaging interface for Java&trade;, Node.js, Python, and Ruby. 
{:shortdesc}


## What is the MQ Light API and how is it different?
{: #mqlight}

<!-- 30/10/18: info was in eventstreams106.md, moved because of doc app changes -->

The {{site.data.keyword.mql}} API provides a higher level of abstraction for messaging compared to Kafka.

The choice between using a Kafka client or the {{site.data.keyword.mql}} API depends on the messaging topology that you
want to build:

* With Kafka, you use a small number of topics and can have multiple partitions for each topic for additional scalability. You can share messages among consumers by using consumer groups, but each consumer must be able to keep up with the rate of messages for the partitions assigned to it.
* With the {{site.data.keyword.mql}} API, you can use a much larger number of topics and the topic names are hierarchical (for example: <code>&lsquo;/sports/football&rsquo;</code> and <code>&lsquo;/sports/tiddlywinks&rsquo;</code>). 

The topics in the {{site.data.keyword.mql}} API are not the same
as Kafka topics. Instead, the {{site.data.keyword.mql}} API uses a
single Kafka topic called "MQLight" and all the messages sent and received using the {{site.data.keyword.mql}} API go through that one Kafka topic.

The {{site.data.keyword.mql}} is available in the following
{{site.data.keyword.Bluemix_notm}} locations (regions) only: Dallas (us-south), London (eu-gb), and Sydney (au-syd). The MQ Light API not available in the Frankfurt (eu-de) location or in
{{site.data.keyword.Bluemix_notm}} Dedicated.

For more information about choosing between the APIs, see [Choosing between the three APIs](/docs/services/EventStreams?topic=eventstreams-choose_api_classic).


## What's required to use the MQ Light API with {{site.data.keyword.messagehub}}?
{: #mql_reqs}

<!-- 30/10/18: info was in eventstreams098.md, moved because of doc app changes -->

The following requirements are needed to use the {{site.data.keyword.mql}} API with {{site.data.keyword.messagehub}}: 

**You must explicitly create a Kafka topic named "MQLight" before you can use the API because all messages go through the "MQLight" topic. This topic must have a single partition. Creating this topic enables the MQ Light API for your service instance. The topics used in the MQ Light API are automatically created as you use them, but all of the messages are actually on the single "MQLight" Kafka topic.** 

The "MQLight" topic is used by the MQ Light API to store its message data and interact with other Kafka clients. Be aware that when this topic is
created, it incurs charges at the standard rate outlined in the services payment plan.

To disable the MQ Light API, delete the "MQLight" topic. Note that all data is destroyed when the topic is deleted.

<!-- 12/11/18: following info was in eventstreams079.md, moved because of doc app changes -->

## How to connect and authenticate
{: #mql_connect}

To connect an app to the service, the app must use the <code>user</code>,
<code>password</code>, and <code>mqlight_lookup_url</code> details from the [VCAP_SERVICES environment variable](/docs/services/EventStreams?topic=eventstreams-connecting#connect_classic_cf). Use the following guidance for your chosen language:

**For Java**

If you specify <code>null</code> as the endpointService parameter of the create() call, this instructs the
client to read the <code>user</code>, <code>password</code> and,
<code>mqlight_lookup_url</code> details from VCAP_SERVICES:

<pre>
<code>NonBlockingClient.create(null, new NonBlockingClientAdapter<Void>() {
    public void onStarted(NonBlockingClient client, Void context) {
        client.send("my/topic", "Hello World!", null);
    }
}, null);</code>
</pre>
{:codeblock}

<br>

**For Node.js**

Retrieve the <code>user</code>, <code>password</code>, and
<code>mqlight_lookup_url</code> details from VCAP_SERVICES and use them to create the client as
follows:

<pre>
<code>var services = JSON.parse(process.env.VCAP_SERVICES);
mqlightService = services['messagehub'][0];
opts.service = mqlightService.credentials.mqlight_lookup_url;
opts.user = mqlightService.credentials.user;
opts.password = mqlightService.credentials.password;
var mqlightClient = mqlight.createClient(opts, function(err) {
...</code>
</pre>
{:codeblock}

<br>

**For Ruby**

Retrieve the <code>user</code>, <code>password</code>, and
<code>mqlight_lookup_url</code> details from VCAP_SERVICES and use them to create the client as
follows:
<pre>
<code>vcap_services = JSON.parse(ENV['VCAP_SERVICES'])
conn_details = vcap_services['messagehub']
credentials = conn_details.first['credentials']
service = credentials['mqlight_lookup_url']
opts[:user] = credentials['user']
opts[:password] = credentials['password']
set :client, Mqlight::BlockingClient.new(service, opts)
...</code>
</pre>
{:codeblock}

<br>

**For Python**

Retrieve the <code>user</code>, <code>password</code>, and
<code>mqlight_lookup_url</code> details from VCAP_SERVICES and use them to create the client as
follows:
<pre>
<code>vcap_services = json.loads(os.environ.get('VCAP_SERVICES'))
conn_details = vcap_services['messagehub'][0]
service = str(conn_details['credentials']['mqlight_lookup_url'])
security_options = {
      'user': str(conn_details['credentials']['user']),
      'password': str(conn_details['credentials']['password'])
}
client = mqlight.Client(service=service, 
                        security_options=security_options,
                        on_started=on_started)</code>
</pre>
{:codeblock}

<br>

For more information about the APIs,
see: [{{site.data.keyword.mql}} APIs on GitHub ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/mqlight){:new_window}.


<!-- 14/11/18: info was in eventstreams080.md, moved because of doc app changes -->

## How to connect existing MQ Light applications
{: #mql_exist_apps}


You can connect existing applications that currently run against either {{site.data.keyword.IBM_notm}} MQ or the {{site.data.keyword.mql}}
{{site.data.keyword.Bluemix_notm}} service to the service. The apps continue to work in the same way.

To connect existing apps, complete the following checks:

* Ensure that the app is using the latest available {{site.data.keyword.mql}} API client version for your language.
* Check that the connection details extracted from VCAP_SERVICES reference the <code>messagehub</code> service type and retrieve the connections user name from the <code>credentials.user</code> property rather than the <code>credentials.username</code> property, and retrieve the connection lookup URL from the <code>credentials.mqlight_lookup_url</code> property rather than the <code>credentials.connectionLookupURI</code> property. For more information, see [VCAP_SERVICES environment variable](/docs/services/EventStreams?topic=eventstreams-connecting).

	Note that this step is done for you if you use the Java&trade; client and specify 'null' as the endpointService parameter in the create() call, so that the client retrieves the information itself.
	
* Your app must support TLS v1.2 connections. VCAP_SERVICES no longer contains a <code>credentials.nonTLSConnectionLookupURI</code> property for creating a non-TLS connection.

You should also note the following information:

* Message limits are consistent with {{site.data.keyword.messagehub}} but might be different from other servers supporting the {{site.data.keyword.mql}} API. For more information, see [Maximum limits](/docs/services/EventStreams?topic=eventstreams-mql_using#max_limits).
* JMS is not supported.

<!-- 15/11/18: info was in eventstreams081.md, moved because of doc app changes -->

## Exchanging messages between the MQ Light API and the Kafka or Kafka REST APIs
{: #mql_exchange}

{{site.data.keyword.mql}} messages are stored in a single underlying Kafka topic named "MQLight" and are encoded as detailed in the following table. This encoding can also be used by other API types, such as Kafka or Kafka REST, to exchange messages with applications using the
{{site.data.keyword.mql}} API.

### Kafka message format
{: #kafka_format notoc}

<table border='1'>
<caption>Table 1. Kafka message format</caption>
  <tr>
    <th> Key </th>
    <th> Value </th>
  </tr>
  <tr>
    <td> Optional (not used by the API)
	<p></p>
	</td>
    <td>**1 byte**
	<p>		     MQ Light API eye catcher, which is always 0xFA.</p>
    <p><var class="keyword varname">**n**</var> **bytes**</p>
    <p>		    AMQP encoded message (formatted based on the AMQP wire format). </p></td>
  </tr>
</table>


<!-- 15/11/18: info was in eventstreams082.md, moved because of doc app changes -->

## MQ Light API samples
{: #mql_samples}

If you don't already have an app, try the {{site.data.keyword.mql}} API out with one of the samples.

The sample app actually consists of two simple apps: a web front end that sends messages to a
back end and a back end that processes the messages, capitalizes the words, and then returns the
messages to the front end. This sample shows how you can get apps talking to each other using
the {{site.data.keyword.mql}} API. You can also use the {{site.data.keyword.mql}} API to perform worker offload; a key capability
required for building scalable, loosely coupled, and distributed apps.

You can find the sample code in the [event-streams-samples GitHub project ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/event-streams-samples/tree/master/mqlight){:new_window}.


<!-- 15/11/18: info was in eventstreams083.md, moved because of doc app changes -->

## Maximum limits
{: #max_limits}

The following limits are enforced for the {{site.data.keyword.mql}} API:

* The maximum amount of data that can be stored is consistent with a single Kafka partition for your payment plan (typically 1 GB). If this data limit is exceeded, the oldest messages in the partition are removed as new messages are sent.
* The maximum time a message is stored is consistent with a single Kafka partition for your payment plan (typically 24 hours). You cannot retrieve messages that are older than this time period.
* The maximum size of a message (excluding headers) is 1 MB.
* The maximum number of clients that can be connected at a single time is 25.
* The maximum number of destinations that can be active at a single time is 25. An active destination is defined as follows:
  - A destination with a TimeToLive > 0 both with or without a client currently connected.
  - A destination with a TimeToLive = 0 (the default) where a client is connected. 
  <p>A destination that is shared between clients counts as a single destination.</p>