---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Differences between Message Hub in {{site.data.keyword.Bluemix_notm}} Public and Dedicated environments
{: #public_dedicated}

{{site.data.keyword.Bluemix}} is an open-standards,
cloud-based platform for building, running, and managing applications. {{site.data.keyword.Bluemix_notm}} provides public and dedicated deployment
models. {{site.data.keyword.messagehub}} is available in both
environments.

## {{site.data.keyword.Bluemix_notm}} Public environment
{: notoc}

{{site.data.keyword.Bluemix_notm}} Public provides an
economical public cloud service where you pay for what you use and share infrastructure with
others.

In {{site.data.keyword.Bluemix_notm}} Public, the cost of
{{site.data.keyword.messagehub}} is determined by two factors: the
number of partitions that you use and the number of messages that you send and receive. There is no
charge for message data while it is retained on the topics, but the data that each partition retains
is capped at 1 GB.

For more information, see [{{site.data.keyword.Bluemix_notm}} Public ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud-computing/bluemix/public){:new_window}.


## {{site.data.keyword.Bluemix_notm}} Dedicated environment
{: notoc}

{{site.data.keyword.Bluemix_notm}} Dedicated provides a more
isolated environment where your infrastructure is not shared and is hosted in a separate SoftLayer
account managed by {{site.data.keyword.IBM_notm}}. This environment is securely connected to {{site.data.keyword.Bluemix_notm}} Public and your own network.

In a dedicated instance of {{site.data.keyword.messagehub}}, you
pay for the service rather than how much you use it. You can have up to 75 partitions across the
whole environment including all organizations and spaces. Each partition is capped at 10 GB to
ensure the cluster doesn't run out of space.

{{site.data.keyword.messagehub}} in Dedicated can only be deployed with {{site.data.keyword.Bluemix_notm}} Dedicated, but a syndicated version of our public service can be made available if you're using other dedicated environments.

The Kibana and Grafana dashboards for monitoring the service are not supported in {{site.data.keyword.Bluemix_notm}} Dedicated.

For more information, see [{{site.data.keyword.Bluemix_notm}} Dedicated ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/cloud-computing/bluemix/dedicated/){:new_window}.


### Kafka quotas in {{site.data.keyword.messagehub}} Dedicated
{: notoc}

{{site.data.keyword.messagehub}} now implements Kafka quotas, that is throttling for producers and consumers.

Kafka brokers can keep track of throughput values, in bytes per second for producers and consumers, measured over a window of about 30 seconds.

If the value is found to exceed a configured threshold, Kafka brokers introduce a delay before sending responses to clients, so that the resulting throughput is lowered to stay within the set quota.

{{site.data.keyword.messagehub}} implements this check by assigning a throughput quota, separate for producers and consumers, to each {{site.data.keyword.messagehub}} instance, proportional to the number of partitions, spread approximately evenly across the brokers.

A base quota for each partition is set administratively by {{site.data.keyword.IBM}} and can be set to be arbitrarily high, turning off the quota mechanism completely.

The throughput is _not_ measured for each partition, that is, it can be used all on one partition if the other ones are idle.

Example:
If a dedicated {{site.data.keyword.messagehub}} has:
* 4 brokers
* overall limit of 1000 partitions
* base value for producers set to 5MB/s

Then for a {{site.data.keyword.messagehub}} instance with a total of 500 partitions, all the producers connecting to that instance must share a throughput of

5MB/s x 500 = 2.5 GB/s across 4 brokers

That is, approximately 625 MB/s for each broker.

### Checking for throttling in client applications

Kafka brokers send the throttling information to clients, as part of produce and fetch responses, so clients can know whether they have been throttled.

In the Java client, the following per-broker metrics are available:

* produce-throttle-time-max
* produce-throttle-time-avg
* fetch-throttle-time-avg
* fetch-throttle-time-max


For more information, see [producer monitoring ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://kafka.apache.org/documentation/#producer_monitoring){:new_window} and 
[new consumer monitoring ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://kafka.apache.org/documentation/#new_consumer_monitoring){:new_window}


In the Node.js client node-rkafka, based on the C librdkafka library, client statisitcs are emitted as a big JSON string, see [statistics ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/edenhill/librdkafka/wiki/Statistics){:new_window}

In a node-rdkafka application, you can access these metrics with code like the following:

```
var producer = new Kafka.Producer({
  'metadata.broker.list': ''kafka01-prod01.messagehub.services.us-south.bluemix.net:9093,kafka02-prod01...',
   ...,
  'statistics.interval.ms' : 1000
});
...
producer.on('event.stats', function(arg) {
  var jmsg = JSON.parse(arg.message);
  if (jmsg.brokers) {
    console.log(jmsg.brokers['sasl_ssl://kafka01-prod01.messagehub.services.us-south.bluemix.net:9093/0'].throttle, ...)
  }  
});
```

If the throttle values are not zero, the client has been throttled by the broker.
