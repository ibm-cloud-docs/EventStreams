---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Using the MQ Light API 
{: #mql_using}

** The MQ Light API is available as part of the Standard plan only.**
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
* With the {{site.data.keyword.mql}} API, you can use a much larger number of topics and the topic names are hierarchical (for example: <code>‘/sports/football’</code> and <code>‘/sports/tiddlywinks’</code>). 

The topics in the {{site.data.keyword.mql}} API are not the same
as Kafka topics. Instead, the {{site.data.keyword.mql}} API uses a
single Kafka topic called "MQLight" and all the messages sent and received using the {{site.data.keyword.mql}} API go through that one Kafka topic.

The {{site.data.keyword.mql}} is available in the following
{{site.data.keyword.Bluemix_notm}} regions only: US South (Dallas), UK South (London), and AP South (Sydney). The MQ Light API not available in the EU Central (Frankfurt) region or in
{{site.data.keyword.Bluemix_notm}} Dedicated.

For more information about choosing between the APIs, see [Choosing between the three APIs](/docs/services/EventStreams/eventstreams087.html).


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
<code>password</code>, and <code>mqlight_lookup_url</code> details from the [VCAP_SERVICES environment variable](/docs/services/EventStreams/eventstreams127.html). Use the following guidance for your chosen language:

**For Java**

If you specify ‘null’ as the endpointService parameter of the create() call, this instructs the
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

For more information about the {{site.data.keyword.mql}} APIs,
see: [{{site.data.keyword.mql}} developerWorks&reg; site ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/messaging/mq-light/){:new_window}.


<!-- 14/11/18: info was in eventstreams080.md, moved because of doc app changes -->

## How to connect existing MQ Light applications
{: #mql_exist_apps}


You can connect existing applications that currently run against either {{site.data.keyword.IBM_notm}} MQ or the {{site.data.keyword.mql}}
{{site.data.keyword.Bluemix_notm}} service to the service. The apps continue to work in the same way.
{:shortdesc}

To connect existing apps, complete the following checks:

* Ensure that the app is using the latest available {{site.data.keyword.mql}} API client version for your language.
* Check that the connection details extracted from VCAP_SERVICES reference the <code>messagehub</code> service type and retrieve the connections user name from the <code>credentials.user</code> property rather than the <code>credentials.username</code> property, and retrieve the connection lookup URL from the <code>credentials.mqlight_lookup_url</code> property rather than the <code>credentials.connectionLookupURI</code> property. For more information, see [VCAP_SERVICES environment variable](/docs/services/EventStreams/eventstreams127.html).

	Note that this step is done for you if you use the Java&trade; client and specify 'null' as the endpointService parameter in the create() call, so that the client retrieves the information itself.
	
* Your app must support TLS v1.2 connections. VCAP_SERVICES no longer contains a <code>credentials.nonTLSConnectionLookupURI</code> property for creating a non-TLS connection.

You should also note the following information:

* Message limits are consistent with {{site.data.keyword.messagehub}} but might be different from other servers supporting the {{site.data.keyword.mql}} API. For more information, see [Maximum limits](/docs/services/EventStreams/eventstreams083.html).
* JMS is not supported.
