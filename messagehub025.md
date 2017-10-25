---

copyright:
  years: 2015, 2017
lastupdated: "2016-11-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Using the Kafka REST API
{: #rest_using}

The Kafka REST API provides a RESTful interface to a Kafka
cluster. You can easily produce and consume messages and complete administration tasks by using the
API. For reference documents, see [Confluent Platform docs ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://docs.confluent.io/2.0.0/){:new_window}. Only the binary embedded format is supported for requests and responses. The Avro and JSON embedded formats are not supported.

If you are using CURL, you can adapt the code
examples detailed in the [Confluent docs ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://docs.confluent.io/2.0.0/){:new_window} by adding the following line to the command line:
<pre class="pre">-H "X-Auth-Token: <var class="keyword varname">APIKEY</var>"</pre>
{: codeblock}

For example, for CURL, use the following to produce:

<pre class="pre">
curl -X POST -H "X-Auth-Token:<var class="keyword varname">APIKEY</var>" -H "Content-Type: application/vnd.kafka.binary.v1+json" <var class="keyword varname">kafka-rest endpoint</var>/topics/<var class="keyword varname">topic name</var> -d 

'
{
  "records": [
    {
      "value": "<var class="keyword varname">A base 64 encoded value string</var>"
    }
  ]
}
'
</pre>
{: codeblock}

For example, for CURL, use the following to consume:
<pre class="pre"><code>
curl -X GET -H "X-Auth-Token:<var class="keyword varname">APIKEY</var>" -H "Accept: application/vnd.kafka.binary.v1+json" <<var class="keyword varname">kafka-rest endpoint</var>/topic/<var class="keyword varname">topic name</var>/partitions/<var class="keyword varname">number of partition</var>/messages?offset=<var class="keyword varname">offset to start from</var>
</code></pre>
{: codeblock}

### Non-secure event POST request
<pre class="pre"><code class="hljs">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/application/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

<!-- Comment from Andrew
basic introduction, definitely including health warning
-->

