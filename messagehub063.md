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

# How to connect and authenticate
{: #kafka_connect}


To connect to {{site.data.keyword.messagehub}}, the
Kafka API uses the <code>kafka_brokers_sasl</code> credentials, and the <code>user</code> and <code>password</code> from
the [VCAP_SERVICES environment variable](/docs/services/MessageHub/messagehub071.html).

## Connecting and authenticating in an application other than Java
{: #kafka_notjava notoc}

The {{site.data.keyword.messagehub}} service currently
authenticates clients by using SASL PLAIN. Credentials are carried over an encrypted connection.
This is a new feature added in Kafka 0.10.0.X. Any client that supports Kafka 0.10 with SASL PLAIN
should work with {{site.data.keyword.messagehub}}. Example clients are as follows:

* [librdkafka ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/edenhill/librdkafka/){:new_window} 
* [confluent-kafka-python ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/confluentinc/confluent-kafka-python){:new_window} 

If you are using the earlier Kafka 0.9.0.0 client, you need to use a custom login module, which you
can download from [{{site.data.keyword.messagehub}} login module ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/message-hub-samples/blob/master/kafka-0.9/message-hub-login-library/messagehub.login-1.0.0.jar){:new_window}. 

