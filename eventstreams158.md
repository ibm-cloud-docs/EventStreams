---

copyright:
  years: 2015, 2020
lastupdated: "2020-02-03e"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka, Sysdig, metrics, cost

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}
{:deprecated: .deprecated}
{:important: .important}

# Event Streams metrics with IBM Cloud Monitoring with Sysdig
{: #metrics}

{{site.data.keyword.mon_full}} is a third-party cloud-native, and container-intelligence management system that you can include as part of your {{site.data.keyword.cloud_notm}} architecture. Use it to gain operational visibility into the performance and health of your applications, services, and platforms. It offers administrators, DevOps teams, and developers full stack telemetry with advanced features to monitor and troubleshoot, define alerts, and design custom dashboards. {{site.data.keyword.mon_full_notm}} is operated by Sysdig in partnership with {{site.data.keyword.IBM_notm}}.
{:shortdesc}


## Opting in to {{site.data.keyword.messagehub}} metrics
{: #opt_in_metrics}

To opt into using {{site.data.keyword.messagehub}} Sysdig metrics, complete the steps detailed in 
[Getting started tutorial for {{site.data.keyword.mon_full}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/services/Monitoring-with-Sysdig?topic=Sysdig-getting-started#step1){:new_window}.


## {{site.data.keyword.messagehub}} metrics details
{: #metric_details}

The following tables describe the metrics provided by {{site.data.keyword.messagehub}}. 

## Metrics available by Service plan
{: metrics-by-plan}

| Metric Name |Lite|Standard|Enterprise|
|-----------|--------|--------|--------|
| [Authentication failures](#ibm_eventstreams_kafka_authentication_failure_total) |    |   | X |
| [Consume message conversion time](#ibm_eventstreams_instance_consume_conversions_time_quantile) |    |   | X |
| [Estimated connections](#ibm_eventstreams_kafka_connected_clients_estimated) |    |   | X |
| [Inactive consumer groups](#ibm_eventstreams_instance_inactive_consumergroups) |    |   | X |
| [Instance bytes in per second](#ibm_eventstreams_instance_bytes_in_per_second) |  X | X | X |
| [Instance bytes out per second](#ibm_eventstreams_instance_bytes_out_per_second) |  X | X | X |
| [Missing SNI connections](#ibm_eventstreams_kafka_missing_sni_host_total) |    |   | X |
| [Number of partitions](#ibm_eventstreams_instance_partitions) |    |   | X |
| [Number of topics](#ibm_eventstreams_instance_topics) |    |   | X |
| [Produce message conversion time](#ibm_eventstreams_instance_produce_conversions_time_quantile) |    |   | X |
| [Rebalancing consumer groups](#ibm_eventstreams_instance_rebalancing_consumergroups) |    |   | X |
| [Reserved disk space percentage](#ibm_eventstreams_instance_reserved_disk_space_percent) |    |   | X |
| [Stable consumer groups](#ibm_eventstreams_instance_stable_consumergroups) |    |   | X |
| [Topic bytes in per second](#ibm_eventstreams_instance_topic_bytes_in_per_second) |  X | X | X |
| [Topic bytes out per second](#ibm_eventstreams_instance_topic_bytes_out_per_second) |  X | X | X |
| [Utilized disk space percentage](#ibm_eventstreams_instance_utilised_disk_space_percent) |    |   | X |
{: caption="Table 1: Metrics Available by Plan Names" caption-side="top"}

### Authentication failures
{: #ibm_eventstreams_kafka_authentication_failure_total}

Incrementing count of the number of authentication failures

| Metadata | Description |
|----------|-------------|
| Metric Name | ibm_eventstreams_kafka_authentication_failure_total |
| Metric Type | counter |
| Value Type  | none |
| Segment By | Service instance, Event Streams cluster, Service instance name |
{: caption="Table 2: Authentication failures metric metadata" caption-side="top"}

### Consume message conversion time
{: #ibm_eventstreams_instance_consume_conversions_time_quantile}

Indicates the accumulated time spent performing message conversion from clients that are consuming using older protocol versions

| Metadata | Description |
|----------|-------------|
| Metric Name | ibm_eventstreams_instance_consume_conversions_time_quantile |
| Metric Type | gauge |
| Value Type  | second |
| Segment By | Service instance, Quantile, Event Streams cluster, Service instance name |
{: caption="Table 3: Consume message conversion time metric metadata" caption-side="top"}

### Estimated connections
{: #ibm_eventstreams_kafka_connected_clients_estimated}

The estimated number of connections using the Kafka API

| Metadata | Description |
|----------|-------------|
| Metric Name | ibm_eventstreams_kafka_connected_clients_estimated |
| Metric Type | counter |
| Value Type  | none |
| Segment By | Service instance, Event Streams cluster, Service instance name |
{: caption="Table 4: Estimated connections metric metadata" caption-side="top"}

### Inactive consumer groups
{: #ibm_eventstreams_instance_inactive_consumergroups}

The number of inactive consumer groups in an Event Streams instance

| Metadata | Description |
|----------|-------------|
| Metric Name | ibm_eventstreams_instance_inactive_consumergroups |
| Metric Type | gauge |
| Value Type  | none |
| Segment By | Service instance, Event Streams cluster, Service instance name |
{: caption="Table 5: Inactive consumer groups metric metadata" caption-side="top"}

### Instance bytes in per second
{: #ibm_eventstreams_instance_bytes_in_per_second}

The number of bytes produced per second to an Event Streams instance

| Metadata | Description |
|----------|-------------|
| Metric Name | ibm_eventstreams_instance_bytes_in_per_second |
| Metric Type | gauge |
| Value Type  | byte |
| Segment By | Service instance, Event Streams cluster, Service instance name |
{: caption="Table 6: Instance bytes in per second metric metadata" caption-side="top"}

### Instance bytes out per second
{: #ibm_eventstreams_instance_bytes_out_per_second}

The number of bytes consumed per second from an Event Streams instance

| Metadata | Description |
|----------|-------------|
| Metric Name | ibm_eventstreams_instance_bytes_out_per_second |
| Metric Type | gauge |
| Value Type  | byte |
| Segment By | Service instance, Event Streams cluster, Service instance name |
{: caption="Table 7: Instance bytes out per second metric metadata" caption-side="top"}

### Missing SNI connections
{: #ibm_eventstreams_kafka_missing_sni_host_total}

Incrementing count of the number of connections rejected due to not supporting the SNI extension to TLS

| Metadata | Description |
|----------|-------------|
| Metric Name | ibm_eventstreams_kafka_missing_sni_host_total |
| Metric Type | counter |
| Value Type  | none |
| Segment By | Service instance, Event Streams cluster, Service instance name |
{: caption="Table 8: Missing SNI connections metric metadata" caption-side="top"}

### Number of partitions
{: #ibm_eventstreams_instance_partitions}

The number of partitions in an Event Streams instance

| Metadata | Description |
|----------|-------------|
| Metric Name | ibm_eventstreams_instance_partitions |
| Metric Type | gauge |
| Value Type  | none |
| Segment By | Service instance, Event Streams cluster, Service instance name |
{: caption="Table 9: Number of partitions metric metadata" caption-side="top"}

### Number of topics
{: #ibm_eventstreams_instance_topics}

The number of topics in an Event Streams instance

| Metadata | Description |
|----------|-------------|
| Metric Name | ibm_eventstreams_instance_topics |
| Metric Type | gauge |
| Value Type  | none |
| Segment By | Service instance, Event Streams cluster, Service instance name |
{: caption="Table 10: Number of topics metric metadata" caption-side="top"}

### Produce message conversion time
{: #ibm_eventstreams_instance_produce_conversions_time_quantile}

Indicates the accumulated time spent performing message conversion from clients that are producing using older protocol versions

| Metadata | Description |
|----------|-------------|
| Metric Name | ibm_eventstreams_instance_produce_conversions_time_quantile |
| Metric Type | gauge |
| Value Type  | second |
| Segment By | Service instance, Quantile, Event Streams cluster, Service instance name |
{: caption="Table 11: Produce message conversion time metric metadata" caption-side="top"}

### Rebalancing consumer groups
{: #ibm_eventstreams_instance_rebalancing_consumergroups}

The number of rebalancing consumer groups in an Event Streams instance

| Metadata | Description |
|----------|-------------|
| Metric Name | ibm_eventstreams_instance_rebalancing_consumergroups |
| Metric Type | gauge |
| Value Type  | none |
| Segment By | Service instance, Event Streams cluster, Service instance name |
{: caption="Table 12: Rebalancing consumer groups metric metadata" caption-side="top"}

### Reserved disk space percentage
{: #ibm_eventstreams_instance_reserved_disk_space_percent}

The percentage of reserved disk space required for all allocated partitions if fully utilized

| Metadata | Description |
|----------|-------------|
| Metric Name | ibm_eventstreams_instance_reserved_disk_space_percent |
| Metric Type | gauge |
| Value Type  | percent |
| Segment By | Service instance, Event Streams cluster, Service instance name |
{: caption="Table 13: Reserved disk space percentage metric metadata" caption-side="top"}

### Stable consumer groups
{: #ibm_eventstreams_instance_stable_consumergroups}

The number of stable consumer groups in an Event Streams instance

| Metadata | Description |
|----------|-------------|
| Metric Name | ibm_eventstreams_instance_stable_consumergroups |
| Metric Type | gauge |
| Value Type  | none |
| Segment By | Service instance, Event Streams cluster, Service instance name |
{: caption="Table 14: Stable consumer groups metric metadata" caption-side="top"}

### Topic bytes in per second
{: #ibm_eventstreams_instance_topic_bytes_in_per_second}

The number of bytes produced per second to a topic

| Metadata | Description |
|----------|-------------|
| Metric Name | ibm_eventstreams_instance_topic_bytes_in_per_second |
| Metric Type | gauge |
| Value Type  | byte |
| Segment By | Service instance, IBM Event Streams Kafka topic, Event Streams cluster, Service instance name |
{: caption="Table 15: Topic bytes in per second metric metadata" caption-side="top"}

### Topic bytes out per second
{: #ibm_eventstreams_instance_topic_bytes_out_per_second}

The number of bytes consumed per second from a topic

| Metadata | Description |
|----------|-------------|
| Metric Name | ibm_eventstreams_instance_topic_bytes_out_per_second |
| Metric Type | gauge |
| Value Type  | byte |
| Segment By | Service instance, IBM Event Streams Kafka topic, Event Streams cluster, Service instance name |
{: caption="Table 16: Topic bytes out per second metric metadata" caption-side="top"}

### Utilized disk space percentage
{: #ibm_eventstreams_instance_utilised_disk_space_percent}

The percentage of currently utilized disk space

| Metadata | Description |
|----------|-------------|
| Metric Name | ibm_eventstreams_instance_utilised_disk_space_percent |
| Metric Type | gauge |
| Value Type  | percent |
| Segment By | Service instance, Event Streams cluster, Service instance name |
{: caption="Table 17: Utilized disk space percentage metric metadata" caption-side="top"}

## Attributes for Segmentation
{: attributes}

### Global Attributes
{: global-attributes}
The following attributes are available for segmenting all of the metrics listed above

| Attribute | Attribute Name | Attribute Description |
|-----------|----------------|-----------------------|
| Cloud Type | ibm_ctype | The cloud type is a value of public, dedicated or local |
| Location | ibm_location | The location of the monitored resource - this may be a region, data center or global |
| Resource group | ibm_resource_group_name | The resource group where the service instance was created |
| Scope | ibm_scope | The scope is the account, organization or space GUID associated with this metric |
| Service name | ibm_service_name | Name of the service generating this metric |

### Additional Attributes
{: additional-attributes}
The following attributes are available for segmenting one or more attributes as described in the reference above.  Please see the individual metrics for segmentation options.

| Attribute | Attribute Name | Attribute Description |
|-----------|----------------|-----------------------|
| Event Streams cluster | ibm_eventstreams_cluster | The name of an Event Streams cluster |
| IBM Event Streams Kafka topic | ibm_eventstreams_topic | IBM Event Streams Kafka topic |
| Quantile | ibm_quantile | The quantile represented when a metric supports segmenting by quantile |
| Service instance | ibm_service_instance | The service instance segment identifies the instance the metric is associated with |
| Service instance name | ibm_service_instance_name | The service instance name provides the user-provided name of the service instance which isn't necessarily a unique value depending on the name provided by the user. |


[Monitoring Event Streams metrics ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/observability-monitoring?topic=observability-monitoring-monitor-sysdig){:new_window}.


## {{site.data.keyword.messagehub}} metrics cost information
{: #metric_costs}

Before you opt in to using {{site.data.keyword.mon_full}} metrics, be aware of the cost of doing so. The estimated cost depends on the following considerations:

* how often time series is sent for each plan
* the number of topics you use
* the {{site.data.keyword.messagehub}} plan that you use
* whether you are using a customer account or a provider account

| Plans            | Tier         | Data collection  |
|------------------|--------------|------------------|
| `Trial`          |              | Data is collected for a maximum of 20 containers per node or for 200 custom metrics per node for 30 days only. |
| `Graduated tier` | `Basic`      | Data is collected for a maximum of 20 containers per node or for 200 custom metrics per node. |
| `Graduated tier` | `Pro`        | Data is collected for a maximum of 50 containers per node or for 500 custom metrics per node. |
| `Graduated tier` | `Advanced`   | Data is collected for a maximum of 110 containers per node or for 3000 custom metrics per node. |
{: caption="Table 1. List of service plans" caption-side="top"} 




