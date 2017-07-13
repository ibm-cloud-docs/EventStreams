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
{:table: .aria-labeledby="caption"}

# Exchanging messages between the MQ Light API and the Kafka or Kafka REST APIs
{: #mql_exchange}

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


