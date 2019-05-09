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

{{site.data.keyword.messagehub}} uses quotas to control the resources, such as network bandwidth, that a service can consume. The types and levels of quotas depend on whether you're using the Standard or Enterprise plan.

## Standard plan
{: #limits_standard }

### Network throughput
{: #standard_throughput }

The maximum throughput for each service instance equates to 1 MB per second per partition up to a maximum of 20 MB per second. For example, for a service instance with 10 partitions, the maximum throughput is 10 MB per second and for 30 partitions it is 20 MB per second.

The throughput is measured separately for producers and consumers. When exceeded, throttling is applied by slightly delaying the responses to requests, effectively applying a gentle brake to producers and consumers until the bandwidth is reduced.

### Partitions
{: #standard_partitions}

100 partitions for each service instance.

### Retention
{: #standard_retention}

A maximum of 1 GB for each partition.

### Other limits
{: #standard_limits}

* Maximum message size: 1 MB
* Maximum concurrently active Kafka clients: 100
* Maximum request rate [HTTP Produce API]: 100 per second
* Maximum request rate [HTTP Admin API]: 10 per second

## Enterprise plan
{: #limits_enterprise }

### Network throughput
{: #enterprise_throughput }

A recommended maximum of 40 MB per second with a peak limit of 90 MB per second. Throughput is expressed as the number of bytes per second that can be both sent and received in a cluster.

The recommended figure is based on a typical workload and takes into account the possible impact of operational actions such as internal updates or failure modes, like the loss of an availability zone. If the average throughput exceeds the recommended figure, a loss in performance might be experienced during these conditions.


### Partitions
{: #enterprise_partitions}

1000 partitions for each service instance.

### Retention
{: #enterprise_retention}

Unlimited, up to the storage limit of your plan.

### Other limits
{: #enterprise_limits}

Maximum message size: 1 MB















