---

copyright:
  years: 2015, 2019
lastupdated: "2018-02-06"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Using KSQL with {{site.data.keyword.messagehub}}
{: #ksql_using}

You can use [KSQL ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/confluentinc/ksql){:new_window} with {{site.data.keyword.messagehub}} for stream processing. Ensure that you use KSQL 0.4, or later. 
{: shortdesc}

Complete the following steps:

1. Create an {{site.data.keyword.messagehub}} KSQL configuration file.

    For example:
    ```
    bootstrap.servers=BOOTSTRAP_SERVERS
    application.id=ksql_server_quickstart
    ksql.command.topic.suffix=commands
    listeners=http://localhost:8080
    security.protocol=SASL_SSL
    sasl.mechanism=PLAIN
    ssl.protocol=TLSv1.2
    ssl.enabled.protocols=TLSv1.2
    sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="USERNAME" password="PASSWORD";
    ksql.sink.replications.default=3
    ```
    where BOOTSTRAP_SERVERS, USERNAME, and PASSWORD are the values from your {{site.data.keyword.messagehub}} **Service Credentials** tab in {{site.data.keyword.Bluemix_notm}}.

2. Use the {{site.data.keyword.messagehub}} dashboard in the {{site.data.keyword.Bluemix_notm}} console to create a topic called <code>ksql__commands</code> with a single partition and the default retention period.
3. From a Docker terminal, start KSQL using the following command:
<pre class="pre">/bin/ksql-cli local 
--<var class="keyword varname">properties-file</var> ./config/ksqlserver.properties
</pre>
4. Use the {{site.data.keyword.messagehub}} dashboard in the {{site.data.keyword.Bluemix_notm}} console to create two topics with one partition each: <code>users</code> and <code>pageviews</code>.

    Then start <code>DataGen</code> twice as follows:
	
    i. With <code>bootstrap-server=HOSTNAME:PORTNUMBER quickstart=users format=json topic=users maxInterval=10000</code> to start creating <code>users</code> events.
	
    ii. With <code>bootstrap-server=HOSTNAME:PORTNUMBER quickstart=pageviews format=delimited topic=pageviews maxInterval=10000</code> to start creating <code>pageviews</code> events.
	
	Ensure you insert all the Kafka hosts listed in the **Service Credentials** page as values for <code>bootstrap-server</code>. To find this information, go to your {{site.data.keyword.messagehub}} instance in {{site.data.keyword.Bluemix_notm}}, go to the **Service Credentials** tab, and select the **Credentials** that you want to use.

When you have completed these steps, you can run all queries listed in the [KSQL Quick Start Guide ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/confluentinc/ksql/tree/0.1.x/docs/quickstart#create-a-stream-and-table){:new_window}

