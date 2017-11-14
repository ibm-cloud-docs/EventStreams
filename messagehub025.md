---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-26"

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
API. For reference documents, see [Confluent Platform docs ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://docs.confluent.io/2.0.0/){:new_window}. Only the binary embedded format is supported for requests and responses in {{site.data.keyword.messagehub}}. The Avro and JSON embedded formats are not supported.

If you are using CURL, you can use an example like the following to produce:
<pre class="pre"><code>
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
</code></pre>
{: codeblock}

If you are using CURL, you can use an example like the following to consume:
<pre class="pre"><code>
curl -X GET -H "X-Auth-Token:<var class="keyword varname">APIKEY</var>" -H "Accept: application/vnd.kafka.binary.v1+json" <var class="keyword varname">kafka-rest endpoint</var>/topics/<var class="keyword varname">topic name</var>/partitions/<var class="keyword varname">partition ID</var>/messages?offset=<var class="keyword varname">offset to start from</var>
</code></pre>
{: codeblock}


For CURL, you can also adapt the code
examples detailed in the [Confluent docs ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://docs.confluent.io/2.0.0/){:new_window} by adding the following line to the command line:
<pre class="pre">-H "X-Auth-Token: <var class="keyword varname">APIKEY</var>"</pre>
{: codeblock}


<!-- Comment from Andrew
basic introduction, definitely including health warning
-->

