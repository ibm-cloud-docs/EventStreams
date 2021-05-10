---

copyright:
  years: 2015, 2021
lastupdated: "2020-01-18"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: EventStreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Limits and quotas
{: #kafka_quotas }

{{site.data.keyword.messagehub}} uses quotas to control the resources, such as network bandwidth, that a service can consume. The types and levels of quotas depend on whether you're using the Lite, Standard, or Enterprise plan.

## Lite plan
{: #limits_lite }

### Network throughput
{: #lite_throughput }

A recommended maximum of 100 KB per second. Throughput is expressed as the number of bytes per second that can be both sent and received in a cluster.

The recommended figure is based on a typical workload and takes into account the possible impact of operational actions such as internal updates or failure modes, like the loss of an availability zone. If the average throughput exceeds the recommended figure, a loss in performance might be experienced during these conditions.


### Partitions
{: #lite_partitions}

1 partition for each service instance.

### Retention
{: #lite_retention}

A maximum of 100 MB for the partition. 


### Consumer groups
{: #lite_consumer_groups}

A maximum of 10 consumer groups. When the limit is exceeded, the `GROUP_MAX_SIZE_REACHED` error is returned to the client.

### Other limits
{: #lite_limits}

* Maximum message size: 1 MB
* Maximum concurrently active Kafka clients: 5
* Maximum request rate [HTTP Produce API]: 5 per second
* Maximum request rate [HTTP Admin API]: 10 per second
* Maximum record key size when using REST Producer API is 4 K 
* Maximum record value size when using REST Producer API is 64 K

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

### Consumer groups
{: #standard_consumer_groups}

A maximum of 1000 consumer groups. When the limit is exceeded, the `GROUP_MAX_SIZE_REACHED` error is returned to the client.

### Other limits
{: #standard_limits}

* Maximum message size: 1 MB
* Maximum concurrently active Kafka clients: 500
* Maximum request rate [HTTP Produce API]: 100 per second
* Maximum request rate [HTTP Admin API]: 10 per second
* Maximum record key size when using REST Producer API is 4 K 
* Maximum record value size when using REST Producer API is 64 K

## Enterprise plan
{: #limits_enterprise }

### Network throughput
{: #enterprise_throughput }

Network throughput capacity is based on the peak maximum.  Each peak maximum has a recommended maximum for typical production workloads.

| Peak Maximum | Recommended maximum | 
|--------------|-----------------------|
|150 MB/s (75 MB/s producing and 75 MB/s consuming)| 100 MB/s (50 MB/s producing and 50 MB/s consuming) |
|300 MB/s (150 MB/s producing and 150 MB/s consuming)|200/s (100 MB/s producing and 100 MB/s consuming) |
|450 MB/s (225 MB/s producing and 225 MB/s consuming)|300 MB/s (150 MB/s producing and 150 MB/s consuming)|

Throughput is expressed as the number of bytes per second that can be both sent and received in a service instance.  The throughput capacity can be selected when the service instance is created, and later scaled as demands increase. 


Throughput capacity cannot be scaled down.  To move to a lower throughput capacity would require creating a new Event Streams service instance at the lower capacity unit.


The recommended maximum figure is based on a typical workload and takes into account the possible impact of operational actions such as internal updates or failure modes, like the loss of an availability zone. If the average throughput exceeds the recommended figure, a loss in performance might be experienced during these conditions.  It is recommended to plan your maximum throughput capacity as two-thirds of the peak maximum.  For example two-thirds of the 150 MB/s peak maximum with one capacity unit is 100 MB/s.

For additional information see [Scaling Event streams](/docs/EventStreams?topic=EventStreams-ES_scaling_capacity).

### Partitions
{: #enterprise_partitions}

The maximum number of partitions increases in line with the number of capacity units, so 3000 for 150MB/s, 6000 for 300MB/s and 9000 for 450MB/s in Enterprise. 

This is a hard limit for the Enterprise plan. If you reach this limit, you can no longer create topics. To increase the number of partitions beyond this, [contact IBM ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/get-support?topic=get-support-getting-customer-support#using-avatar){:new_window}.

### Retention
{: #enterprise_retention}

The storage capacity can be selected when the service instance is created, and later scaled as demands increase.  Storage capacity is dependent upon the configured throughput capacity.  Refer to [Scaling Event streams](/docs/EventStreams?topic=EventStreams-ES_scaling_capacity) for additional information on storage capacity options.


Storage capacity cannot be scaled down.  To move to a lower storage capacity would require creating a new Event Streams service instance at the lower capacity unit


For additional information see [Scaling Event streams](/docs/EventStreams?topic=EventStreams-ES_scaling_capacity).

### Schema Registry
{: #enterprise_schema_registry}

#### Schemas
* Maximum number of schemas that can be stored: 1000
* Maximum number of schema versions for each schema that can be stored: 100
* Maximum schema size 64kB

#### Limits
* Maximum request rate [HTTP Schema Admin] 10 per second
* Maximum request rate [HTTP Serdes] 100 per second

### Other limits
{: #enterprise_limits}

* Maximum message size: 1 MB
* Maximum concurrently active Kafka clients: 10000
* Maximum record key size when using REST Producer API is 4 K 
* Maximum record value size when using REST Producer API is 64 K



















