---

copyright:
  years: 2015, 2019
lastupdated: "2019-05-09"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Limits and quotas
{: #kafka_quotas }

{{site.data.keyword.messagehub}} uses quotas to control the resources, such as network bandwidth, that a service can consume. The types and levels of quotas depend on the plan being used:

## Standard plan

**Network throughput**

The maximum throughput per service instance equates to 1MB/sec per partition up to a maximum of 20 MB/sec e.g. for a service instance with 10 partitions the maximum throughput will be 10MB/sec and for 30 partitions it will be 20 MB/s.

The throughput is measured separately for producers and consumers. When exceeded, throttling is applied by slightly delaying the responses to requests, effectively applying a gentle brake to producers and consumers until the bandwidth is reduced.

**Partitions** 100 partitions per service instance.

**Retention** A maximum of 1 GB per partition

**Other limits**:
* Maximum message size: 1MB
* Maximum concurrently active Kafka clients: 100
* Maximum request rate [HTTP Produce API]: 100/sec
* Maximum request rate [HTTP Admin API]: 10/sec

## Enterprise plan

**Network throughput** 
A recommended maximum of 40 MB/sec with a peak limit of 90 MB per second. Throughput is expressed as the number of bytes per second that can be both sent and received in a cluster.
The recommended figure is based on a typical workload and takes into account the possible impact of operational actions such as internal updates or failure modes, like the loss of an availability zone. If the average throughput exceeds the recommended figure, a loss in performance might be experienced during these conditions.


**Partitions** 1000 partitions per service instance.

**Retention** Unlimited up to the storage limit of your plan.


Other Limits:
Max message size: 1MB















