---

copyright:
  years: 2015, 2023
lastupdated: "2023-08-15"

keywords: cli reference

subcollection: EventStreams

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.messagehub}} CLI reference 
{: #cli_reference}

If you want information about how to install the CLI for {{site.data.keyword.messagehub}}, see [Getting started with the {{site.data.keyword.messagehub}} CLI](/docs/EventStreams?topic=EventStreams-cli#cli).
{: shortdesc}

## Changelog
{: #es_cli_changelog}

| Version | Release date  | Changes  |
|---|---|---|
| v1.0 |  12 May 2019 |  - Initial release of the {{site.data.keyword.messagehub}} CLI.  |
| v1.0.1  | 27 May 2019 |  - Improved error message when you run the command without init.  \n - Sorted instances list during init.  \n -  Translation update. |
|  v2.0  | 21 August 2019  |  - init: Removed the service-key requirement.  \n - Added group-delete command. Updated translations of help text. |
| v2.1 | 24 June 2020  |  - init: Displayed provision parameters for Enterprise instance. \n - Translation update. |
|  v2.1.1| 10 July 2020  |  - Replaced `whitelist` with ´allowlist`.  \n - Fixed color configuration.  \n - Translation update.  |
| v2.2.0  | 3 August 2020  |  - Added support for the Mirroring feature.  |
| v2.2.1 | 7 August 2020 |  - init: Refined the display of IP allowlist.   |
| v2.3 |  9 November 2020 |  - Added support for configuring message audit on topic. \n - init: Display encryption key if parameter kms_key_crn is specified in provisioning.  |
| v2.3.1 |  21 January 2021 |  - Added support for Satellite plan.  |
| v2.3.2 |  5 May 2022 |  - Added support for Mac OS X M1/ARM. \n - init: Display Object Storage bucket if parameter `cos_bucket_crn` is specified in provisioning. |
| v2.4.0 |  28 Feb 2023 |  - Added Kafka version to `ibmcloud es cluster`. \n - Updated Go to 1.9.6. |
{: caption="Table 1. Changelog for the {{site.data.keyword.messagehub}} CLI plug-in" caption-side="bottom"}

## ibmcloud es init
{: #ibmcloud_es_init}

Initialize the {{site.data.keyword.messagehub}} plug-in.

```bash
ibmcloud es init [-i|--instance-name INSTANCE_NAME] [-a|--api-url API_ENDPOINT_URL]
```
{: codeblock}

**Prerequisites**: None

**Command options**:

--instance-name value, -i value (optional)
:   Name of the {{site.data.keyword.messagehub}} instance.

--api-url value, -a value (optional)
:   Kafka admin URL of the {{site.data.keyword.messagehub}} instance.

## ibmcloud es broker
{: #ibmcloud_es_broker}

Display the details of a broker.

```bash
ibmcloud es broker [--broker] ID [--json]
```
{: codeblock}

**Prerequisites**: None

**Command options**:

--broker value, -b value
:   Broker ID, you can specify with or without a preceding '--broker' flag.
          
--json (optional)
:   Output format in JSON.
          
## ibmcloud es broker-config
{: #ibmcloud_es_broker_config}

Display the configuration of a broker.

```bash
ibmcloud es broker-config [--broker] ID [--filter FILTER] [--verbose] [--json]
```
{: codeblock}

**Prerequisites**: None

**Command options**:

--broker value, -b value
:   Broker ID, you can specify with or without a preceding '--broker' flag.

--filter value, -f value (optional)
:   Filter the list of configuration by using wildcards (*) or a regular expression with forward slash (/) delimiters.

--verbose, -v  (optional)
:   Display verbose configuration information.

--json (optional)
:   Output format in JSON.
          
## ibmcloud es cluster
{: #ibmcloud_es_cluster}

Display the details of the cluster, including the Kafka version.

```bash
ibmcloud es cluster [--json]
```
{: codeblock}

**Prerequisites**: None

**Command options**:

--json (optional)
:   Output format in JSON.

## ibmcloud es topic
{: #ibmcloud_es_topic}

Display the details of a topic.

```bash
ibmcloud es topic [--name] TOPIC_NAME [--json]
```
{: codeblock}

**Prerequisites**: None

**Command options**:

--name value, -n value
:   Topic name.

--json (optional)
:   Output format of JSON.

## ibmcloud es topic-create
{: #ibmcloud_es _topic-create}

Create a new topic.

```bash
ibmcloud es topic-create [--name] TOPIC_NAME [--partitions PARTITIONS] [--config KEY=VALUE[;KEY=VALUE]* ]*
```
{: codeblock}

**Prerequisites**: None

**Command options**:

--name value, -n value
:   Topic name.

--partitions value, -p value
:   Set the number of partitions for the topic.

--config KEY=VALUE, -c KEY=VALUE(optional)
:   Set a configuration option for the topic as a KEY=VALUE pair. 
:   You can specify multiple --config options. Each '--config' option can specify a semicolon-delimited list of assignments. The following list shows valid configuration keys:
  
    - cleanup.policy
    - retention.ms
    - retention.bytes
    - segment.bytes
    - segment.ms
    - segment.index.bytes

## ibmcloud es topic-delete
{: #ibmcloud_es_topic_delete}

Delete a topic.

```bash
ibmcloud es topic-delete [--name] TOPIC_NAME [--force]
```
{: codeblock}

**Prerequisites**: None

**Command options**:

--name value, -n value
:   Topic name.

--force, -f (optional)
:   Delete without confirmation.

## ibmcloud es topic-delete-records
{: #ibmcloud_es_topic_delete_records}

Delete records from a topic for a given offset.

```bash
ibmcloud es topic-delete-records [--name] TOPIC_NAME [--partition-offset PARTITION:OFFSET[;PARTITION:OFFSET]* ]* [--force]
```
{: codeblock}

**Prerequisites**: None

**Command options**:

--name value, -n value
:   Topic name.

--partition-offset PARTITION:OFFSET, -p PARTITION:OFFSET
:   The partition and offset to delete records from in PARTITION:OFFSET format. 
:   You can specify multiple --partition-offset options or you can specify multiple PARTITION:OFFSET pairs with semicolon delimiters and surrounded with quotations: 'PARTITION1:OFFSET1;PARTITION2:OFFSET2;PARTITION3:OFFSET3'.
  
--force, -f (optional)
:   Delete records without confirmation.

## ibmcloud es topic-partitions-set
{: #ibmcloud_es_topic_partitions_set}

Set the partitions for a topic.

```bash
ibmcloud es topic-partitions-set [--name] TOPIC_NAME --partitions PARTITIONS
```
{: codeblock}

**Prerequisites**: None

**Command options**:

--name value, -n value
:   Topic name.

--partitions value, -p value
:   Set the number of partitions for the topic.

## ibmcloud es topic-update
{: #ibmcloud_es_topic_update}

Update the configuration for a topic.

```bash
ibmcloud es topic-update [--name] TOPIC_NAME --config KEY[=VALUE][;KEY[=VALUE]]* [--default]
```
{: codeblock}

**Prerequisites**: None

**Command options**:

--name value, -n value
:   Topic name.

--config KEY[=VALUE], -c KEY[=VALUE]
:   Set a configuration option for the topic as a KEY[=VALUE] pair.
:   If VALUE is not given, the '--default' flag is to be specified to indicate resetting the configuration value back to the default. Multiple '--config' options can be specified. Each '--config' option can specify a semicolon-delimited list of assignments. The following list shows valid configuration keys:

    - cleanup.policy
    - retention.ms
    - retention.bytes
    - segment.bytes
    - segment.ms
    - segment.index.bytes

--default, -d  (optional)
:   Reset each configuration parameter that is specified by using '--config' to its default value.

## ibmcloud es topics
{: #ibmcloud_es_topics}

List topics.

```bash
ibmcloud es topics [--filter FILTER] [--json]
```
{: codeblock}

**Prerequisites**: None

**Command options**:

--filter value, -f value (optional)
:   Topic name.
  
--json (optional)
:   Format output in JSON. Up to 1000 topics are returned.

## ibmcloud es group
{: #ibmcloud_es_group}

Display details of a consumer group.

```bash
ibmcloud es group [--group] GROUP_ID [--json]
```
{: codeblock}

**>Prerequisites**: None

**Command options**:

--group value, -g value
:   Consumer group ID.
  
--json (optional)
:   Format output in JSON. 

## ibmcloud es group-reset
{: #ibmcloud_es_group_reset}

Reset the offsets for a consumer group.

```bash
ibmcloud es group-reset [--group] GROUP_ID [--topic TOPIC_NAME] [--all-topics] --mode MODE --value VALUE [--dry-run] [--execute] [--json]
```
{: codeblock}

**Prerequisites**: None

**Command options**:

--group value, -g value
:   Consumer group ID

--topic value, -t value
:   Topic name. Apply to just this topic. Omit if '--all-topics' flag was supplied. 

--all-topics, -a
:   Apply to all topics assigned to the group. Omit if '--topic' flag was supplied. 

--mode value, -m value
:   One of the following values: 'earliest', 'latest' or 'datetime'.

--value value, -v value
:   Value for resetting offsets, based on '--mode'. Omit for 'earliest' and 'latest'.
'datetime': use 'YYYY-MM-DDTHH:mm:SS.sss[±hh:mm|Z]'.

--dry-run (optional)
:   Show results and do not implement the changes.

--execute  (optional)
:   Execute the changes to the offsets.

--json (optional)
:   Format output in JSON. 

## ibmcloud es groups
{: #ibmcloud_es_groups}

List consumer groups.

```bash
ibmcloud es groups [--filter FILTER] [--json]
```
{: codeblock}

**Prerequisites**: None

**Command options**:
{: #ibmcloud_es_groups_params}

--filter value, -f value (optional)
:   Optional. Filter the list of consumer groups by using wildcards (*) or a regular expression with forward slash (/) delimiters.

--json (optional)
:   Format output in JSON. A maximum of 1000 groups are returned.

## ibmcloud es group-delete
{: #ibmcloud_es_group_delete}

Delete a consumer group.

```bash
ibmcloud es group-delete [--group] GROUP_ID [--force]
```
{: codeblock}

**Prerequisites**: None

**Command options**:

--group value, -g value
:   Consumer group ID

--force, -f (optional)
:   Delete group without confirmation.

## ibmcloud es mirroring-topic-selection
{: #ibmcloud_es_mirroring_topic_selection}

List mirroring topic selection.

```bash
ibmcloud es mirroring-topic-selection [--json]
```
{: codeblock}

**Prerequisites**: Mirroring enabled on {{site.data.keyword.messagehub}} instance. ES plug-in configured to connect to the mirroring target cluster through `ibmcloud es init`.

**Command options**:

--json (optional)
:   Format output in JSON.

## ibmcloud es mirroring-topic-selection-set
{: #ibmcloud_es_mirroring_topic_selection_set}

Replace mirroring topic selection.

```bash
ibmcloud es mirroring-topic-selection-set (--select pattern1,pattern2 | --none) [--force]
```
{: codeblock}

**Prerequisites**: Mirroring enabled on {{site.data.keyword.messagehub}} instance. ES plug-in configured to connect to the mirroring target cluster through `ibmcloud es init`.

**Command options**:

--select value
:   Selection of topics to mirror as comma-separated regex patterns. Use '.*' to mirror all topics.

--none
:   Clear currently selected topics (disable mirroring of topics).

--force
:   Optional. Replace mirroring topic selection without confirmation.
