---

copyright:
  years: 2015, 2017
lastupdated: "2017-11-28"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Kafka quotas
{: #kafka_quotas }

{{site.data.keyword.messagehub}} uses throughput quotas to control the network bandwidth that is used by clients. The quotas are in place to minimize the impact of clients on each other. {{site.data.keyword.messagehub}} now implements Kafka quotas, that is throttling for producers and consumers.

Quotas work by measuring the throughput of producers and consumers, and then throttling those that exceed the quotas by slightly delaying the responses to their requests. The effect is to apply a gentle brake to producers and consumers that attempt to consume a lot of bandwidth.

{{site.data.keyword.messagehub}} assigns a throughput quota to each {{site.data.keyword.messagehub}} service instance. A separate quota is used for producers and consumers. The quota is proportional to the number of partitions created for that service instance, although the quota is not applied to each partition.

For example, consider a service instance with 10 topics, each with 1 partition. The throughput quota for producers is as follows:

```
10 x 5 MB/s = 50 MB/s
```

The quota is applied across the nodes of the Kafka cluster. The precise value applied at a point in time depends on the current distribution of partition leaders on the nodes of the cluster.

Kafka brokers can monitor throughput values, in bytes per second, for producers and consumers. These values are measured over a window of about 30 seconds. If the value exceeds a configured threshold, Kafka brokers introduce a delay before sending responses to clients, so that the resulting throughput is lowered to stay within the set quota.

{{site.data.keyword.messagehub}} implements this check by assigning a throughput quota to each {{site.data.keyword.messagehub}} instance, separately for producers and consumers. This quota is proportional to the number of partitions and is spread approximately evenly across the brokers. A base quota for each partition is set administratively by {{site.data.keyword.IBM}} and can be set arbitrarily high to effectively turn off the quota mechanism completely.

The throughput is _not_ measured for each partition, that is, it can be used all on one partition if the other partitions are idle.

For example, if a dedicated {{site.data.keyword.messagehub}} has the following setup:
* 4 brokers
* an overall limit of 1000 partitions
* a base value for producers set to 5 MB/s

then a {{site.data.keyword.messagehub}} instance with a total of 500 partitions with all the producers connecting to that instance must share a throughput of the following:

```
5 MB/s x 500 = 2.5 GB/s across 4 brokers
```

That is, approximately 625 MB/s for each broker.

### Checking for throttling in client applications
{: throttling_apps notoc}

Kafka brokers send the throttling information to clients as part of produce and fetch responses, so clients are aware whether they have been throttled.

In the Java client, the following per-broker metrics are available:

* ```produce-throttle-time-max```
* ```produce-throttle-time-avg```
* ```fetch-throttle-time-avg```
* ```fetch-throttle-time-max```


For more information, see [producer monitoring ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://kafka.apache.org/documentation/#producer_monitoring){:new_window} and 
[new consumer monitoring ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://kafka.apache.org/documentation/#new_consumer_monitoring){:new_window}.


In the Node.js client, node-rkafka client statisitcs are emitted as a big JSON string. node-rkafka is based on the C librdkafka library. For more information, see [statistics ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/edenhill/librdkafka/wiki/Statistics){:new_window}.

In a node-rdkafka application, you can access these metrics with code like the following:

<pre class="pre"><code>
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
</code></pre>
{:codeblock}

If the throttle values are not zero, the client has been throttled by the broker.


