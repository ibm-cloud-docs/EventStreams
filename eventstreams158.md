---

copyright:
  years: 2015, 2021
lastupdated: "2021-04-30"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka, IBM Cloud Monitoring, metrics, cost, billing, opting in

subcollection: EventStreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}
{:deprecated: .deprecated}
{:important: .important}

# Monitoring {{site.data.keyword.messagehub}} metrics using {{site.data.keyword.mon_full_notm}}
{: #metrics}

[{{site.data.keyword.mon_full}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/monitoring?topic=monitoring-getting-started)
 is a third-party cloud-native, and container-intelligence management system that you can include as part of your {{site.data.keyword.cloud_notm}} architecture. Use it to gain operational visibility into the performance and health of your applications, services, and platforms. It offers administrators, DevOps teams, and developers full stack telemetry with advanced features to monitor and troubleshoot, define alerts, and design custom dashboards.
{:shortdesc}


## Opting in to and enabling {{site.data.keyword.messagehub}} metrics
{: #opt_in_metrics}

Before you can start using {{site.data.keyword.messagehub}} {{site.data.keyword.mon_full_notm}} metrics, you must first opt in and then enable platform metrics by completing the following steps: 

1. Enable platform metrics for {{site.data.keyword.messagehub}}. For more information, see [Enabling platform metrics ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/monitoring?topic=monitoring-platform_metrics_enabling){:new_window}. The owner of the account has full access to the this metrics data. For more information about managing access for other users see [Getting started tutorial for {{site.data.keyword.mon_full}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/monitoring?topic=monitoring-getting-started-monitor#getting-started-monitor_prereqs){:new_window}.

2. To navigate from the {{site.data.keyword.messagehub}} instance page to the {{site.data.keyword.mon_full_notm}} dashboard, click the 3 vertical dots in the upper right corner of the instance page (**Service instance options**) and select **Monitoring**. 

   On your first usage, you might see a welcome wizard. To advance to the dashboard selection menu, select **Next** and then **Skip** at the bottom of the **Choosing an installation method** page.  Accept the prompts that follow. You can then select the **IBM Event Streams** or **IBM Event Streams (Enterprise)** dashboard, depending on the plan you're using. 
   
   Dashboards are available only after metrics have started to be recorded; this might take a few minutes to initialize.
   {:note} 


## {{site.data.keyword.messagehub}} metrics cost information 
{: #metric_costs}

Before you opt in to using {{site.data.keyword.mon_full}} metrics, be aware of the cost of doing so. The estimated cost depends on the following considerations:

* the {{site.data.keyword.messagehub}} plan that you use
* how many unique time series are sent for each plan
* the number of topics that you have created


<br/>

| Plan            | Topics         | Number of time series  | Monthly cost |
|------------------|--------------|------------------|
| `Lite`          | 1        |1 x 2 + 5 = 7 | $0.08 x 7 = $0.56       |
| `Standard` | 1      | 1 x 2 + 5 = 7 | $0.08 x 7 = $0.56   |
| | 10      | 10 x 2 + 5 = 25 | $0.08 x 25 = $2   |
|  | 100      | 100 x 2 + 5 = 205 | $0.08 x 205 = $16.40   |
| `Enterprise` | 1        | 1 x 2 + 16 = 18 | $0.08 x 18 = $1.44  |
|           | 10        | 10 x 2 + 16 = 36 | $0.08 x 36 = $2.88  |
|         | 100        |  100 x 2 + 16 = 216   | $0.08 x 216 = $17.28  |
|        | 1000        |  1000 x 2 + 16 = 2016  | $0.08 x 2016 = $161.28   |
|      | 3000        |   3000 x 2 + 16 = 6016    | $0.08 x 6016 = $481.28  |

{: caption="Table 1. Cost for each plan" caption-side="top"} 

Enabling Mirroring for Enterprise clusters introduces one additional global gauge and an additional gauge per topic in the target cluster (with the target cluster already emitting metrics in accordance with the above table), therefore increasing the costs accordingly.

For more information, see [{{site.data.keyword.mon_full_notm}} pricing ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/monitoring?topic=monitoring-pricing_plans). 


## {{site.data.keyword.messagehub}} metrics details
{: #metric_details}

The following tables describe the specific metrics provided by {{site.data.keyword.messagehub}} for each plan. 




## Metrics available by service plan
{: metrics-by-plan}

| Metric Name |Enterprise|Lite|Standard|
|-----------|--------|--------|--------|
| [Authentication failures](#ibm_eventstreams_kafka_authentication_failure_total) |  ![Checkmark icon](../../icons/checkmark-icon.svg)  |   |  |
| [Consume message conversion time](#ibm_eventstreams_instance_consume_conversions_time_quantile) |  ![Checkmark icon](../../icons/checkmark-icon.svg)  |   |  |
| [Estimated connected clients percentage](#ibm_eventstreams_kafka_recommended_max_connected_clients_percent) |  ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| [Inactive consumer groups](#ibm_eventstreams_instance_inactive_consumergroups) |  ![Checkmark icon](../../icons/checkmark-icon.svg)  |   |  |
| [Instance bytes in per second](#ibm_eventstreams_instance_bytes_in_per_second) |  ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| [Instance bytes out per second](#ibm_eventstreams_instance_bytes_out_per_second) |  ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| [Missing SNI connections](#ibm_eventstreams_kafka_missing_sni_host_total) |  ![Checkmark icon](../../icons/checkmark-icon.svg)  |   |  |
| [Number of partitions](#ibm_eventstreams_instance_partitions) |  ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| [Number of topics](#ibm_eventstreams_instance_topics) |  ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| [Produce message conversion time](#ibm_eventstreams_instance_produce_conversions_time_quantile) |  ![Checkmark icon](../../icons/checkmark-icon.svg)  |   |  |
| [Rebalancing consumer groups](#ibm_eventstreams_instance_rebalancing_consumergroups) |  ![Checkmark icon](../../icons/checkmark-icon.svg)  |   |  |
| [Reserved disk space percentage](#ibm_eventstreams_instance_reserved_disk_space_percent) |  ![Checkmark icon](../../icons/checkmark-icon.svg)  |   |  |
| [Schema greatest version percentage](#ibm_eventstreams_instance_schema_registry_schema_versions_greatest_percentage) |  ![Checkmark icon](../../icons/checkmark-icon.svg)  |   |  |
| [Schema used percentage](#ibm_eventstreams_instance_schema_registry_schemas_used_percentage) |  ![Checkmark icon](../../icons/checkmark-icon.svg)  |   |  |
| [Stable consumer groups](#ibm_eventstreams_instance_stable_consumergroups) |  ![Checkmark icon](../../icons/checkmark-icon.svg)  |   |  |
| [Topic bytes in per second](#ibm_eventstreams_instance_topic_bytes_in_per_second) |  ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| [Topic bytes out per second](#ibm_eventstreams_instance_topic_bytes_out_per_second) |  ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) | ![Checkmark icon](../../icons/checkmark-icon.svg) |
| [Utilized disk space percentage](#ibm_eventstreams_instance_utilised_disk_space_percent) |  ![Checkmark icon](../../icons/checkmark-icon.svg)  |   |  |  <br/> 
{: caption="Table 1: Metrics Available by Plan Names" caption-side="top"}

---

## Metrics available with Mirroring enabled
{: metrics-mirroring}

| Metric Name |Enterprise|Lite|Standard|
|-----------|--------|--------|--------|
| [Mirroring throughput](#ibm_eventstreams_instance_mirroring_throughput) |  ![Checkmark icon](../../icons/checkmark-icon.svg)  |   |  |
| [Mirroring latency](#ibm_eventstreams_instance_mirroring_latency) |  ![Checkmark icon](../../icons/checkmark-icon.svg)  |   |  |
<br/> 
{: caption="Table 2: Metrics Available for Mirroring" caption-side="top"}

---

### Authentication failures
{: #ibm_eventstreams_kafka_authentication_failure_total}

Incrementing count of the number of authentication failures

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_kafka_authentication_failure_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 2: Authentication failures metric metadata" caption-side="top"}

Ideally zero. A non-zero value on this indicates client(s) are attempting to connect using invalid credentials. Ensure all clients are using valid credentials.??

### Consume message conversion time
{: #ibm_eventstreams_instance_consume_conversions_time_quantile}

Indicates the accumulated time spent performing message conversion from clients that are consuming using older protocol versions

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_consume_conversions_time_quantile`|
| `Metric Type` | `gauge` |
| `Value Type`  | `second` |
| `Segment By` | `Service instance, Quantile, Service instance name` |
{: caption="Table 3: Consume message conversion time metric metadata" caption-side="top"}

Ideally zero, as non-zero indicates clients are experiencing additional latency due to using an older protocol level. Those clients are down-level and should be upgraded. Ensure that all clients are at the latest levels.

### Estimated connected clients percentage
{: #ibm_eventstreams_kafka_recommended_max_connected_clients_percent}

The percentage of maximum number of connected clients

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_kafka_recommended_max_connected_clients_percent`|
| `Metric Type` | `gauge` |
| `Value Type`  | `percent` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 4: Estimated connected clients percentage metric metadata" caption-side="top"}

This is for information to help you monitor trends in your usage. Refer to [{{site.data.keyword.messagehub}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/EventStreams?topic=EventStreams-plan_choose){:new_window} to determine what the recommended limits are for your plan and cluster.

### Inactive consumer groups
{: #ibm_eventstreams_instance_inactive_consumergroups}

The number of inactive consumer groups in an Event Streams instance

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_inactive_consumergroups`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 5: Inactive consumer groups metric metadata" caption-side="top"}

This is for information only and is not an issue. Spikes indicate that a set of consumer groups have stopped sending messages.

### Instance bytes in per second
{: #ibm_eventstreams_instance_bytes_in_per_second}

The number of bytes produced per second to an Event Streams instance

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_bytes_in_per_second`|
| `Metric Type` | `gauge` |
| `Value Type`  | `byte` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 6: Instance bytes in per second metric metadata" caption-side="top"}

This is for information to help you monitor trends in your usage of how many incoming or outgoing MB/s your clients are transferring to/from your cluster. Refer to [{{site.data.keyword.messagehub}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/EventStreams?topic=EventStreams-plan_choose){:new_window} to determine what the recommended limits are for your plan and cluster.

### Instance bytes out per second
{: #ibm_eventstreams_instance_bytes_out_per_second}

The number of bytes consumed per second from an Event Streams instance

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_bytes_out_per_second`|
| `Metric Type` | `gauge` |
| `Value Type`  | `byte` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 7: Instance bytes out per second metric metadata" caption-side="top"}

This is for information to help you monitor trends in your usage of how many incoming or outgoing MB/s your clients are transferring to/from your cluster. Refer to [{{site.data.keyword.messagehub}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/EventStreams?topic=EventStreams-plan_choose){:new_window} to determine what the recommended limits are for your plan and cluster.


### Missing SNI connections
{: #ibm_eventstreams_kafka_missing_sni_host_total}

Incrementing count of the number of connections rejected due to not supporting the SNI extension to TLS

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_kafka_missing_sni_host_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 8: Missing SNI connections metric metadata" caption-side="top"}

Ideally this should be zero. It indicates clients that are not configured correctly. Clients must use the SNI extension for TLS in order to connect to the service. If this value is non-zero, then ensure that all clients are at correct level and configured correctly for [SNI ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/EventStreams?topic=EventStreams-kafka_using){:new_window}.


### Number of partitions
{: #ibm_eventstreams_instance_partitions}

The number of leader partitions in an Event Streams instance

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_partitions`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 9: Number of partitions metric metadata" caption-side="top"}

This is for information to help you monitor trends in your usage. Refer to [{{site.data.keyword.messagehub}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/EventStreams?topic=EventStreams-plan_choose){:new_window} to determine what the recommended limits are for your plan and cluster.

### Number of topics
{: #ibm_eventstreams_instance_topics}

The number of topics in an Event Streams instance

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_topics`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 10: Number of topics metric metadata" caption-side="top"}

### Produce message conversion time
{: #ibm_eventstreams_instance_produce_conversions_time_quantile}

Indicates the accumulated time spent performing message conversion from clients that are producing using older protocol versions

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_produce_conversions_time_quantile`|
| `Metric Type` | `gauge` |
| `Value Type`  | `second` |
| `Segment By` | `Service instance, Quantile, Service instance name` |
{: caption="Table 11: Produce message conversion time metric metadata" caption-side="top"}

Ideally zero. A consistent growth in this indicates that some clients are down-level and should be upgraded. Ensure that all clients are at the latest levels.

### Rebalancing consumer groups
{: #ibm_eventstreams_instance_rebalancing_consumergroups}

The number of rebalancing consumer groups in an Event Streams instance

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_rebalancing_consumergroups`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 12: Rebalancing consumer groups metric metadata" caption-side="top"}

Whilst it is expected that this figure is occasionally >0 (as broker restarts happen frequently,) sustained high levels suggest that consumers may be restarting frequently and leaving/rejoining the consumer groups. Check you client logs.

### Reserved disk space percentage
{: #ibm_eventstreams_instance_reserved_disk_space_percent}

The percentage of reserved disk space required for all allocated partitions if fully utilized

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_reserved_disk_space_percent`|
| `Metric Type` | `gauge` |
| `Value Type`  | `percent` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 13: Reserved disk space percentage metric metadata" caption-side="top"}

Shows the % of disk space that would be used if your topics are filled to the extent of their configured retention size.


### Schema greatest version percentage
{: #ibm_eventstreams_instance_schema_registry_schema_versions_greatest_percentage}

The percentage of schema version capacity used for the schema with the greatest number of versions in the registry

| Metadata | Description |
|-------------|-------------------------------------------------------------------------------|
| `Metric Name` | `ibm_eventstreams_instance_schema_registry_schema_versions_greatest_percentage`|
| `Metric Type` | `gauge` |
| `Value Type`  | `percent` |
| `Segment By`  | `Service instance, Service instance name` |
{: caption="Table 14: Schema greatest version percentage metric metadata" caption-side="top"}

### Schema used percentage
{: #ibm_eventstreams_instance_schema_registry_schemas_used_percentage}

The percentage of schema capacity used in the schema registry

| Metadata | Description |
|-------------|-------------------------------------------------------------------|
| `Metric Name` | `ibm_eventstreams_instance_schema_registry_schemas_used_percentage`|
| `Metric Type` | `gauge` |
| `Value Type`  | `percent` |
| `Segment By`  | `Service instance, Service instance name` |
{: caption="Table 15: Schema used percentage metric metadata" caption-side="top"}

### Stable consumer groups
{: #ibm_eventstreams_instance_stable_consumergroups}

The number of stable consumer groups in an Event Streams instance

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_stable_consumergroups`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 16: Stable consumer groups metric metadata" caption-side="top"}

Use in conjunction with re-balancing consumer groups. If this is consistently zero and re-balancing high, then it indicates a cluster problem. If this is non-zero and re-balancing high, then it indicates a consumer group issue.

### Topic bytes in per second
{: #ibm_eventstreams_instance_topic_bytes_in_per_second}

The number of bytes produced per second to a topic

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_topic_bytes_in_per_second`|
| `Metric Type` | `gauge` |
| `Value Type`  | `byte` |
| `Segment By` | `Service instance, IBM Event Streams Kafka topic, Service instance name` |
{: caption="Table 17: Topic bytes in per second metric metadata" caption-side="top"}

This is for information to help you monitor trends in your usage, particularly if any topics are producing unusually more or less throughput than expected.

### Topic bytes out per second
{: #ibm_eventstreams_instance_topic_bytes_out_per_second}

The number of bytes consumed per second from a topic

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_topic_bytes_out_per_second`|
| `Metric Type` | `gauge` |
| `Value Type`  | `byte` |
| `Segment By` | `Service instance, IBM Event Streams Kafka topic, Service instance name` |
{: caption="Table 18: Topic bytes out per second metric metadata" caption-side="top"}

This is for information to help you monitor trends in your usage, particularly if any topics are consuming unusually more or less throughput than expected.

### Utilized disk space percentage
{: #ibm_eventstreams_instance_utilised_disk_space_percent}

The percentage of currently utilized disk space

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_utilised_disk_space_percent`|
| `Metric Type` | `gauge` |
| `Value Type`  | `percent` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 19: Utilized disk space percentage metric metadata" caption-side="top"}

This is for information to help you monitor trends in your usage. Refer to [{{site.data.keyword.messagehub}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/EventStreams?topic=EventStreams-plan_choose){:new_window} to determine what the recommended limits are for your plan and cluster.

---




### Mirroring_throughput
{: #ibm_eventstreams_instance_mirroring_throughput}

The bytes per second of mirroring throughput from the source Event Streams instance.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | ` ibm_eventstreams_instance_mirroring_throughput_bytes_per_second`|
| `Metric Type` | `gauge` |
| `Value Type`  | `bytes_per_second` |
| `Segment By` | `Service instance, IBM Event Streams Kafka topic, Service instance name` |
{: caption="Table 21: Mirroring throughput" caption-side="top"}

This is useful to see if mirroring is active and for capacity planning.

### Mirroring_latency
{: #ibm_eventstreams_instance_mirroring_latency}

The per-topic mirroring latency in seconds from the source Event Streams instance.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_mirroring_latency_seconds`|
| `Metric Type` | `gauge` |
| `Value Type`  | `seconds` |
| `Segment By` | `Service instance, IBM Event Streams Kafka topic, Service instance name` |
{: caption="Table 22: Mirroring latency" caption-side="top"}

This is useful to determine how far behind a topic on the target cluster is.

---

## Attributes for segmentation
{: attributes}

### Global attributes
{: global-attributes}

The following attributes are available for segmenting all of the metrics listed above

| Attribute | Attribute Name | Attribute Description |
|-----------|----------------|-----------------------|
| `Cloud Type` | `ibm_ctype` | The cloud type is a value of public, dedicated or local |
| `Location` | `ibm_location` | The location of the monitored resource - this may be a region, data center or global |
| `Scope` | `ibm_scope` | The scope is the account, organization or space GUID associated with this metric |
| `Service name` | `ibm_service_name` | Name of the service generating this metric |
| `Service instance` | `ibm_service_instance` | The service instance GUID identifies the instance the metric is associated with |
| `Service instance name` | `ibm_service_instance_name` | The service instance name provides the user-provided name of the service instance which isn't necessarily a unique value depending on the name provided by the user. |
| `Resource group` | `ibm_resource_group_name` | The resource group name where the service instance was created |

### Additional attributes
{: additional-attributes}

The following attributes are available for segmenting one or more attributes as described in the reference above.  Please see the individual metrics for segmentation options.

| Attribute | Attribute Name | Attribute Description |
|-----------|----------------|-----------------------|
| `IBM Event Streams Kafka topic` | `ibm_eventstreams_topic` | IBM Event Streams Kafka topic |
| `Quantile` | `ibm_quantile` | The quantile represented when a metric supports segmenting by quantile |


<br/>

For more information about enabling platform metrics from the {{site.data.keyword.messagehub}} dashboard and viewing metrics, see [Monitoring Event Streams metrics ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/monitoring?topic=monitoring-monitoring){:new_window}.
