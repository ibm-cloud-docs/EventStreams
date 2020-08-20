---

copyright:
  years: 2015, 2020
lastupdated: "2020-01-15"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: EventStreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}

# Using ksqlDB with {{site.data.keyword.messagehub}}
{: #ksql_using}

You can use [KSQL ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/confluentinc/ksql){:new_window} with {{site.data.keyword.messagehub}} for stream processing. Ensure that you use ksqlDB V5.5.0.
{: shortdesc}

The quickest and easiest way to run ksqlDB with {{site.data.keyword.messagehub}} is to use a docker container as described in [ksqlDB quickstart](https://ksqldb.io/quickstart.html). 

Because ksqlDB needs to create a topic with an unlimited `retention.ms` setting, you can only use ksqlDB with the Enterprise plan.
{:important}

1. Use the {{site.data.keyword.messagehub}} dashboard in the {{site.data.keyword.Bluemix_notm}} console to create a topic called <code>_confluent-ksql-default__command_topic</code> with a single partition and the default retention period.

2. If you want to run ksqlDB in docker container, follow these steps:
   
    a. Create <code>docker-compose.yml</code> file with the following contents:
    ```
    ---
    version: '2'
    services:
      ksqldb-server:
        image: confluentinc/cp-ksqldb-server:5.5.0
        hostname: ksqldb-server
        container_name: ksqldb-server
        ports:
          - "8088:8088"
        environment:
          KSQL_LISTENERS: http://0.0.0.0:8088
          KSQL_BOOTSTRAP_SERVERS: <BOOTSTRAP_SERVERS>
          KSQL_KSQL_SERVICE_ID: default_
          KSQL_KSQL_SINK_REPLICAS: 3
          KSQL_KSQL_STREAMS_REPLICATION_FACTOR: 3
          KSQL_SECURITY_PROTOCOL: SASL_SSL
          KSQL_KSQL_INTERNAL_TOPIC_REPLICAS: 3
          KSQL_SASL_JAAS_CONFIG: org.apache.kafka.common.security.plain.PlainLoginModule required username=\"token\" password=\"<PASSWORD>\";
          KSQL_SASL_MECHANISM: PLAIN

      ksqldb-cli:
        image: confluentinc/cp-ksqldb-cli:5.5.0
        container_name: ksqldb-cli
        depends_on:
          - ksqldb-server
        entrypoint: /bin/sh
        tty: true
    ```
    where BOOTSTRAP_SERVERS and PASSWORD are the values from your {{site.data.keyword.messagehub}} **Service Credentials** tab in {{site.data.keyword.Bluemix_notm}}.

    b. From the directory you created the file, run the following command to start ksqlDB server.
    ```
    docker-compose up
    ```

    c. Run the following command to connect to the ksqlDB server and start an interactive command-line interface (CLI) session. 
    ```
    docker exec -it ksqldb-cli ksql http://localhost:8088
    ```

3. If you are not running ksqlDB in docker container, then follow these steps:
 
    a. Clone the ksqlDB repository:
    ```
    git clone https://github.com/confluentinc/ksql
    ```

    b. Navigate to the ksqlDB directory and compile the code. 
    ```
    cd ksql
    mvn clean install -Dmaven.test.skip=true
    ```
    
    c. Create an {{site.data.keyword.messagehub}} ksqlDB configuration file.

    For example:
    ```
    bootstrap.servers=BOOTSTRAP_SERVERS
    listeners=http://localhost:8088
    security.protocol=SASL_SSL
    sasl.mechanism=PLAIN
    ssl.protocol=TLSv1.2
    ssl.enabled.protocols=TLSv1.2
    sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="token" password="PASSWORD";
    ksql.sink.replications.default=3
    ```
    where BOOTSTRAP_SERVERS and PASSWORD are the values from your {{site.data.keyword.messagehub}} **Service Credentials** tab in {{site.data.keyword.Bluemix_notm}}.

    b. Start ksqlDB server using the following command:
    ```
    ./bin/ksql-server-start ./config/ibm-eventstreams.properties
    ```
    
    c. Start ksqlDB CLI using the following command:
    ```
    ./bin/ksql
    ```

4. You can use <code>ksql-datagen</code> command line tool to generate a test data. Use the {{site.data.keyword.messagehub}} dashboard in the {{site.data.keyword.Bluemix_notm}} console to create two topics with one partition each: <code>users</code> and <code>pageviews</code>.

    Then start <code>DataGen</code> twice as follows:
    
    i. Run the following command to start creating <code>users</code> events.
    ```
    ./bin/ksql-datagen quickstart=users format=json topic=users maxInterval=10000 propertiesFile=./config/ibm-eventstreams.properties
    ```

    ii. Run the following command to start creating <code>pageviews</code> events.
    ```
    ./bin/ksql-datagen quickstart=pageviews format=delimited topic=pageviews maxInterval=10000 propertiesFile=./config/ibm-eventstreams.properties
    ```
	Ensure you insert all the Kafka hosts listed in the **Service Credentials** page as values for <code>bootstrap-server</code>. To find this information, go to your {{site.data.keyword.messagehub}} instance in {{site.data.keyword.Bluemix_notm}}, go to the **Service Credentials** tab, and select the **Credentials** that you want to use.

When you have completed these steps, you can run all queries listed in the [ksqlDB Quick Start Guide ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/confluentinc/ksql/tree/0.1.x/docs/quickstart#create-a-stream-and-table){:new_window}