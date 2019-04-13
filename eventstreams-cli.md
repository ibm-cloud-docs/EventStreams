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
    <dt><code>--broker value, -b value</code></dt>
        <dd>Broker ID, with or without a preceding '--broker' flag.</dd>
    <dt><code>--json (optional)</code></dt>
        <dd>Output format in JSON.</dd>
</dl>

<strong>Examples</strong>:


## bmcloud es broker-config
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
    <dt><code>--broker value, -b value</code></dt>
        <dd>Broker ID, with or without a preceding '--broker' flag.</dd>
    <dt><code>--filter value, -f value (optional)</code></dt>
        <dd> Filter the list of configuration using wildcards (*) or a regular expression with forward slash (/) delimiters.</dd>
        <dt><code>--verbose, -v  (optional)</code></dt>
        <dd>Display verbose configuration information.</dd>
        <dt><code>--filter value, -f value(optional)</code></dt>
    <dt><code>--json (optional)</code></dt>
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
    <dt><code>--json (optional)</code></dt>
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
    <dt><code>--name value, -n value</code></dt>
        <dd>Topic name.</dd>
    <dt><code>--json (optional)</code></dt>
        <dd>Output format in JSON.</dd>
</dl>

<strong>Examples</strong>:


-------------

 
* **Duplicates**:<br/>
Enabling retries might result in duplicate messages. Depending on when a connection is lost, the producer might not be able to determine if a message was successfully processed by the server and therefore must send it again when reconnected. You are recommended to architect applications to expect duplicate messages. If duplicates cannot be tolerated, you can use the idempotent producer feature (from Kafka 1.1) to prevent duplicates during retries. For more information, see the [ 'enable.idempotency' property for producers ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://kafka.apache.org/11/documentation.html#topicconfigs){:new_window}.

.



