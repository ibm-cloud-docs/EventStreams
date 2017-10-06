---

copyright:
  years: 2015, 2017
lastupdated: "2017-09-26"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Using KSQL with Message Hub
{: #ksql_using}

You can use [KSQL ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/confluentinc/ksql){:new_window} with {{site.data.keyword.messagehub}} for stream processing. Complete the following steps:

<ol>
<li>Create a {{site.data.keyword.messagehub}} KSQL configuration file. For example:

<pre>
<code>
    bootstrap.servers=
    kafka01-prod01.messagehub.services.us-south.bluemix.net:9093
    application.id=ksql_server_quickstart
    ksql.command.topic.suffix=commands
    listeners=http://localhost:8080
    security.protocol=SASL_SSL
    sasl.mechanism=PLAIN
    ssl.protocol=TLSv1.2
    ssl.enabled.protocols=TLSv1.2
    sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="USERNAME" password="PASSWORD";
    ksql.sink.replications.default=3
</code>
</pre>
{:codeblock}

</li>

<li>Use the {{site.data.keyword.messagehub}} dashboard in the {{site.data.keyword.Bluemix_notm}} console to create a topic called ```ksql__commands``` with a single partition and the default retention period.
</li>

<li>From a Docker terminal, start KSQL using the following command:
<pre>
<code>
    /bin/ksql-cli local --<var class="keyword varname">messagehub-ksql-properties-file</var> ./config/ksqlserver.properties
</code>
</pre>
{:codeblock}

</li>

<li>To populate data, edit the ```DataGen``` class in ```io.confluent.ksql.datagen;``` in the ksql-examples project. For example:

<pre>
<code>
    Properties props = new Properties();
       props.put("bootstrap.servers", arguments.bootstrapServer);
       props.put("client.id", "KSQLDataGenProducer");
       props.put("security.protocol", "SASL_SSL");
       props.put("sasl.mechanism", "PLAIN");
       props.put("ssl.protocol", "TLSv1.2");
       props.put("ssl.enabled.protocols", "TLSv1.2");
       props.put("sasl.jaas.config", "org.apache.kafka.common.security.plain.PlainLoginModule required username=\"USERNAME\" password=\"PASSWORD\";");
</code>
</pre>
{:codeblock}

</li>

<li>Use the {{site.data.keyword.messagehub}} dashboard in the {{site.data.keyword.Bluemix_notm}} console to create two topics with one partition each: ```users``` and ```pageviews```. 

    Then start <code>DataGen</code> twice as follows:

    a. With <code>bootstrap-server=kafka01-prod01.messagehub.services.us-south.bluemix.net:9093 quickstart=users format=json topic=users maxInterval=10000</code> to start creating <code>users</code> events.

    b. With <code>bootstrap-server=kafka01-prod01.messagehub.services.us-south.bluemix.net:9093 quickstart=pageviews format=delimited topic=pageviews maxInterval=10000</code> to start creating <code>pageviews</code> events.

</li>
</ol>

When you have completed these steps, you can run all queries listed in the [Quick Start guide ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/confluentinc/ksql/tree/0.1.x/docs/quickstart#create-a-stream-and-table){:new_window}







