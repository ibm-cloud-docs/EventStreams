---

copyright:
  years: 2024
lastupdated: "2024-01-22"

keywords: monitoring, metrics

subcollection: EventStreams

---

{{site.data.keyword.attribute-definition-list}}

# Getting started with Kafka metrics
{: #getting-started-metrics}

Apache Kafka is a widely recognized open-source event store and stream processing platform, having evolved into the de facto standard for data streaming and used by over 70% of Fortune 500 companies. Major cloud service providers such as AWS, Azure, and Confluent provide managed data streaming services to meet this growing demand. One key advantage of opting for managed Kafka services is the delegation of responsibility for broker and operational metrics, allowing users to focus solely on metrics specific to their producers, consumers, and clients. Following is a guidance on a set of metrics for you to monitor for optimal performance.

When it comes to Kafka, monitoring typically involves various metrics related to topics, partitions, brokers, and consumer groups. Standard Kafka metrics include information on throughput, latency, replication, disk usage, and so on. Refer to the [Kafka documentation](https://kafka.apache.org/documentation/) and relevant monitoring tools to understand the specific metrics available for your version of Kafka and how to interpret them effectively.

## Why is it important to monitor Kafka?
{: #why-monitor}

Monitoring your {{site.data.keyword.messagehub_full}} instance is crucial to ensure optimal functionality and overall health of your data pipeline. Kafka is a powerful distributed streaming platform and often plays a central role in a variety of data architectures. Monitoring your Kafka instance helps identify early signs of application failure, such as high resource usage and lagging consumers and bottlenecks. Identifying warning signs early enables proactive response to potential issues that minimize downtime and prevent any disruption to business operations. Monitoring your Kafka instance also allows you to optimize costs by effectively utilising your resources and the limits of your plan. That helps you to avoid potential service disruptions due to resource exhaustion and to plan your capacity effectively as you scale.

## Which metrics to monitor
{: #what-monitor}

### General metrics
{: #general-metrics}

| Metric | Use case |
| --- | --- |
| throughput | If you stream data on a regular basis, a drop in throughput might indicate an anomaly. |
{: caption="Table 1. General metrics" caption-side="bottom"}

### Producer metrics
{: #producer-metrics}

| Metric | Use case |
| --- | --- |
| reccord-error-rate | The total number of record sends that resulted in errors. |
| request-latency-avg and request-size-avg |  |
| error-rate |  |
| throughput |  |
| compression |  |
{: caption="Table 2. Producer metrics" caption-side="bottom"}

### Consumer metrics
{: #consumer-metrics}

| Metric | Use case |
| --- | --- |
| fetch-rate |  |
| commit-latency-avg |  |
| error-rate |  |
{: caption="Table 3. Consumer metrics" caption-side="bottom"}

These selected metrics cover a wide variety of applications and use cases, however {{site.data.keyword.messagehub}} provides a [rich set of metrics](/docs/EventStreams?topic=EventStreams-metrics) that provide further useful insights depending on the domain of your application. For more information, see [Event Streams for IBM Cloud](/docs/EventStreams?topic=EventStreams-about).

### Next steps
{: #whats-next}

You’re now an expert in scaling Kafka applications. You’re invited to put these points into practise and try out the fully managed Kafka offering on {{site.data.keyword.cloud}}.

- Learn more about [Kafka and its use cases](/docs/EventStreams?topic=EventStreams-use_cases).
- Provision an instance of [{{site.data.keyword.messagehub}}](https://www.ibm.com/products/event-streams).
- Learn how to [get started](/docs/EventStreams?topic=EventStreams-getting-started) and see the [FAQs](/docs/EventStreams?topic=EventStreams-faqs) for any challenges or questions in setting up {{site.data.keyword.messagehub}}.
