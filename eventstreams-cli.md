---

copyright:
  years: 2015, 2019
lastupdated: "2019-04-10"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.messagehub}} CLI reference for the Standard+ and Enterprise   m,//plans
{: #cli_reference}

## ibmcloud es init
{: #ibmcloud es init}

Initialize the {{site.data.keyword.messagehub}} plugin. {{site.data.keyword.cloud_notm}} API endpoint.
```
ibmcloud es init [-i|--instance-name INSTANCE_NAME] [-a|--api-url API_ENDPOINT_URL]
```

<strong>Prerequisites</strong>: None

<strong>Command options</strong>:
   <dl>
   <dt>API_ENDPOINT (optional)</dt>
   <dd>The API endpoint that is targeted, for example, `https://cloud.ibm.com`. If both *API_ENDPOINT* and `--unset` options aren't specified, the current API endpoint is displayed.</dd>
   <dt>--unset (optional)</dt>
   <dd>Remove the API endpoint setting.</dd>
   <dt>--skip-ssl-validation (optional)</dt>
   <dd>Bypass SSL validation of HTTP requests.</dd>
   </dl>

<strong>Examples</strong>:

Set the API endpoint to cloud.ibm.com:
```
ibmcloud api cloud.ibm.com
```
{: codeblock}

```
ibmcloud api https://cloud.ibm.com --skip-ssl-validation
```
{: codeblock}


View the current API endpoint:
```
ibmcloud api
```
{: codeblock}


Unset the API endpoint:
```
ibmcloud api --unset
```
{: codeblock}


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
    <dt><code>KEY_NAME</code></dt>
        <dd>A unique, human-readable alias to assign to your key.</dd>
    <dt><code>-i, --instance-ID | $INSTANCE_ID</code></dt>
        <dd>The {{site.data.keyword.cloud_notm}} instance ID that identifies your {{site.data.keyword.keymanagementserviceshort}} service instance.</dd>
</dl>

### Optional parameters
{: #create-opt-params}

<dl>
    <dt><code>-k, --key-material</code></dt>
        <dd>The base64 encoded key material that you want to store and manage in the service. To import an existing key, provide a 256-bit key. To generate a new key, omit the <code>--key-material</code> parameter.</dd>
    <dt><code>-s, --standard-key</code></dt>
        <dd>Set the parameter only if you want to create a <a href="/docs/services/key-protect?topic=key-protect-envelope-encryption#key-types">standard key</a>. To create a root key, omit the <code>--standard-key</code> parameter.</dd>
    <dt><code>-o, s--output</code></dt>
        <dd>Set the CLI output format. By default, all commands print in table format. To change the output format to JSON, use <code>--output json</code>.</dd>
</dl>



-------------
The {{site.data.keyword.messagehub}} service is provided with an availability of 99.95%. 
For further information about the SLA for {{site.data.keyword.Bluemix}}, see
[{{site.data.keyword.Bluemix_notm}} service description ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www-03.ibm.com/software/sla/sladb.nsf/pdf/6605-14/$file/i126-6605-14_08-2018_en_US.pdf){:new_window}.




* **Retries**:<br/>
Kafka clients provide re-connect logic, but you must explicitly enable reconnects for producers. For more information, see the [ 'retries' property for producers ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://kafka.apache.org/11/documentation.html#producerconfigs){:new_window}. Connections are remade within 60 seconds.   
 
* **Duplicates**:<br/>
Enabling retries might result in duplicate messages. Depending on when a connection is lost, the producer might not be able to determine if a message was successfully processed by the server and therefore must send it again when reconnected. You are recommended to architect applications to expect duplicate messages. If duplicates cannot be tolerated, you can use the idempotent producer feature (from Kafka 1.1) to prevent duplicates during retries. For more information, see the [ 'enable.idempotency' property for producers ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://kafka.apache.org/11/documentation.html#topicconfigs){:new_window}.

.



