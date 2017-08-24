---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# How to migrate the Kafka client from 0.9.x to 0.10.x
{: #kafka_migrate}


If you're using the Java clients, you can now use
the publicly available 0.10.x Kafka clients. You are strongly encouraged to move from 0.9.x to the
latest 0.10.x version (currently 0.10.2.1). Complete the following steps:

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


