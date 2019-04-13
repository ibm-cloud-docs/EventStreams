---

copyright:
  years: 2015, 2019
lastupdated: "2019-04-13"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.messagehub}} CLI reference for the Standard+ and Enterprise plans
{: #cli_reference}

## ibmcloud es init
{: #ibmcloud es init}

Initialize the {{site.data.keyword.messagehub}} plugin.
```
ibmcloud es init [-i|--instance-name INSTANCE_NAME] [-a|--api-url API_ENDPOINT_URL]
```

<strong>Prerequisites</strong>: None

<strong>Command options</strong>:
   <dl>
   <dt>--instance-name value, -i value (optional)</dt>
   <dd>Name of the {{site.data.keyword.messagehub}} instance.</dd>
   <dt>--api-url value, -a value (optional)</dt>
   <dd>Kafka admin URL of {{site.data.keyword.messagehub}} instance.</dd>
   </dl>

<strong>Examples</strong>:


## ibmcloud es broker
{: #ibmcloud es broker}

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
        <dd>Broker ID, with or without a preceding '--broker' flag.</dd>
    <dt>--json (optional)</dt>
        <dd>Output format in JSON.</dd>
</dl>

<strong>Examples</strong>:


## ibmcloud es broker-config
{: #ibmcloud es broker config}

Display broker configuration.

```
ibmcloud es broker-config [--broker] ID [--filter FILTER] [--verbose] [--json]
```
{:codeblock}

<strong>Prerequisites</strong>: None

<strong>Command options</strong>:
{: #broker config params}

<dl>
    <dt>--broker value, -b value</dt>
        <dd>Broker ID, with or without a preceding '--broker' flag.</dd>
    <dt>--filter value, -f value (optional)</dt>
        <dd> Filter the list of configuration using wildcards (*) or a regular expression with forward slash (/) delimiters.</dd>
        <dt>--verbose, -v  (optional)</dt>
        <dd>Display verbose configuration information.</dd>
        <dt>--filter value, -f value(optional)</dt>
    <dt>--json (optional)</dt>
        <dd>Output format in JSON.</dd>
</dl>

<strong>Examples</strong>:


## ibmcloud es cluster
{: #ibmcloud es cluster}

Display the details of the cluster

```
ibmcloud es cluster [--json]
```
{:codeblock}

<strong>Prerequisites</strong>: None

<strong>Command options</strong>:
{: #es cluster params}

<dl>
    <dt>--json (optional)</dt>
        <dd>Output format in JSON.</dd>
</dl>

<strong>Examples</strong>:

## ibmcloud es topic
{: #ibmcloud es topic}

Display the details of a topic.

```
ibmcloud es topic [--name] TOPIC_NAME [--json]
```
{:codeblock}

<strong>Prerequisites</strong>: None

<strong>Command options</strong>:
{: #es topic params}

<dl>
    <dt>--name value, -n value</dt>
        <dd>Topic name.</dd>
    <dt>--json (optional)</dt>
        <dd>Output format in JSON.</dd>
</dl>

<strong>Examples</strong>:

## ibmcloud es topic-create
{: #ibmcloud es topic-create}

Create a new topic.

```
ibmcloud es topic-create [--name] TOPIC_NAME [--partitions PARTITIONS] [--config KEY=VALUE[;KEY=VALUE]* ]*
```
{:codeblock}

<strong>Prerequisites</strong>: None

<strong>Command options</strong>:
{: #es topic-create params}

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

<strong>Examples</strong>:

## ibmcloud es topic-delete
{: #ibmcloud es topic-delete}

Display the details of a topic.

```
ibmcloud es topic-delete [--name] TOPIC_NAME [--force]
```
{:codeblock}

<strong>Prerequisites</strong>: None

<strong>Command options</strong>:
{: #es topic-delete params}

<dl>
    <dt>--name value, -n value</dt>
        <dd>Topic name.</dd>
    <dt>--force, -f (optional)</dt>
        <dd>Delete without confirmation.</dd>
</dl>

<strong>Examples</strong>:

## ibmcloud es topic-delete-records
{: #ibmcloud es topic-delete-records}

Delete records from a topic for a given offset.

```
ibmcloud es topic-delete-records [--name] TOPIC_NAME [--partition-offset PARTITION:OFFSET[;PARTITION:OFFSET]* ]* [--force]

```
{:codeblock}

<strong>Prerequisites</strong>: None

<strong>Command options</strong>:
{: #es topic-create params}

<dl>
    <dt>--name value, -n value</dt>
        <dd>Topic name.</dd>
    <dt>--partition-offset PARTITION:OFFSET, -p PARTITION:OFFSET</dt>
        <dd>The partition and offset to delete records from in PARTITION:OFFSET format. <p> You can specify multiple --partition-offset options or you can specify
multiple PARTITION:OFFSET pairs with semicolon delimiters and surrounded with quotations: 'PARTITION1:OFFSET1;PARTITION2:OFFSET2;PARTITION3:OFFSET3'.</dd>
     <dt>--force, -f (optional)</dt>
        <dd>Delete records without confirmation.</dd>
</dl>

<strong>Examples</strong>:

-------------

 
* **Duplicates**:<br/>
Enabling retries might result in duplicate messages. Depending on when a connection is lost, the producer might not be able to determine if a message was successfully processed by the server and therefore must send it again when reconnected. You are recommended to architect applications to expect duplicate messages. If duplicates cannot be tolerated, you can use the idempotent producer feature (from Kafka 1.1) to prevent duplicates during retries. For more information, see the [ 'enable.idempotency' property for producers ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://kafka.apache.org/11/documentation.html#topicconfigs){:new_window}.

.



