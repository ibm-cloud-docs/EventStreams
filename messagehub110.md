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
<li>item 2 item 2</li>
<li>item 3 item 3
<ol>
<li>item 3a item 3a</li>
<li>item 3b item 3b</li>
<li>item 3c item 3c</li>
</ol>
</li>
</ol>





When you have completed these steps, you can run all queries listed in the [Quick Start guide ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/confluentinc/ksql/tree/0.1.x/docs/quickstart#create-a-stream-and-table){:new_window}








