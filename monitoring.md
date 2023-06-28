---

copyright:
  years: 2015, 2023
lastupdated: "2023-06-28"

keywords: Kafka as a service, managed Apache Kafka, cloud monitoring, metrics, cost, billing, opting in

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

2. To navigate from the {{site.data.keyword.messagehub}} instance page to the {{site.data.keyword.monitoringshort}} dashboard, click **Actions** on the instance page and select **Monitoring**.

   On your first usage, you might see a welcome wizard. To advance to the dashboard selection menu, select **Next** and then **Skip** on the **Choosing an installation method** page. Accept the prompts that follow. You can then select the **IBM {{site.data.keyword.messagehub}}** or **IBM {{site.data.keyword.messagehub}} (Enterprise)** dashboard, depending on the plan that you use.

### Enabling enhanced {{site.data.keyword.messagehub}} metrics
{: #opt_in_enhanced_metrics}

The enhanced {{site.data.keyword.messagehub}} metrics consist of three groups; `topic`, `partition` and `consumers`. You can opt in to either one, two, or all. The metrics available are described in the [topic](#metrics-topic), [partition](#metrics-partition) and [consumers](#metrics-consumers) tables.

Enabling enhanced metrics introduces more global gauge metrics and therefore increases the costs.

Before you can start to use enhanced {{site.data.keyword.messagehub}} metrics, you must first enable them by completing the following step:

* Run the following command to update the service instance to start using enhanced metrics:
   
   ```bash
   ibmcloud resource service-instance-update <instance-name> -p '{"metrics":["topic","partition","consumers"]}'
   ```
   {: codeblock}

When enhanced metrics are enabled, depending on the selection, the following new dashboards are available; **IBM {{site.data.keyword.messagehub}}(Topic)**, **IBM {{site.data.keyword.messagehub}}(Partitions)** and **IBM {{site.data.keyword.messagehub}}(Consumers)**.

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
- The number of partitions that you created.
- Whether you have topics, partitions, consumers, or all enabled.

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
| [IAM ID bytes in per second](#ibm_eventstreams_iam_id_bytes_in_per_second) |  ![Checkmark icon](../icons/checkmark-icon.svg) |   |  |
| [IAM ID bytes out per second](#ibm_eventstreams_iam_id_bytes_out_per_second) |  ![Checkmark icon](../icons/checkmark-icon.svg) |    |  |
| [Used disk space percentage](#ibm_eventstreams_instance_utilised_disk_space_percent) |  ![Checkmark icon](../icons/checkmark-icon.svg)  |   |  |   /n 
{: caption="Table 1. Metrics Available by Plan Names" caption-side="top"}

## Metrics available with mirroring enabled
{: #metrics-mirroring}

| Metric name |Enterprise|Lite|Standard|
|-----------|--------|--------|--------|
| [Mirroring throughput](#ibm_eventstreams_instance_mirroring_throughput) |  ![Checkmark icon](../icons/checkmark-icon.svg)  |   |  |
| [Mirroring latency](#ibm_eventstreams_instance_mirroring_latency) |  ![Checkmark icon](../icons/checkmark-icon.svg)  |   |  |
{: caption="Table 2. Metrics available for mirroring" caption-side="bottom"}

## Enhanced metrics available with topic enabled
{: #metrics-topic}

| Metric name |Enterprise|Lite|Standard|
|-----------|--------|--------|--------|
| [Maximum partition retention percentage](#ibm_eventstreams_instance_max_partition_retention_percent) |  ![Checkmark icon](../icons/checkmark-icon.svg)|  | |
| [Topic size](#ibm_eventstreams_instance_topic_size) |  ![Checkmark icon](../icons/checkmark-icon.svg) |  | |
{: caption="Table 3. Metrics available for topic" caption-side="bottom"}


## Enhanced metrics available with consumers enabled
{: #metrics-consumers}

| Metric name |Enterprise|Lite|Standard|
|-----------|--------|--------|--------|
| [Consumer groups lag](#ibm_eventstreams_instance_consumer_groups_lag) |  ![Checkmark icon](../icons/checkmark-icon.svg)  | | |
{: caption="Table 4. Metrics available for consumers" caption-side="bottom"}

## Enhanced metrics available with partitions enabled
{: #metrics-partition}

| Metric name |Enterprise|Lite|Standard|
|-----------|--------|--------|--------|
| [Message rate per partition](#ibm_eventstreams_instance_message_rate_per_partition) |  ![Checkmark icon](../icons/checkmark-icon.svg)  | | |
{: caption="Table 5. Metrics available for partitions" caption-side="bottom"}

## Metrics available with quotas enabled
{: #metrics-quotas}

| Metric name |Enterprise|Lite|Standard|
|-----------|--------|--------|--------|
| [IAM ID bytes in quota used percentage](#ibm_eventstreams_iam_id_bytes_in_quota_used_percentage) |  ![Checkmark icon](../icons/checkmark-icon.svg)  |   |  |
| [IAM ID bytes out quota used percentage](#ibm_eventstreams_iam_id_bytes_out_quota_used_percentage) |  ![Checkmark icon](../icons/checkmark-icon.svg)  |   |  |
{: caption="Table 6. Metrics available for quotas" caption-side="bottom"}

Kafka quotas use sampling to determine how long clients should be paused before they can send or receive more data. For unpredictable workloads, or configurations that result in quota decisions being made using only a few samples, you might observe the percentage quota used metric going above 100%.

### Authentication failures
{: #ibm_eventstreams_kafka_authentication_failure_total}

Incrementing count of the number of authentication failures

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_kafka_authentication_failure_total`|
| `Metric Type` | `counter` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 7. Authentication failures metric metadata" caption-side="bottom"}

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
{: caption="Table 8. Consume message conversion time metric metadata" caption-side="bottom"}

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
{: caption="Table 9. Estimated connected clients percentage metric metadata" caption-side="bottom"}

This is for information to help you monitor trends in your usage. See [Choosing your plan](/docs/EventStreams?topic=EventStreams-plan_choose) to determine what the recommended limits are for your plan and cluster.

### Connected clients software name and version
{: #ibm_eventstreams_connected_clients_software_name_and_version}

The number of connected clients with a particular client software name and version.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_connected_clients_software_name_and_version`|
| `Metric Type` | `gauge` |
| `Value Type`  | `number` |
| `Segment By` | `Client software name, Client software version` |
{: caption="Table 10. Connected clients software name and version metric metadata" caption-side="bottom"}

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
{: caption="Table 11. Inactive consumer groups metric metadata" caption-side="bottom"}

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
{: caption="Table 12. Instance bytes in per second metric metadata" caption-side="bottom"}

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
{: caption="Table 13. Instance bytes out per second metric metadata" caption-side="bottom"}

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
{: caption="Table 14. Missing SNI connections metric metadata" caption-side="bottom"}

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
{: caption="Table 15. Number of offline partitions metric metadata" caption-side="bottom"}

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
{: caption="Table 16. Number of partitions metric metadata" caption-side="bottom"}

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
{: caption="Table 17. Number of topics metric metadata" caption-side="bottom"}

### Number of under in-sync replica partitions
{: #ibm_eventstreams_kafka_under_minisr_partitions}

The number of partitions with fewer than two in-sync replicas.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_kafka_under_minisr_partitions`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance` |
{: caption="Table 18. Number of under in-sync replica partitions metric metadata" caption-side="bottom"}

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
{: caption="Table 19. Produce message conversion time metric metadata" caption-side="bottom"}

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
{: caption="Table 20. Rebalancing consumer groups metric metadata" caption-side="top"}

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
{: caption="Table 21. Reserved disk space percentage metric metadata" caption-side="bottom"}

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
{: caption="Table 22. Schema greatest version percentage metric metadata" caption-side="bottom"}

### Schema used percentage
{: #ibm_eventstreams_instance_schema_registry_schemas_used_percentage}

The percentage of schema capacity used in the schema registry.

| Metadata | Description |
|-------------|-------------------------------------------------------------------|
| `Metric Name` | `ibm_eventstreams_instance_schema_registry_schemas_used_percentage`|
| `Metric Type` | `gauge` |
| `Value Type`  | `percent` |
| `Segment By`  | `Service instance, Service instance name` |
{: caption="Table 23. Schema used percentage metric metadata" caption-side="bottom"}

### Stable consumer groups
{: #ibm_eventstreams_instance_stable_consumergroups}

The number of stable consumer groups in an {{site.data.keyword.messagehub}} instance.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_stable_consumergroups`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 24. Stable consumer groups metric metadata" caption-side="bottom"}

Use along with rebalancing consumer groups. If this is consistently zero and rebalancing high, then it indicates a cluster problem. If this is nonzero and rebalancing high, it indicates a consumer group issue.

### Topic bytes in per second
{: #ibm_eventstreams_instance_topic_bytes_in_per_second}

The number of bytes produced per second to a topic.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_topic_bytes_in_per_second`|
| `Metric Type` | `gauge` |
| `Value Type`  | `byte` |
| `Segment By` | `Service instance, IBM {{site.data.keyword.messagehub}} Kafka topic, Service instance name` |
{: caption="Table 25. Topic bytes in per second metric metadata" caption-side="bottom"}

This is for information to help you monitor trends in your usage, particularly if any topics are producing unusual throughput, which is more or less than expected.

### Topic bytes out per second
{: #ibm_eventstreams_instance_topic_bytes_out_per_second}

The number of bytes consumed per second from a topic.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_topic_bytes_out_per_second`|
| `Metric Type` | `gauge` |
| `Value Type`  | `byte` |
| `Segment By` | `Service instance, IBM {{site.data.keyword.messagehub}} Kafka topic, Service instance name` |
{: caption="Table 26. Topic bytes out per second metric metadata" caption-side="bottom"}

This is for information to help you monitor trends in your usage, particularly if any topics are consuming unusually more or less throughput than expected.

### IAM ID bytes in per second
{: #ibm_eventstreams_iam_id_bytes_in_per_second}

The number of bytes in per second per IAM ID.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_iam_id_bytes_in_per_second`|
| `Metric Type` | `gauge` |
| `Value Type`  | `byte` |
| `Segment By` | `Service instance, Service instance name, Iam Id` |
{: caption="Table 27. The number of bytes in per second per IAM ID" caption-side="bottom"}

This is for information to help you monitor trends in your usage, particularly if any IAM IDs are producing unusually more throughput than expected.

### IAM ID bytes out per second
{: #ibm_eventstreams_iam_id_bytes_out_per_second}

The number of bytes out per second per IAM ID.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_iam_id_bytes_out_per_second`|
| `Metric Type` | `gauge` |
| `Value Type`  | `byte` |
| `Segment By` | `Service instance, Service instance name, Iam Id` |
{: caption="Table 28. The number of bytes out per second per IAM ID" caption-side="bottom"}

This is for information to help you monitor trends in your usage, particularly if any IAM IDs are consuming unusually more throughput than expected.

### IAM ID bytes in quota used percentage
{: #ibm_eventstreams_iam_id_bytes_in_quota_used_percentage}

The percentage of bytes in quota used per IAM ID.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_iam_id_bytes_in_quota_used_percentage`|
| `Metric Type` | `gauge` |
| `Value Type`  | `percent` |
| `Segment By` | `Service instance, Service instance name, Iam Id` |
{: caption="Table 29. The percentage of bytes in quota used per IAM ID" caption-side="bottom"}

This is for information to help you monitor trends in your usage, particularly if any IAM IDs are producing close to their quota limits. 

### IAM ID bytes out quota used percentage
{: #ibm_eventstreams_iam_id_bytes_out_quota_used_percentage}

The percentage of bytes out quota used per IAM ID.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_iam_id_bytes_out_quota_used_percentage`|
| `Metric Type` | `gauge` |
| `Value Type`  | `percent` |
| `Segment By` | `Service instance, Service instance name, Iam Id` |
{: caption="Table 30. The percentage of bytes out quota used per IAM ID" caption-side="bottom"}

This is for information to help you monitor trends in your usage, particularly if any IAM IDs are consuming close to their quota limits. 

### Used disk space percentage
{: #ibm_eventstreams_instance_utilised_disk_space_percent}

The percentage of currently used disk space.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_utilised_disk_space_percent`|
| `Metric Type` | `gauge` |
| `Value Type`  | `percent` |
| `Segment By` | `Service instance, Service instance name` |
{: caption="Table 31. Used disk space percentage metric metadata" caption-side="bottom"}

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
{: caption="Table 32: Rest-producer requests per second metric metadata" caption-side="top"}

This is for information to help you monitor usage of the REST Producer API, including use of schema encoders.

### Mirroring throughput
{: #ibm_eventstreams_instance_mirroring_throughput}

The bytes per second of mirroring throughput from the source {{site.data.keyword.messagehub}} instance.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_mirroring_throughput_bytes_per_second`|
| `Metric Type` | `gauge` |
| `Value Type`  | `bytes_per_second` |
| `Segment By` | `Service instance, IBM {{site.data.keyword.messagehub}} Kafka topic, Service instance name` |
{: caption="Table 33. Mirroring throughput" caption-side="bottom"}

This is useful to see whether mirroring is active and for capacity planning.

### Mirroring_latency
{: #ibm_eventstreams_instance_mirroring_latency}

The per-topic mirroring latency in seconds from the source {{site.data.keyword.messagehub}} instance.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_mirroring_latency_seconds`|
| `Metric Type` | `gauge` |
| `Value Type`  | `seconds` |
| `Segment By` | `Service instance, IBM {{site.data.keyword.messagehub}} Kafka topic, Service instance name` |
{: caption="Table 34. Mirroring latency" caption-side="bottom"}

This is useful to determine how far behind a topic on the target cluster is.

### Consumer group lag 
{: #ibm_eventstreams_instance_consumer_groups_lag}

Lag for each consumer group for each topic-partition in an {{site.data.keyword.messagehub}} instance. This metric indicates that the number of messages that are yet to be processed for each partition in a consumer group. 

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_consumer_groups_lag`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance name, IBM {{site.data.keyword.messagehub}} consumer groups, IBM {{site.data.keyword.messagehub}} Kafka topic, IBM {{site.data.keyword.messagehub}} Kafka partitions` |
{: caption="Table 35. Consumer group lag metric metadata" caption-side="bottom"}

An increasing lag might highlight that the consumers in the group are not keeping pace with the rate that messages are being produced. This might require you to scale the number of consumers that process messages for the group.

It is normal for this metric to fluctuate when viewed over short time periods because of sampling and batch processing effects.
{: note}

### Message rate per partition 
{: #ibm_eventstreams_instance_message_rate_per_partition}

The rate of change of this metric gives the message per seccond that is incoming in to a partition of a {{site.data.keyword.messagehub}} instance topic.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_message_rate_per_partition`|
| `Metric Type` | `gauge` |
| `Value Type`  | `none` |
| `Segment By` | `Service instance name, IBM {{site.data.keyword.messagehub}} Kafka topic, IBM {{site.data.keyword.messagehub}} Kafka partitions` |
{: caption="Table 36. Message rate per partition metric metadata" caption-side="bottom"}

### Maximum partition retention percentage
{: #ibm_eventstreams_instance_max_partition_retention_percent}

Maximum percentage of the retention size used for partitions of a topic.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_max_partition_retention_percent`|
| `Metric Type` | `gauge` |
| `Value Type`  | `percent` |
| `Segment By` | `Service instance, IBM {{site.data.keyword.messagehub}} Kafka topic, Service instance name` |
{: caption="Table 37. Maximum partition retention percentage metric metadata" caption-side="bottom"}

### Topic size
{: #ibm_eventstreams_instance_topic_size}

Total disk size of all partitions of a topic.

| Metadata | Description |
|----------|-------------|
| `Metric Name` | `ibm_eventstreams_instance_topic_size`|
| `Metric Type` | `gauge` |
| `Value Type`  | `byte` |
| `Segment By` | `Service instance, IBM {{site.data.keyword.messagehub}} Kafka topic, Service instance name` |
{: caption="Table 38. Topic size metric metadata" caption-side="bottom"}

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
{: caption="Table 39. Global attributes" caption-side="bottom"}

### More attributes
{: #additional-attributes}

The following attributes are available for segmenting one or more attributes. See the individual metrics for segmentation options.

| Attribute | Attribute name | Attribute description |
|-----------|----------------|-----------------------|
| `Client software name` | `ibm_eventstreams_clientsoftwarename` | Client software name. |
| `Client software version` | `ibm_eventstreams_clientsoftwareversion` | Client software version. |
| `IBM {{site.data.keyword.messagehub}} Consumer Group` | `ibm_eventstreams_consumergroup` | IBM {{site.data.keyword.messagehub}} consumer group. |
| `IBM {{site.data.keyword.messagehub}} Kafka partition` | `ibm_eventstreams_partition` | IBM {{site.data.keyword.messagehub}} Kafka partition. |
| `IBM {{site.data.keyword.messagehub}} Kafka topic` | `ibm_eventstreams_topic` | IBM {{site.data.keyword.messagehub}} Kafka topic. |
| `Quantile` | `ibm_quantile` | The quantile represented when a metric supports segmenting by quantile. |
| `Service instance` | `ibm_service_instance` | The service instance segment identifies the instance that the metric is associated with. |
| `Service instance name` | `ibm_service_instance_name` | The service instance name provides the user-provided name of the service instance, which isn't necessarily a unique value that depends on the name that is provided by the user. |
{: caption="Table 40. More attributes" caption-side="bottom"}

For more information about enabling platform metrics from the {{site.data.keyword.messagehub}} dashboard and viewing metrics, see [Monitoring {{site.data.keyword.messagehub}} metrics](/docs/monitoring?topic=monitoring-monitoring){: external}.
