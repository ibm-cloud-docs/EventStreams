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

To use KSQL with {{site.data.keyword.messagehub}}, complete the following steps:

1. Create a configuration file. For example:
```
    bootstrap.servers=kafka01-prod01.messagehub.services.us-south.bluemix.net:9093
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
2. Using the {{site.data.keyword.messagehub}} UI, create a topic called ```ksql__commands``` with a single partition.

3. Start KSQL using the following command:
```
/bin/ksql-cli local --properties-file ./config/ksqlserver.properties
```

4. To populate data, edit the ```DataGen``` ```class in io.confluent.ksql.datagen;``` in the ksql-examples project:

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
5. Using the {{site.data.keyword.messagehub}} UI, create 2 topics with 1 partition each: ```users``` and ```pageviews```. Then start DataGen twice as follows:

    1. With ```bootstrap-server=kafka01-prod01.messagehub.services.us-south.bluemix.net:9093 quickstart=users format=json topic=users maxInterval=10000``` to start creating users events
    2. With ```bootstrap-server=kafka01-prod01.messagehub.services.us-south.bluemix.net:9093 quickstart=pageviews format=delimited topic=pageviews maxInterval=10000``` to start creating pageviews events

When you have completed these steps, you can run all queries listed in the [Quick Start guide ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/confluentinc/ksql/tree/0.1.x/docs/quickstart#create-a-stream-and-table){:new_window}







