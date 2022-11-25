---

copyright:
  years: 2015, 2022
lastupdated: "2022-11-22"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: EventStreams

---

{{site.data.keyword.attribute-definition-list}}

# Using ksqlDB with {{site.data.keyword.messagehub}}
{: #ksql_using}

You can use [KSQL](https://github.com/confluentinc/ksql){: external} with {{site.data.keyword.messagehub}} for stream processing. Ensure that you use ksqlDB version 5.5.0.
{: shortdesc}

The quickest and easiest way to run ksqlDB with {{site.data.keyword.messagehub}} is to use a docker container as described in [ksqlDB quickstart](https://ksqldb.io/quickstart.html). 

Because ksqlDB needs to create a topic with an unlimited `retention.ms` setting, you can use only ksqlDB with the Enterprise plan.
{: important}

1. Use the {{site.data.keyword.messagehub}} dashboard in the {{site.data.keyword.Bluemix_notm}} console to create a topic called `_confluent-ksql-default__command_topic` with a single partition and the default retention period.

2. If you want to run ksqlDB in docker container, follow these steps:
   
    a. Create `docker-compose.yml` file with the following contents:
    
    ```text
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
    
    Where BOOTSTRAP_SERVERS and PASSWORD are the values from your {{site.data.keyword.messagehub}} **Service Credentials** tab in {{site.data.keyword.Bluemix_notm}}.

    b. From the directory that you created the file, run the following command to start ksqlDB server.
    
    ```text
    docker-compose up
    ```

    c. Run the following command to connect to the ksqlDB server and start an interactive command-line interface (CLI) session. 
    
    ```text
    docker exec -it ksqldb-cli ksql http://localhost:8088
    ```

3. If you are not running ksqlDB in docker container, then follow these steps:
 
    a. Clone the ksqlDB repository:
    
    ```text
    git clone https://github.com/confluentinc/ksql
    ```

    b. Navigate to the ksqlDB directory and compile the code. 
    
    ```text
    cd ksql
    mvn clean install -Dmaven.test.skip=true
    ```
    
    c. Create an {{site.data.keyword.messagehub}} ksqlDB configuration file.

    For example:
    
    ```text
    bootstrap.servers=BOOTSTRAP_SERVERS
    listeners=http://localhost:8088
    security.protocol=SASL_SSL
    sasl.mechanism=PLAIN
    ssl.protocol=TLSv1.2
    ssl.enabled.protocols=TLSv1.2
    sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="token" password="PASSWORD";
    ksql.sink.replications.default=3
    ```
    
    Where BOOTSTRAP_SERVERS and PASSWORD are the values from your {{site.data.keyword.messagehub}} **Service Credentials** tab in {{site.data.keyword.Bluemix_notm}}.

    d. Start ksqlDB server by using the following command:
    
    ```text
    ./bin/ksql-server-start ./config/ibm-eventstreams.properties
    ```
    
    e. Start ksqlDB CLI by using the following command:
    
    ```text
    ./bin/ksql
    ```

4. You can use `ksql-datagen` command-line tool to generate a test data. Use the {{site.data.keyword.messagehub}} dashboard in the {{site.data.keyword.Bluemix_notm}} console to create two topics with one partition each: `users` and `pageviews`.

    Then, start `DataGen` twice as follows:
    
    a. Run the following command to start creating `users` events.
    
    ```text
    ./bin/ksql-datagen quickstart=users format=json topic=users maxInterval=10000 propertiesFile=./config/ibm-eventstreams.properties
    ```

    b. Run the following command to start creating `pageviews` events.
    
    ```text
    ./bin/ksql-datagen quickstart=pageviews format=delimited topic=pageviews maxInterval=10000 propertiesFile=./config/ibm-eventstreams.properties
    ```
    
	Ensure you insert all the Kafka hosts listed in the **Service Credentials** page as values for `bootstrap-server`. To find this information, go to your {{site.data.keyword.messagehub}} instance in {{site.data.keyword.Bluemix_notm}}, go to the **Service Credentials** tab, and select the **Credentials** that you want to use.

When you completed these steps, you can run all queries that are listed in the [ksqlDB Quick Start Guide](https://github.com/confluentinc/ksql/tree/0.1.x/docs/quickstart#create-a-stream-and-table){: external}.
