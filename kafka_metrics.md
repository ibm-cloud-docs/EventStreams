---

copyright:
  years: 2024
lastupdated: "2024-02-21"

keywords: monitoring, metrics

subcollection: EventStreams

---

{{site.data.keyword.attribute-definition-list}}

# Getting started with Kafka metrics
{: #getting-started-metrics}

Apache Kafka is a widely recognized open-source event store and stream processing platform and is the de facto standard for data streaming and is used by over 70% of Fortune 500 companies. All major Cloud providers offer managed data streaming services to meet this growing demand. One key advantage of opting for managed Kafka services is the delegation of responsibility for broker and operational metrics, allowing you to focus solely on metrics specific to your producers, consumers, and clients. Following is a guidance on a set of metrics for you to monitor for optimal performance.

When it comes to Kafka, monitoring typically involves various metrics related to topics, partitions, brokers, and consumer groups. Standard Kafka metrics include information on throughput, latency, replication, and disk usage. Refer to the [Kafka documentation](https://kafka.apache.org/documentation/) and relevant monitoring tools to understand the specific metrics available for your version of Kafka and how to interpret them effectively.

## Why is it important to monitor Kafka?
{: #why-monitor}

Monitoring your {{site.data.keyword.messagehub_full}} instance is crucial to ensure optimal functionality and overall health of your data pipeline. Kafka is a powerful distributed streaming platform, consisting of servers and clients that communicate over a high-performance protocol and often plays a central role in a variety of data architectures. Monitoring your Kafka clients helps to identify early signs of application failure, such as high resource usage and lagging consumers and bottlenecks. Identifying these warning signs early enables proactive response to potential issues that minimize downtime and prevent any disruption to business operations. Monitoring your Kafka instance also allows you to optimize costs by effectively utilizing your resources and the limits of your plan, which helps you to avoid potential service disruptions due to resource exhaustion and aids effective capacity planning as you scale. 

Kafka clients (producers and consumers) have their own set of metrics to monitor their performance and health. {{site.data.keyword.messagehub}} supports a rich set of metrics for both clients and is exposed in the official Java client. For more information, see [Monitoring Event Streams metrics by using IBM Cloud Monitoring](/docs/EventStreams?topic=EventStreams-metrics).

## Which metrics to monitor
{: #what-monitor}

### Producer metrics
{: #producer-metrics}

| Metric | Why monitor |
| --- | --- |
| record-error-rate | This metric measures the average per-second number of records sent that resulted in errors. A high (or an increase in) record-error-rate might indicate a loss in data or data not being ingested as expected. All these effects could compromize the integrity of the data you are processing and storing in Kafka. Monitoring this metric helps to ensure that data being sent by producers is accurately and reliably recorded in your Kafka topics.  |
| request-latency-avg | This is the average latency for each produce request in ms. An increase in latency impacts performance and might signal an issue. Measuring the request-latency-avg metric can help to identify bottlenecks within your instance. For many applications, low latency is crucial to ensure a high-quality end user experience and a spike in request-latency-avg could be a signal that you are hitting the limits of your provisioned instance. This issue can be fixed by changing your producer settings, for example, by batching or scaling your plan to optimize performance.  |
| byte-rate  | The average number of bytes sent per second for a topic is a measure of your throughput. If you stream data on a regular basis, a drop in throughput may indicate an anomaly in your Kafka instance. The {{site.data.keyword.messagehub}} Enterprise plan starts from 150MB/s split one-to-one between ingress and egress and it is important to know how much of that you are consuming for effective capacity planning. Do not go above two-thirds of the maximum throughput, in order to account for the possible impact of operational actions, such as internal updates or failure modes (for example, the loss of an availability zone).  |
{: caption="Table 2. Producer metrics" caption-side="bottom"}

### Consumer metrics
{: #consumer-metrics}

| Metric | Why monitor |
| --- | --- |
| fetch-rate <br>fetch-size-avg| The number of fetch requests per second (fetch-rate) and the average number of bytes fetched per request (fetch-size-avg) are key indicators for how well your Kafka consumers are performing. A high fetch-rate could signal inefficiency especially over a small number of messages, as it means insufficient (possibly no) data is being received each time. The fetch-rate and fetch-size-avg is affected by three settings: fetch.min.bytes, fetch.max.bytes, and fetch.max.wait.ms. Tune these settings to achieve the desired overall latency, whilst minimizing the number of fetch requests and potentially the load on the broker CPU. Monitoring and optimizing both of these metrics ensures that you are processing data efficiently for current and future workloads. |
| commit-latency-avg | This metric measures the average time between a committed record being sent and the commit response being received. Similar to the request-latency-avg as a producer metric, a stable commit-latency-avg means that your offset commits happen in a timely manner. A high commit latency could indicate problems within the consumer that prevent it from committing offsets quickly, which directly impacts the reliability of data processing, as it could lead to duplicate processing of messages if a consumer has to restart and reprocess messages from a previously uncommitted offset. A high commit latency also means that more time is spent in administrative operations rather than actual message processing. This issue could lead to backlogs of messages waiting to be processed, especially in high-volume environments.   |
| bytes-consumed-rate | This is a consumer fetch metric that measures the average number of bytes consumed per second. Similar to the byte-rate as a producer metric, this should be a stable and expected metric. A sudden change in the expected trend of the bytes-consumed-rate could represent an issue with your applications. A low rate could be a signal of efficiency in data fetches or over-provisioned resources. A higher rate could overwhelm the consumers' processing capability and thus require scaling, creating more consumers to balance out the load or changing consumer configurations, such as fetch sizes. |
| rebalance-rate-per-hour | The number of group rebalance participated per hour. Rebalancing occurs every time there is a new consumer or a consumer leaves the group and causes a delay in processing as partitions are re-assigned making Kafka consumers less efficient, if there are a lot of rebalances per hour. A higher rebalance rate per hour could be caused by misconfigurations leading to unstable consumer behavior. This rebalancing act could cause an increase in latency and could result in applications crashing. Ensure that your consumer groups are stable by tracking a low and stable rebalance-rate-per-hour.  |
{: caption="Table 3. Consumer metrics" caption-side="bottom"}
