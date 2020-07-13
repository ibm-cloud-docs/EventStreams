---

copyright:
  years: 2015, 2020
lastupdated: "2020-07-13"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka, Sysdig, metrics, cost, billing, opting in

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

[{{site.data.keyword.mon_full}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/Monitoring-with-Sysdig?topic=Sysdig-getting-started#getting-started)
 is a third-party cloud-native, and container-intelligence management system that you can include as part of your {{site.data.keyword.cloud_notm}} architecture. Use it to gain operational visibility into the performance and health of your applications, services, and platforms. It offers administrators, DevOps teams, and developers full stack telemetry with advanced features to monitor and troubleshoot, define alerts, and design custom dashboards.
{:shortdesc}


## Opting in to and enabling {{site.data.keyword.messagehub}} metrics
{: #opt_in_metrics}

Before you can start using {{site.data.keyword.messagehub}} Sysdig metrics, you must first opt in and then enable platform metrics by completing the following steps: 

1. Enable platform metrics for {{site.data.keyword.messagehub}}. For more information, see [Enabling platform metrics ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/Monitoring-with-Sysdig?topic=Sysdig-platform_metrics_enabling){:new_window}. The owner of the account has full access to the this metrics data. For more information about managing access for other users see [Getting started tutorial for {{site.data.keyword.mon_full}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/Monitoring-with-Sysdig?topic=Sysdig-getting-started#prereqs){:new_window}. 

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

For more information, see [{{site.data.keyword.mon_full_notm}} pricing ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/Monitoring-with-Sysdig?topic=Sysdig-pricing_plans). 


## {{site.data.keyword.messagehub}} metrics details
{: #metric_details}

The following tables describe the specific metrics provided by {{site.data.keyword.messagehub}} for each plan. 




## Metrics available by Service Plan
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

## Attributes for Segmentation
{: attributes}

### Global Attributes
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

### Additional Attributes
{: additional-attributes}

The following attributes are available for segmenting one or more attributes as described in the reference above.  Please see the individual metrics for segmentation options.

| Attribute | Attribute Name | Attribute Description |
|-----------|----------------|-----------------------|
| `IBM Event Streams Kafka topic` | `ibm_eventstreams_topic` | IBM Event Streams Kafka topic |
| `Quantile` | `ibm_quantile` | The quantile represented when a metric supports segmenting by quantile |


<br/>

For more information about enabling platform metrics from the {{site.data.keyword.messagehub}} dashboard and viewing metrics, see [Monitoring Event Streams metrics ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/observability-monitoring?topic=observability-monitoring-monitor-sysdig){:new_window}.






