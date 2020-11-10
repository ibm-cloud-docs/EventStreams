---

copyright:
  years: 2015, 2019
lastupdated: "2019-10-09"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: EventStreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.messagehub}} CLI reference 
{: #cli_reference}

If you want information about how to install the CLI for {{site.data.keyword.messagehub}}, see 
[Getting started with the {{site.data.keyword.messagehub}} CLI ](/docs/EventStreams?topic=EventStreams-cli#cli).

## Changelog
{: #es_cli_changelog}

<table summary="Overview of version changes for the {{site.data.keyword.messagehub}} CLI plug-in">
<caption>Changelog for the {{site.data.keyword.messagehub}} CLI plug-in</caption>
<thead>
<tr>
<th>Version</th>
<th>Release date</th>
<th>Changes</th>
</tr>
</thead>
<tbody>
<tr>
<td>v1.0</td>
<td>May 12 2019</td>
<td>
Initial release of the {{site.data.keyword.messagehub}} CLI</td>
</tr>
<tr>
<td>v1.0.1</td>
<td>May 27 2019</td>
<td>
<ul>
<li>Improved error message when running command without init</li>
<li>Sorted instances list during init</li>
<li>Translation update</li>
</ul>
</td>
</tr>
<tr>
<td>v2.0</td>
<td>August 21 2019</td>
<td>
<ul>
<li>init: removed the service-key requirement</li>
<li>Added group-delete command</li>
<li>Updated translations of help text</li>
</ul></td>
</tr>
<tr>
<td>v2.1</td>
<td>June 24 2020</td>
<td>
<ul>
<li>init: displayed provision parameters for Enterprise instance</li>
<li>Translation update</li>
</ul></td>
</tr>
<tr>
<td>v2.1.1</td>
<td>July 10 2020</td>
<td>
<ul>
<li>Replaced whitelist with allowlist</li>
<li>Fixed color configuration</li>
<li>Translation update</li>
</ul></td>
</tr>
<tr>
<td>v2.2.0</td>
<td>August 3 2020</td>
<td>
<ul>
<li>Added support for the Mirroring feature</li>
</ul></td>
</tr>
<tr>
<td>v2.2.1</td>
<td>August 7 2020</td>
<td>
<ul>
<li>Refined the display of IP allowlist in init command</li>
</ul></td>
</tr>
<tr>
<td>v2.3</td>
<td>November 9 2020</td>
<td>
<ul>
<li>Added support for configuring message audit on topic</li>
<li>init: display encryption key if parameter kms_key_crn is specified in provisioning</li>
</ul></td>
</tr>
</tbody>
</table>



## ibmcloud es init
{: #ibmcloud_es_init}

Initialize the {{site.data.keyword.messagehub}} plugin.
```
ibmcloud es init [-i|--instance-name INSTANCE_NAME] [-a|--api-url API_ENDPOINT_URL]
```
{:codeblock}

<strong>Prerequisites</strong>: None

<strong>Command options</strong>:
   <dl>
   <dt>--instance-name value, -i value (optional)</dt>
   <dd>Name of the {{site.data.keyword.messagehub}} instance.</dd>
   <dt>--api-url value, -a value (optional)</dt>
   <dd>Kafka admin URL of the {{site.data.keyword.messagehub}} instance.</dd>
   </dl>

<!--
<strong>Examples</strong>:
-->

<br/>
## ibmcloud es broker
{: #ibmcloud_es_broker}

Display the details of a broker.

```
ibmcloud es broker [--broker] ID [--json]
```
{:codeblock}

<strong>Prerequisites</strong>: None

<strong>Command options</strong>:
{: #broker-req-params}

<dl>
    <dt>--broker value, -b value</dt>
        <dd>Broker ID, you can specify with or without a preceding '--broker' flag.</dd>
    <dt>--json (optional)</dt>
        <dd>Output format in JSON.</dd>
</dl>

<!--
<strong>Examples</strong>:
-->

<br/>
## ibmcloud es broker-config
{: #ibmcloud_es_broker_config}

Display the configuration of a broker.

```
ibmcloud es broker-config [--broker] ID [--filter FILTER] [--verbose] [--json]
```
{:codeblock}

<strong>Prerequisites</strong>: None

<strong>Command options</strong>:
{: #broker_config_params}

<dl>
    <dt>--broker value, -b value</dt>
        <dd>Broker ID, you can specify with or without a preceding '--broker' flag.</dd>
    <dt>--filter value, -f value (optional)</dt>
        <dd> Filter the list of configuration using wildcards (*) or a regular expression with forward slash (/) delimiters.</dd>
        <dt>--verbose, -v  (optional)</dt>
        <dd>Display verbose configuration information.</dd>
        <dt>--filter value, -f value(optional)</dt>
    <dt>--json (optional)</dt>
        <dd>Output format in JSON.</dd>
</dl>

<!--
<strong>Examples</strong>:
-->

<br/>
## ibmcloud es cluster
{: #ibmcloud_es_cluster}

Display the details of the cluster

```
ibmcloud es cluster [--json]
```
{:codeblock}

<strong>Prerequisites</strong>: None

<strong>Command options</strong>:
{: #es_cluster_params}

<dl>
    <dt>--json (optional)</dt>
        <dd>Output format in JSON.</dd>
</dl>

<!--
<strong>Examples</strong>:
-->
<br/>

## ibmcloud es topic
{: #ibmcloud_es_topic}

Display the details of a topic.

```
ibmcloud es topic [--name] TOPIC_NAME [--json]
```
{:codeblock}

<strong>Prerequisites</strong>: None

<strong>Command options</strong>:
{: #es_topic_params}

<dl>
    <dt>--name value, -n value</dt>
        <dd>Topic name.</dd>
    <dt>--json (optional)</dt>
        <dd>Output format of JSON.</dd>
</dl>

<!--
<strong>Examples</strong>:
-->
<br/>

## ibmcloud es topic-create
{: #ibmcloud_es _topic-create}

Create a new topic.

```
ibmcloud es topic-create [--name] TOPIC_NAME [--partitions PARTITIONS] [--config KEY=VALUE[;KEY=VALUE]* ]*
```
{:codeblock}

<strong>Prerequisites</strong>: None

<strong>Command options</strong>:
{: #es_topic_create_params}

<dl>
    <dt>--name value, -n value</dt>
        <dd>Topic name.</dd>
    <dt>--partitions value, -p value</dt>
        <dd>Set the number of partitions for the topic.</dd>
    <dt>--config KEY=VALUE, -c KEY=VALUE(optional)</dt>
        <dd>Set a configuration option for the topic as a KEY=VALUE pair.<p> You can specify multiple --config options.
Each '--config' option can specify a semicolon-delimited list of assignments.
The following is a list of valid configuration keys:
cleanup.policy
retention.ms
retention.bytes
segment.bytes
segment.ms
segment.index.bytes</p></dd>
</dl>

<!--
<strong>Examples</strong>:
-->
<br/>

## ibmcloud es topic-delete
{: #ibmcloud_es_topic_delete}

Delete a topic.

```
ibmcloud es topic-delete [--name] TOPIC_NAME [--force]
```
{:codeblock}

<strong>Prerequisites</strong>: None

<strong>Command options</strong>:
{: #es_topic_delete_params}

<dl>
    <dt>--name value, -n value</dt>
        <dd>Topic name.</dd>
    <dt>--force, -f (optional)</dt>
        <dd>Delete without confirmation.</dd>
</dl>

<!--
<strong>Examples</strong>:
-->
<br/>

## ibmcloud es topic-delete-records
{: #ibmcloud_es_topic_delete_records}

Delete records from a topic for a given offset.

```
ibmcloud es topic-delete-records [--name] TOPIC_NAME [--partition-offset PARTITION:OFFSET[;PARTITION:OFFSET]* ]* [--force]

```
{:codeblock}

<strong>Prerequisites</strong>: None

<strong>Command options</strong>:
{: #es_topic_delete_records_params}

<dl>
    <dt>--name value, -n value</dt>
        <dd>Topic name.</dd>
    <dt>--partition-offset PARTITION:OFFSET, -p PARTITION:OFFSET</dt>
        <dd>The partition and offset to delete records from in PARTITION:OFFSET format. <p> You can specify multiple --partition-offset options or you can specify
multiple PARTITION:OFFSET pairs with semicolon delimiters and surrounded with quotations: 'PARTITION1:OFFSET1;PARTITION2:OFFSET2;PARTITION3:OFFSET3'.</dd>
     <dt>--force, -f (optional)</dt>
        <dd>Delete records without confirmation.</dd>
</dl>

<!--
<strong>Examples</strong>:
-->
<br/>

## ibmcloud es topic-partitions-set
{: #ibmcloud_es_topic_partitions_set}

Set the partitions for a topic.


```
ibmcloud es topic-partitions-set [--name] TOPIC_NAME --partitions PARTITIONS

```
{:codeblock}

<strong>Prerequisites</strong>: None

<strong>Command options</strong>:
{: #ibmcloud_es_topic_partitions_set_params}

<dl>
    <dt>--name value, -n value</dt>
        <dd>Topic name.</dd>
     <dt>--partitions value, -p value</dt>
        <dd>Set the number of partitions for the topic.
</dd>
</dl>

<br/>

## ibmcloud es topic-update
{: #ibmcloud_es_topic_update}

Update the configuration for a topic.


```
ibmcloud es topic-update [--name] TOPIC_NAME --config KEY[=VALUE][;KEY[=VALUE]]* [--default]

```
{:codeblock}

<strong>Prerequisites</strong>: None

<strong>Command options</strong>:
{: #ibmcloud_es_topic_update_params}

<dl>
    <dt>--name value, -n value</dt>
        <dd>Topic name.</dd>
     <dt>--config KEY[=VALUE], -c KEY[=VALUE] </dt>
        <dd>Set a configuration option for the topic as a KEY[=VALUE] pair.
        <p>If VALUE is not given, the '--default' flag should be specified to indicate resetting the configuration value back to the default.
Multiple --config options can be specified.
Each '--config' option can specify a semicolon-delimited list of assignments
The following is a list of valid configuration keys:
cleanup.policy
retention.ms
retention.bytes
segment.bytes
segment.ms
segment.index.bytes</p></dd>
    <dt>--default, -d  (optional)</dt>
        <dd>Reset each configuration parameter specified using '--config' to its default value.</dd>
</dl>

<!--
<strong>Examples</strong>:
-->
<br/>

## ibmcloud es topics
{: #ibmcloud_es_topics}

List topics.


```
ibmcloud es topics [--filter FILTER] [--json]

```
{:codeblock}

<strong>Prerequisites</strong>: None

<strong>Command options</strong>:
{: #ibmcloud_es_topics_params}

<dl>
    <dt>--filter value, -f value (optional)</dt>
        <dd>Topic name.</dd>
     <dt>--json (optional)</dt>
        <dd>Format output in JSON. Up to 1000 topics are returned.
</dd>
</dl>

<!--
<strong>Examples</strong>:
-->
<br/>

## ibmcloud es group
{: #ibmcloud_es_group}

Display details of a consumer group.


```
ibmcloud es group [--group] GROUP_ID [--json]

```
{:codeblock}

<strong>Prerequisites</strong>: None

<strong>Command options</strong>:
{: #ibmcloud_es_group_params}

<dl>
    <dt>--group value, -g value </dt>
        <dd>Consumer group ID</dd>
     <dt>--json (optional)</dt>
        <dd>Format output in JSON. 
</dd>
</dl>

<!--
<strong>Examples</strong>:
-->
<br/>

## ibmcloud es group-reset
{: #ibmcloud_es_group_reset}

Reset the offsets for a consumer group.


```
ibmcloud es group-reset [--group] GROUP_ID [--topic TOPIC_NAME] [--all-topics] --mode MODE --value VALUE [--dry-run] [--execute] [--json]


```
{:codeblock}

<strong>Prerequisites</strong>: None

<strong>Command options</strong>:
{: #ibmcloud_es_group_reset_params}

<dl>
    <dt>--group value, -g value </dt>
        <dd>Consumer group ID</dd>
     <dt>--topic value, -t value</dt>
        <dd>Topic name. Apply to just this topic. Omit if '--all-topics' flag has been supplied. 
</dd>
     <dt>--all-topics, -a   </dt>
        <dd>Apply to all topics assigned to the group. Omit if '--topic' flag has been supplied. 
</dd>
     <dt>--mode value, -m value</dt>
        <dd>One of the following: 'earliest', 'latest' or 'datetime'.
</dd>
     <dt>--value value, -v value</dt>
        <dd>Value for resetting offsets, based on '--mode'. Omit for 'earliest' and 'latest'.
'datetime': use 'YYYY-MM-DDTHH:mm:SS.sss[±hh:mm|Z]'.
</dd>
     <dt>--dry-run (optional)</dt>
        <dd>Show results and do not implement the changes.
</dd>
     <dt>--execute  (optional)</dt>
        <dd> Execute the changes to the offsets.
</dd>
     <dt>--json (optional)</dt>
        <dd> Format output in JSON. 
</dd>
</dl>

<!--
<strong>Examples</strong>:
-->
<br/>

## ibmcloud es groups
{: #ibmcloud_es_groups}

List consumer groups.


```
ibmcloud es groups [--filter FILTER] [--json]

```
{:codeblock}

<strong>Prerequisites</strong>: None

<strong>Command options</strong>:
{: #ibmcloud_es_groups_params}

<dl>
    <dt>--filter value, -f value (optional)
 </dt>
        <dd>Optional. Filter the list of consumer groups using wildcards (*) or a regular expression with forward slash (/) delimiters.</dd>
     <dt>--json (optional)</dt>
        <dd>Format output in JSON. A maximum of 1000 groups are returned.
</dd>
</dl>

## ibmcloud es group-delete
{: #ibmcloud_es_group_delete}

Delete a consumer group.


```
ibmcloud es group-delete [--group] GROUP_ID [--force]

```
{:codeblock}

<strong>Prerequisites</strong>: None

<strong>Command options</strong>:
{: #ibmcloud_es_group_delete_params}

<dl>
    <dt>--group value, -g value </dt>
        <dd>Consumer group ID</dd>
    <dt>--force, -f (optional)</dt>
        <dd>Delete group without confirmation.</dd> 
</dd>
</dl>

## ibmcloud es mirroring-topic-selection
{: #ibmcloud_es_mirroring_topic_selection}

List mirroring topic selection.


```
ibmcloud es mirroring-topic-selection [--json]

```
{:codeblock}

<strong>Prerequisites</strong>: Mirroring enabled on {{site.data.keyword.messagehub}} instance. es plugin configured to connect to the mirroring target cluster via `ibmcloud es init`.

<strong>Command options</strong>:
{: #ibmcloud_es_mirroring_topic_selection_params}

<dl>
    <dt>--json (optional)</dt>
        <dd>Format output in JSON.</dd>
</dl>

## ibmcloud es mirroring-topic-selection-set
{: #ibmcloud_es_mirroring_topic_selection_set}

Replace mirroring topic selection.

```
ibmcloud es mirroring-topic-selection-set (--select pattern1,pattern2 | --none) [--force]

```
{:codeblock}

<strong>Prerequisites</strong>: Mirroring enabled on {{site.data.keyword.messagehub}} instance. es plugin configured to connect to the mirroring target cluster via `ibmcloud es init`.

<strong>Command options</strong>:
{: #ibmcloud_es_mirroring_topic_selection_set_params}

<dl>
    <dt>--select value</dt>
        <dd>Selection of topics to mirror as comma separated regex patterns. Use '.*' to mirror all topics.</dt>
    <dt>--none</dt>
        <dd>Clear currently selected topics (disable mirroring of topics).</dd>
    <dt>--force</dt>
        <dd>Optional. Replace mirroring topic selection without confirmation.</dd>
</dl>

<!--
<strong>Examples</strong>:
-->
<br/>
 
 <br/>








