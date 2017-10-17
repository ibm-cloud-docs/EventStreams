---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# How to migrate the Kafka client from 0.9.X to 0.10.X or 0.11.X
{: #kafka_migrate}


If you're using the Java clients, you can use
the publicly available 0.10.X or 0.11.X Kafka clients. You are strongly encouraged to move from 0.9.X to the
latest 0.10.X or 0.11.X version (we support all newer versions). Complete the following steps:

1. Delete the {{site.data.keyword.messagehub}} login jar module.
2. Change your <code>jaas.conf</code> file to the following:
    ```
        KafkaClient {
          org.apache.kafka.common.security.plain.PlainLoginModule required
          serviceName="kafka"
            username="<your username>"
            password="<your password>";
        };
    ```
    {: codeblock}

3. Add this line to your consumer and producer properties: <code>sasl.mechanism=PLAIN</code>


