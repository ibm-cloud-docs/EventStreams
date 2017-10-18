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

1. Create a {{site.data.keyword.messagehub}} KSQL configuration file.

    For example:
    ```
    bootstrap.servers=HOSTNAME:PORTNUMBER
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
    Ensure that you edit the following lines to insert your own data:
	- ```bootstrap.servers``` - insert all the Kafka hosts listed in the **Service Credentials** page.  To find this information, go to your
	{{site.data.keyword.messagehub}} instance in {{site.data.keyword.Bluemix_notm}}, go to the **Service Credentials** tab, and select the
	**Credentials** that you want to use.
	- ```sasl.jaas.config``` - insert your own username and password pair
	
2. Use the {{site.data.keyword.messagehub}} dashboard in the {{site.data.keyword.Bluemix_notm}} console to create a topic called ```ksql__commands``` with a single partition and the default retention period.
3. From a Docker terminal, start KSQL using the following command:
<pre class="pre">/bin/ksql-cli local 
--<var class="keyword varname">properties-file</var> ./config/ksqlserver.properties
</pre>
4. To populate data, edit the ```DataGen``` class in ```io.confluent.ksql.datagen;``` in the ```ksql-examples``` project. For example:
```
     Properties props = new Properties();
        props.put("bootstrap.servers", arguments.bootstrapServer);
        props.put("client.id", "KSQLDataGenProducer");
        props.put("security.protocol", "SASL_SSL");
        props.put("sasl.mechanism", "PLAIN");
        props.put("ssl.protocol", "TLSv1.2");
        props.put("ssl.enabled.protocols", "TLSv1.2");
        props.put("sasl.jaas.config", "org.apache.kafka.common.security.plain.PlainLoginModule required username=\"USERNAME\" password=\"PASSWORD\";"); 
```
    {: codeblock}
5. Use the {{site.data.keyword.messagehub}} dashboard in the {{site.data.keyword.Bluemix_notm}} console to create two topics with one partition each: ```users``` and ```pageviews```.

    Then start ```DataGen``` twice as follows:
	
    i. With ```bootstrap-server=HOSTNAME:PORTNUMBER quickstart=users format=json topic=users maxInterval=10000``` to start creating ```users``` events.
	
    ii. With ```bootstrap-server=HOSTNAME:PORTNUMBER quickstart=pageviews format=delimited topic=pageviews maxInterval=10000``` to start creating ```pageviews``` events.
	
	Ensure you insert all the Kafka hosts listed in the **Service Credentials** page as values for ```bootstrap-server```. To find this information, go to your {{site.data.keyword.messagehub}} instance in {{site.data.keyword.Bluemix_notm}}, go to the **Service Credentials** tab, and select the **Credentials** that you want to use.

When you have completed these steps, you can run all queries listed in the [KSQL Quick Start Guide ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/confluentinc/ksql/tree/0.1.x/docs/quickstart#create-a-stream-and-table){:new_window}

