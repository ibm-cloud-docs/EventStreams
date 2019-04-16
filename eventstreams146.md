---

copyright:
  years: 2015, 2019
lastupdated: "2019-04-15"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Migrating a Kafka Java client on the Classic plan 
{: #kafka_java_migrating_classic}


## Migrating a Kafka Java client from 0.9.X or 0.10.X to later client versions
{: #kafka_migrate}


If you're using the Java clients, you can use
the publicly available Kafka clients at 0.10 or later. 

You are strongly encouraged to move from 0.9.X to the
latest version. You can download a Kafka client from 
[https://kafka.apache.org/downloads ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://kafka.apache.org/downloads){:new_window}.

For information about the implications of using a 0.9.X client, see 
[Backward compatibility](/docs/services/EventStreams?topic=eventstreams-kafka_clients#compatibility).



### Migrating a Kafka Java client to 0.10.2.X or later versions

From 0.10.2, you can configure SASL authentication directly in the client's properties instead of using a JAAS file. This simplification allows you to run multiple clients in the same JVM using different sets of credentials, which is not possible with a JAAS file.

Complete the following steps:

1. Delete the JAAS file. Note that the JVM property java.security.auth.login.config=<PATH TO JAAS> is also no longer required.
2. If you're migrating from 0.9.X, delete the {{site.data.keyword.messagehub}} login jar module.
2. Add the following to the client's properties:
    ```
	sasl.mechanism=PLAIN
    sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="USERNAME" password="PASSWORD";
	```

	where USERNAME and PASSWORD are the values from your {{site.data.keyword.messagehub}} **Service Credentials** tab in {{site.data.keyword.Bluemix_notm}}.
	
	

### Migrating a Kafka client from 0.9.X to 0.10.0.X or 0.10.1.X

Complete the following steps:

1. Delete the {{site.data.keyword.messagehub}} login jar module.
2. Change your <code>jaas.conf</code> file to the following:
    ```
        KafkaClient {
          org.apache.kafka.common.security.plain.PlainLoginModule required
          serviceName="kafka"
            username="USERNAME"
            password="PASSWORD";
        };
    ```
    {: codeblock}

	where USERNAME and PASSWORD are the values from your {{site.data.keyword.messagehub}} **Service Credentials** tab in {{site.data.keyword.Bluemix_notm}}.
	
3. Add this line to your consumer and producer properties: <code>sasl.mechanism=PLAIN</code>
