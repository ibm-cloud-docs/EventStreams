---

copyright:
  years: 2015, 2022
lastupdated: "2022-11-28"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka, IBM Cloud Monitoring, metrics, cost, billing, opting in

subcollection: EventStreams

---

{{site.data.keyword.attribute-definition-list}}

# Monitoring {{site.data.keyword.messagehub}} metrics by using {{site.data.keyword.mon_full_notm}}
{: #metrics}

[{{site.data.keyword.mon_full}}](/docs/monitoring?topic=monitoring-getting-started) is a third-party cloud-native, and container-intelligence management system that you can include as part of your {{site.data.keyword.cloud_notm}} architecture. Use it to gain operational visibility into the performance and health of your applications, services, and platforms. It offers administrators, DevOps teams, and developers full stack telemetry with advanced features to monitor and troubleshoot, define alerts, and design custom dashboards.
{: shortdesc}

## Opting in to and enabling {{site.data.keyword.messagehub}} metrics
{: #opt_in_metrics}

{{site.data.keyword.messagehub}} metrics can broadly be categorized into two different groups: **Default** and **Enhanced**.

### Enabling default {{site.data.keyword.messagehub}} metrics
{: #enabling_default_metrics}

Before you can start to use {{site.data.keyword.messagehub}} {{site.data.keyword.mon_full_notm}} metrics, you must first opt in, and then enable platform metrics by completing the following steps:

1. Enable platform metrics for {{site.data.keyword.messagehub}}. For more information, see [Enabling platform metrics](/docs/monitoring?topic=monitoring-platform_metrics_enabling){: external}. 

   The owner of the account has full access to this metrics data. For more information about managing access for other users, see [Getting started with {{site.data.keyword.mon_full_notm}} - manage user access](/docs/monitoring?topic=monitoring-getting-started#getting-started-step1){: external}.

2. To navigate from the {{site.data.keyword.messagehub}} instance page to the {{site.data.keyword.monitoringshort}} dashboard, click the three vertical dots of the instance page (**Service instance options**) and select **Monitoring**.

   On your first usage, you might see a welcome wizard. To advance to the dashboard selection menu, select **Next** and then **Skip** on the **Choosing an installation method** page. Accept the prompts that follow. You can then select the **IBM Event Streams** or **IBM Event Streams (Enterprise)** dashboard, depending on the plan that you use.

### Enabling enhanced {{site.data.keyword.messagehub}} metrics
{: #opt_in_enhanced_metrics}

The enhanced {{site.data.keyword.messagehub}} metrics consist of two groups; `topic` and `consumers`. You can opt in to either one or both. The metrics available are described in the [topic](#metrics-topic) and [consumers](#metrics-consumers) tables.

Enabling enhanced metrics introduces more global gauge metric and therefore increases the costs.

Before you can start to use enhanced {{site.data.keyword.messagehub}} metrics, you must first enable them by completing the following step:

* Run the following command to update the service instance to start using enhanced metrics:
   
   ```bash
   ibmcloud resource service-instance-update <instance-name> -p '{"metrics":["topic","consumers"]}'
   ```
   {: codeblock}

When enhanced metrics are enabled, depending on the selection, new dashboards are available; **IBM Event Streams(Topic)** and **IBM Event Streams(Consumers)**.

To opt out of enhanced metrics, run the following command:

   ```bash
   ibmcloud resource service-instance-update <instance-name> -p '{"metrics":[]}'
   ```
   {: codeblock}

Dashboards are available only after metrics started to be recorded; it might take a few minutes to initialize.
{: note}

## {{site.data.keyword.messagehub}} metrics cost information
{: #metric_costs}

Before you opt in to using {{site.data.keyword.monitoringshort}} metrics, be aware of the cost of doing so. The estimated cost depends on the following considerations:

- The {{site.data.keyword.messagehub}} plan that you use.
- How many unique time series are sent for each plan.
- The number of topics that you created.

| Plan            | Topics         | Number of time series  | Monthly cost |
|------------------|--------------|------------------|------------------|
| `Lite`          | 1        |1 x 2 + 5 = 7 | $0.08 x 7 = $0.56      |
| `Standard` | 1      | 1 x 2 + 5 = 7 | $0.08 x 7 = $0.56   |
| | 10      | 10 x 2 + 5 = 25 | $0.08 x 25 = $2   |
|  | 100      | 100 x 2 + 5 = 205 | $0.08 x 205 = $16.40   |
| `Enterprise` | 1        | 1 x 2 + 19 = 21 | $0.08 x 21 = $1.68  |
|           | 10        | 10 x 2 + 19 = 39 | $0.08 x 39 = $3.12  |
|         | 100        |  100 x 2 + 19 = 219   | $0.08 x 219 = $17.52  |
|        | 1000        |  1000 x 2 + 19 = 2019  | $0.08 x 2019 = $161.52   |
|      | 3000        |   3000 x 2 + 19 = 6019    | $0.08 x 6019 = $481.52  |
{: caption="Table 1. Cost for each plan" caption-side="bottom"}

Enabling mirroring for Enterprise clusters introduces one more global gauge metric and an extra gauge metric per topic in the target cluster (with the target cluster already emitting metrics in accordance with the preceding table), therefore increasing the costs.

For more information, see [{{site.data.keyword.monitoringshort}} pricing](/docs/monitoring?topic=monitoring-pricing_plans).

## {{site.data.keyword.messagehub}} metrics details
{: #metric_details}

The following tables describe the specific metrics that are provided by {{site.data.keyword.messagehub}} for each plan.

## Metrics available by service plan
{: #metrics-by-plan}

| Metric name |Enterprise|Lite|Standard|
|-----------|--------|--------|--------|
| [Authentication failures](#ibm_eventstreams_kafka_authentication_failure_total) |  ![Checkmark icon](../icons/checkmark-icon.svg)  |   |  |
| [Connected clients software name and version](#ibm_eventstreams_connected_clients_software_name_and_version) |  ![Checkmark icon](../icons/checkmark-icon.svg)  |   |  |
| [Consume message conversion time](#ibm_eventstreams_instance_consume_conversions_time_quantile) |  ![Checkmark icon](../icons/checkmark-icon.svg)  |   |  |
| [Estimated connected clients percentage](#ibm_eventstreams_kafka_recommended_max_connected_clients_percent) |  ![Checkmark icon](../icons/checkmark-icon.svg) | ![Checkmark icon](../icons/checkmark-icon.svg) | ![Checkmark icon](../icons/checkmark-icon.svg) |
| [Inactive consumer groups](#ibm_eventstreams_instance_inactive_consumergroups) |  ![Checkmark icon](../icons/checkmark-icon.svg)  |   |  |
| [Instance bytes in per second](#ibm_eventstreams_instance_bytes_in_per_second) |  ![Checkmark icon](../icons/checkmark-icon.svg) | ![Checkmark icon](../icons/checkmark-icon.svg) | ![Checkmark icon](../icons/checkmark-icon.svg) |
| [Instance bytes out per second](#ibm_eventstreams_instance_bytes_out_per_second) |  ![Checkmark icon](../icons/checkmark-icon.svg) | ![Checkmark icon](../icons/checkmark-icon.svg) | ![Checkmark icon](../icons/checkmark-icon.svg) |
| [Missing SNI connections](#ibm_eventstreams_kafka_missing_sni_host_total) |  ![Checkmark icon](../icons/checkmark-icon.svg)  |   |  |
| [Number of offline partitions](#ibm_eventstreams_kafka_offline_partitions) |  ![Checkmark icon](../icons/checkmark-icon.svg) |  |  |
| [Number of partitions](#ibm_eventstreams_instance_partitions) |  ![Checkmark icon](../icons/checkmark-icon.svg) | ![Checkmark icon](../icons/checkmark-icon.svg) | ![Checkmark icon](../icons/checkmark-icon.svg) |
| [Number of topics](#ibm_eventstreams_instance_topics) |  ![Checkmark icon](../icons/checkmark-icon.svg) | ![Checkmark icon](../icons/checkmark-icon.svg) | ![Checkmark icon](../icons/checkmark-icon.svg) |
| [Number of under in-sync replica partitions](#ibm_eventstreams_kafka_under_minisr_partitions) |  ![Checkmark icon](../icons/checkmark-icon.svg) | |  |
| [Produce message conversion time](#ibm_eventstreams_instance_produce_conversions_time_quantile) |  ![Checkmark icon](../icons/checkmark-icon.svg)  |   |  |
| [Rebalancing consumer groups](#ibm_eventstreams_instance_rebalancing_consumergroups) |  ![Checkmark icon](../icons/checkmark-icon.svg)  |   |  |
| [Reserved disk space percentage](#ibm_eventstreams_instance_reserved_disk_space_percent) |  ![Checkmark icon](../icons/checkmark-icon.svg)  |   |  |
| [Rest-producer requests per second](#ibm_eventstreams_instance_rest_producer_requests_per_sec) |  ![Checkmark icon](../icons/checkmark-icon.svg)  |   |  |
| [Schema greatest version percentage](#ibm_eventstreams_instance_schema_registry_schema_versions_greatest_percentage) |  ![Checkmark icon](../icons/checkmark-icon.svg)  |   |  |
| [Schema used percentage](#ibm_eventstreams_instance_schema_registry_schemas_used_percentage) |  ![Checkmark icon](../icons/checkmark-icon.svg)  |   |  |
| [Stable consumer groups](#ibm_eventstreams_instance_stable_consumergroups) |  ![Checkmark icon](../icons/checkmark-icon.svg)  |   |  |
| [Topic bytes in per second](#ibm_eventstreams_instance_topic_bytes_in_per_second) |  ![Checkmark icon](../icons/checkmark-icon.svg) | ![Checkmark icon](../icons/checkmark-icon.svg) | ![Checkmark icon](../icons/checkmark-icon.svg) |
| [Topic bytes out per second](#ibm_eventstreams_instance_topic_bytes_out_per_second) |  ![Checkmark icon](../icons/checkmark-icon.svg) | ![Checkmark icon](../icons/checkmark-icon.svg) | ![Checkmark icon](../icons/checkmark-icon.svg) |
| [Used disk space percentage](#ibm_eventstreams_instance_utilised_disk_space_percent) |  ![Checkmark icon](../icons/checkmark-icon.svg)  |   |  |   /n 
{: caption="Table 2. Metrics Available by Plan Names" caption-side="top"}

## Metrics available with mirroring enabled
{: #metrics-mirroring}

| Metric name |Enterprise|Lite|Standard|
|-----------|--------|--------|--------|
| [Mirroring throughput](#ibm_eventstreams_instance_mirroring_throughput) |  ![Checkmark icon](../icons/checkmark-icon.svg)  |   |  |
| [Mirroring latency](#ibm_eventstreams_instance_mirroring_latency) |  ![Checkmark icon](../icons/checkmark-icon.svg)  |   |  |
{: caption="Table 3. Metrics available for mirroring" caption-side="bottom"}

## Enhanced metrics available with topic enabled
{: #metrics-topic}

| Metric name |Enterprise|Lite|Standard|
|-----------|--------|--------|--------|
| [Maximum partition retention percentage](#ibm_eventstreams_instance_max_partition_retention_percent) |  ![Checkmark icon](../icons/checkmark-icon.svg)|  | |
| [Topic size](#ibm_eventstreams_instance_topic_size) |  ![Checkmark icon](../icons/checkmark-icon.svg) |  | |
{: caption="Table 4. Metrics available for topic" caption-side="bottom"}

### Metrics cost information with topic enabled
{: #metrics_cost_topic}

 Topics| Number of time series  | Monthly cost |
|----------------|-------|----------|
| 1        | 1 x 2 = 2         | $0.08 x 2 = $0.16     |
| 10        | 10 x 2  = 20     | $0.08 x 20 = $1.60  |
| 100        |  100 x 2 = 200    | $0.08 x 200 = $16.00  |
{: caption="Table 5. Cost for topic metrics" caption-side="bottom"}

## Enhanced metrics available with consumers enabled
{: #metrics-consumers}

| Metric name |Enterprise|Lite|Standard|
|-----------|--------|--------|--------|
| [Consumer groups lag](#ibm_eventstreams_instance_consumer_groups_lag) |  ![Checkmark icon](../icons/checkmark-icon.svg)  | | |
{: caption="Table 6. Metrics available for consumers" caption-side="bottom"}

### Metrics cost information with consumers enabled
{: #metrics-cost}

| Consumer group | Topics| Partitions| Number of time series  | Monthly cost |
|----------------|-------|----------|------------------------|--------------|
| 1              | 1     | 3        | 1 x 1 x 3  = 3         | $0.08 x 3 = $0.24     |
| 10             | 10    | 3        | 10 x 10 x 3 = 300      | $0.08 x 300 = $24.00  |
| 25             | 25    | 6        |  25 x 25 x 6 = 3750    | $0.08 x 15000 = $300.00  |
{: caption="Table 7. Cost for consumers metric" caption-side="bottom"}

### Authentication failures
{: #ibm_eventstreams_kafka_authentication_failure_total}

Incrementing count of the number of authentication failures

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_kafka_authentication_failure_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 8. Authentication failures metric metadata" caption-side="bottom"}

Ideally zero. A nonzero value on this indicates that clients attempt to connect by using invalid credentials. Ensure that all clients are using valid credentials.

### Consume message conversion time
{: #ibm_eventstreams_instance_consume_conversions_time_quantile}

Indicates that the accumulated time spent performing message conversion from clients that are consuming by using older protocol versions.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_consume_conversions_time_quantile`|
| `Metric Type` | `gauge` |
| `Value Type`  | `second` |
| `Segment By` | `Service instance, Quantile, Service instance name` |
{: caption="Table 9. Consume message conversion time metric metadata" caption-side="bottom"}

Ideally zero, as nonzero indicates that clients are experiencing more latency because of using an older protocol level. Those clients are down-level and must be upgraded. Ensure that all clients are at the latest levels.

### Estimated connected clients percentage
{: #ibm_eventstreams_kafka_recommended_max_connected_clients_percent}

The percentage of maximum number of connected clients.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_kafka_recommended_max_connected_clients_percent`|
| `Metric Type` | `gauge` |
| `Value Type`  | `percent` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 10. Estimated connected clients percentage metric metadata" caption-side="bottom"}

This is for information to help you monitor trends in your usage. Refer to [{{site.data.keyword.messagehub}}](/docs/EventStreams?topic=EventStreams-plan_choose){: external} to determine what the recommended limits are for your plan and cluster.

### Connected clients software name and version
{: #ibm_eventstreams_connected_clients_software_name_and_version}

The number of connected clients with a particular client software name and version.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_connected_clients_software_name_and_version`|
| `Metric Type` | `gauge` |
| `Value Type`  | `number` |
| `Segment By` | `Client software name, Client software version` |
{: caption="Table 11. Connected clients software name and version metric metadata" caption-side="bottom"}

This is for information to help you monitor the software name and version data of the active clients that are connected to the {{site.data.keyword.messagehub}} instance.

Client software name and version are available for the Kafka client (Java version 2.4 or later, and other implementations that support software name and version) as described in [KIP-8855](https://issues.apache.org/jira/browse/KAFKA-8855). If the client software name and version are not available, these are set as `unknown`.

### Inactive consumer groups
{: #ibm_eventstreams_instance_inactive_consumergroups}

The number of inactive consumer groups in an {{site.data.keyword.messagehub}} instance.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_inactive_consumergroups`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 12. Inactive consumer groups metric metadata" caption-side="bottom"}

This is for information only and is not an issue. Spikes indicate that a set of consumer groups stopped sending messages.

### Instance bytes in per second
{: #ibm_eventstreams_instance_bytes_in_per_second}

The number of bytes produced per second to an {{site.data.keyword.messagehub}} instance.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_bytes_in_per_second`|
| `Metric Type` | `gauge` |
| `Value Type`  | `byte` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 13. Instance bytes in per second metric metadata" caption-side="bottom"}

This is for information to help you monitor trends in your usage of how many incoming or outgoing MB/s your clients are transferring to and from your cluster. Refer to [{{site.data.keyword.messagehub}}](/docs/EventStreams?topic=EventStreams-plan_choose){: external} to determine what the recommended limits are for your plan and cluster.

### Instance bytes out per second
{: #ibm_eventstreams_instance_bytes_out_per_second}

The number of bytes consumed per second from an {{site.data.keyword.messagehub}} instance.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_bytes_out_per_second`|
| `Metric Type` | `gauge` |
| `Value Type`  | `byte` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 14. Instance bytes out per second metric metadata" caption-side="bottom"}

This is for information to help you monitor trends in your usage of how many incoming or outgoing MB/s your clients are transferring to and from your cluster. Refer to [{{site.data.keyword.messagehub}}](/docs/EventStreams?topic=EventStreams-plan_choose){: external} to determine what the recommended limits are for your plan and cluster.

### Missing SNI connections
{: #ibm_eventstreams_kafka_missing_sni_host_total}

Incrementing count of the number of connections rejected due to not supporting the SNI extension to TLS.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_kafka_missing_sni_host_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 15. Missing SNI connections metric metadata" caption-side="bottom"}

Ideally this should be zero. It indicates clients that are not configured correctly. Clients must use the SNI extension for TLS to connect to the service. If this value is nonzero, ensure that all clients are at correct level and configured correctly for [SNI](/docs/EventStreams?topic=EventStreams-kafka_using){: external}.

### Number of offline partitions
{: #ibm_eventstreams_kafka_offline_partitions}

The number of partitions offline in an {{site.data.keyword.messagehub}} instance.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_kafka_offline_partitions`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance` |
{: caption="Table 16. Number of offline partitions metric metadata" caption-side="bottom"}

Ideally this value should be zero. A nonzero value might indicate to a temporary issue with the cluster. It might also indicate to a Kafka partition leader election difficulty.

### Number of partitions
{: #ibm_eventstreams_instance_partitions}

The number of leader partitions in an {{site.data.keyword.messagehub}} instance.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_partitions`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 17. Number of partitions metric metadata" caption-side="bottom"}

This is for information to help you monitor trends in your usage. Refer to [{{site.data.keyword.messagehub}}](/docs/EventStreams?topic=EventStreams-plan_choose){: external} to determine what the recommended limits are for your plan and cluster.

### Number of topics
{: #ibm_eventstreams_instance_topics}

The number of topics in an {{site.data.keyword.messagehub}} instance.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_topics`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 18. Number of topics metric metadata" caption-side="bottom"}

### Number of under in-sync replica partitions
{: #ibm_eventstreams_kafka_under_minisr_partitions}

The number of partitions with fewer than two in-sync replicas.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_kafka_under_minisr_partitions`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance` |
{: caption="Table 19. Number of under in-sync replica partitions metric metadata" caption-side="bottom"}

Ideally this value should be zero. A nonzero value might highlight a temporary issue with the cluster.

### Produce message conversion time
{: #ibm_eventstreams_instance_produce_conversions_time_quantile}

Indicates that the accumulated time spent performing message conversion from clients that are producing by using older protocol versions.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_produce_conversions_time_quantile`|
| `Metric Type` | `gauge` |
| `Value Type`  | `second` |
| `Segment By` | `Service instance, Quantile, Service instance name` |
{: caption="Table 20. Produce message conversion time metric metadata" caption-side="bottom"}

Ideally zero. A consistent growth in this indicates that some clients are down-level and should be upgraded. Ensure that all clients are at the latest levels.

### Rebalancing consumer groups
{: #ibm_eventstreams_instance_rebalancing_consumergroups}

The number of rebalancing consumer groups in an {{site.data.keyword.messagehub}} instance.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_rebalancing_consumergroups`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 21. Rebalancing consumer groups metric metadata" caption-side="top"}

While it is expected that this figure is occasionally >0 (as broker restarts happen frequently,) sustained high levels suggest that consumers might be restarting frequently and leaving or rejoining the consumer groups. Check you client logs.

### Reserved disk space percentage
{: #ibm_eventstreams_instance_reserved_disk_space_percent}

The percentage of reserved disk space that is required for all allocated partitions if fully used.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_reserved_disk_space_percent`|
| `Metric Type` | `gauge` |
| `Value Type`  | `percent` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 22. Reserved disk space percentage metric metadata" caption-side="bottom"}

Shows the percentage of disk space that would be used if your topics were filled to the extent of their configured retention size.

### Schema greatest version percentage
{: #ibm_eventstreams_instance_schema_registry_schema_versions_greatest_percentage}

The percentage of schema version capacity used for the schema with the greatest number of versions in the registry.

| Metadata | Description |
|-------------|-------------------------------------------------------------------------------|
| `Metric Name` | `ibm_eventstreams_instance_schema_registry_schema_versions_greatest_percentage`|
| `Metric Type` | `gauge` |
| `Value Type`  | `percent` |
| `Segment By`  | `Service instance, Service instance name` |
{: caption="Table 23. Schema greatest version percentage metric metadata" caption-side="bottom"}

### Schema used percentage
{: #ibm_eventstreams_instance_schema_registry_schemas_used_percentage}

The percentage of schema capacity used in the schema registry.

| Metadata | Description |
|-------------|-------------------------------------------------------------------|
| `Metric Name` | `ibm_eventstreams_instance_schema_registry_schemas_used_percentage`|
| `Metric Type` | `gauge` |
| `Value Type`  | `percent` |
| `Segment By`  | `Service instance, Service instance name` |
{: caption="Table 24. Schema used percentage metric metadata" caption-side="bottom"}

### Stable consumer groups
{: #ibm_eventstreams_instance_stable_consumergroups}

The number of stable consumer groups in an {{site.data.keyword.messagehub}} instance.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_stable_consumergroups`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 25. Stable consumer groups metric metadata" caption-side="bottom"}

Use along with rebalancing consumer groups. If this is consistently zero and rebalancing high, then it indicates a cluster problem. If this is nonzero and rebalancing high, it indicates a consumer group issue.

### Topic bytes in per second
{: #ibm_eventstreams_instance_topic_bytes_in_per_second}

The number of bytes produced per second to a topic.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_topic_bytes_in_per_second`|
| `Metric Type` | `gauge` |
| `Value Type`  | `byte` |
| `Segment By` | `Service instance, IBM Event Streams Kafka topic, Service instance name` |
{: caption="Table 26. Topic bytes in per second metric metadata" caption-side="bottom"}

This is for information to help you monitor trends in your usage, particularly if any topics are producing unusually more or less throughput than expected.

### Topic bytes out per second
{: #ibm_eventstreams_instance_topic_bytes_out_per_second}

The number of bytes consumed per second from a topic.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_topic_bytes_out_per_second`|
| `Metric Type` | `gauge` |
| `Value Type`  | `byte` |
| `Segment By` | `Service instance, IBM Event Streams Kafka topic, Service instance name` |
{: caption="Table 27. Topic bytes out per second metric metadata" caption-side="bottom"}

This is for information to help you monitor trends in your usage, particularly if any topics are consuming unusually more or less throughput than expected.

### Used disk space percentage
{: #ibm_eventstreams_instance_utilised_disk_space_percent}

The percentage of currently used disk space.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_utilised_disk_space_percent`|
| `Metric Type` | `gauge` |
| `Value Type`  | `percent` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 28. Used disk space percentage metric metadata" caption-side="bottom"}

This is for information to help you monitor trends in your usage. Refer to [{{site.data.keyword.messagehub}}](/docs/EventStreams?topic=EventStreams-plan_choose){: external} to determine what the recommended limits are for your plan and cluster.

### Rest-producer requests per second
{: #ibm_eventstreams_instance_rest_producer_requests_per_sec}

Number of requests per second made to the REST Producer API.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_rest_producer_requests_per_sec`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 29: Rest-producer requests per second metric metadata" caption-side="top"}

This is for information to help you monitor usage of the REST Producer API, including use of schema encoders.

### Mirroring throughput
{: #ibm_eventstreams_instance_mirroring_throughput}

The bytes per second of mirroring throughput from the source {{site.data.keyword.messagehub}} instance.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_mirroring_throughput_bytes_per_second`|
| `Metric Type` | `gauge` |
| `Value Type`  | `bytes_per_second` |
| `Segment By` | `Service instance, IBM Event Streams Kafka topic, Service instance name` |
{: caption="Table 30. Mirroring throughput" caption-side="bottom"}

This is useful to see whether mirroring is active and for capacity planning.

### Mirroring_latency
{: #ibm_eventstreams_instance_mirroring_latency}

The per-topic mirroring latency in seconds from the source {{site.data.keyword.messagehub}} instance.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_mirroring_latency_seconds`|
| `Metric Type` | `gauge` |
| `Value Type`  | `seconds` |
| `Segment By` | `Service instance, IBM Event Streams Kafka topic, Service instance name` |
{: caption="Table 31. Mirroring latency" caption-side="bottom"}

This is useful to determine how far behind a topic on the target cluster is.

### Consumer group lag 
{: #ibm_eventstreams_instance_consumer_groups_lag}

Lag for each consumer group for each topic-partition in an {{site.data.keyword.messagehub}} instance. This metric indicates that the number of messages that are yet to be processed for each partition in a consumer group. 

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_consumer_groups_lag`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance name, IBM Event Streams consumer groups, IBM Event Streams Kafka topic, IBM Event Streams Kafka partitions` |
{: caption="Table 32. Consumer group lag metric metadata" caption-side="bottom"}

An increasing lag might highlight that the consumers in the group are not keeping pace with the rate that messages are being produced. This might require you to scale the number of consumers that process messages for the group.

It is normal for this metric to fluctuate when viewed over short time periods because of sampling and batch processing effects.
{: note}

### Maximum partition retention percentage
{: #ibm_eventstreams_instance_max_partition_retention_percent}

Maximum percentage of the retention size used for partitions of a topic.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_max_partition_retention_percent`|
| `Metric Type` | `gauge` |
| `Value Type`  | `percent` |
| `Segment By` | `Service instance, IBM Event Streams Kafka topic, Service instance name` |
{: caption="Table 33. Maximum partition retention percentage metric metadata" caption-side="bottom"}

### Topic size
{: #ibm_eventstreams_instance_topic_size}

Total disk size of all partitions of a topic.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_topic_size`|
| `Metric Type` | `gauge` |
| `Value Type`  | `byte` |
| `Segment By` | `Service instance, IBM Event Streams Kafka topic, Service instance name` |
{: caption="Table 34. Topic size metric metadata" caption-side="bottom"}

## Attributes for segmentation
{: #attributes}

### Global attributes
{: #global-attributes}

The following attributes are available for segmenting all of the listed metrics.

| Attribute | Attribute name | Attribute description |
|-----------|----------------|-----------------------|
| `Cloud Type` | `ibm_ctype` | The Cloud type is a value of public, dedicated, or local. |
| `Location` | `ibm_location` | The location of the monitored resource - this might be a region, data center or global. |
| `Scope` | `ibm_scope` | The scope is the account, organization, or space GUID associated with this metric. |
| `Service name` | `ibm_service_name` | Name of the service that generates this metric. |
| `Service instance` | `ibm_service_instance` | The service instance GUID identifies the instance that the metric is associated with. |
| `Service instance name` | `ibm_service_instance_name` | The service instance name provides the user-provided name of the service instance that isn't necessarily a unique value that depends on the name that is provided by the user. |
| `Resource` | `ibm_resource` | The resource that is measured by the service - typically an identifying name or GUID. |
| `Resource Type` | `ibm_resource_type` | The type of the resource that is measured by the service. |
| `Resource group` | `ibm_resource_group_name` | The resource group name where the service instance was created. |
{: caption="Table 35. Global attributes" caption-side="bottom"}

### More attributes
{: #additional-attributes}

The following attributes are available for segmenting one or more attributes. See the individual metrics for segmentation options.

| Attribute | Attribute name | Attribute description |
|-----------|----------------|-----------------------|
| `Client software name` | `ibm_eventstreams_clientsoftwarename` | Client software name. |
| `Client software version` | `ibm_eventstreams_clientsoftwareversion` | Client software version. |
| `IBM Event Streams Consumer Group` | `ibm_eventstreams_consumergroup` | IBM {{site.data.keyword.messagehub}} consumer group. |
| `IBM Event Streams Kafka partition` | `ibm_eventstreams_partition` | IBM {{site.data.keyword.messagehub}} Kafka partition. |
| `IBM Event Streams Kafka topic` | `ibm_eventstreams_topic` | IBM Event Streams Kafka topic. |
| `Quantile` | `ibm_quantile` | The quantile represented when a metric supports segmenting by quantile. |
| `Service instance` | `ibm_service_instance` | The service instance segment identifies the instance that the metric is associated with. |
| `Service instance name` | `ibm_service_instance_name` | The service instance name provides the user-provided name of the service instance, which isn't necessarily a unique value that depends on the name that is provided by the user. |
{: caption="Table 36. More attributes" caption-side="bottom"}

For more information about enabling platform metrics from the {{site.data.keyword.messagehub}} dashboard and viewing metrics, see [Monitoring {{site.data.keyword.messagehub}} metrics](/docs/monitoring?topic=monitoring-monitoring){: external}.
