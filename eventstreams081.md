---

copyright:
  years: 2015, 2019
lastupdated: "2018-05-25"

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

<!-- 15/11/18: info moved to eventstreams075.md, moved because of doc app changes -->

# Exchanging messages between the MQ Light API and the Kafka or Kafka REST APIs
{: #mql_exchange}

** The MQ Light API is available as part of the Standard plan only.**
<br/>

{{site.data.keyword.mql}} messages are stored in a single underlying Kafka topic named "MQLight" and are encoded as detailed in the following table. This encoding can also be used by other API types, such as Kafka or Kafka REST, to exchange messages with applications using the
{{site.data.keyword.mql}} API.

## Kafka message format
{: #kafka_format notoc}

<table border='1'>
<caption>Table 1. Kafka message format</caption>
  <tr>
    <th> Key </th>
    <th> Value </th>
  </tr>
  <tr>
    <td> Optional (not used by the API)
	<p></p>
	</td>
    <td>**1 byte**
	<p>		     MQ Light API eye catcher, which is always 0xFA.</p>
    <p><var class="keyword varname">**n**</var> **bytes**</p>
    <p>		    AMQP encoded message (formatted based on the AMQP wire format). </p></td>
  </tr>
</table>


