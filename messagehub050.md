---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-23"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Using the Kafka API
{: #kafka_using}

If you're using the Java clients, you can use the publicly available Kafka clients at 0.10.x or later. 

Kafka clients exist in multiple languages and we provide instructions for some of those languages. You can use others but you'll need SASL PLAIN support to provide credentials. Additionally, if you're using the Enterprise plan, you'll also need to use the Service Name Identifaction (SNI) extension to the TLSv1.2 protocol.

<table>
    <caption>Table 1. Kafka client support in Standard and Enterprise plans</caption>
      <tr>
	        <th></th>
		    <th>Standard Plan</th>
		    <th>Enterprise Plan</th>
        </tr>
	  		<tr>
			<td>**Kafka version on cluster**</td>
			<td>Kafka 0.10.2</td>
			<td>Kafka 1.1</td>
		</tr>
	  		<tr>
			<td>**Supported client versions**</td>
			<td>Kafka 0.10.x, or later</td>
			<td>Kafka 0.10.x, or later</td>
		</tr>
		<tr>
			<td>**Kafka Connect, Kafka Streams, and KSQL supported? **</td>
			<td>Yes</td>
			<td>Yes</td>
		</tr>

			<td>**Authentication requirements**</td>
			<td>Client must support authentication using the SASL Plain mechanism</td>
			<td>Client must support authentication using the SASL Plain mechanism and use the Service Name Identifaction (SNI) extension to the TLSv1.2 protocol</td>
		</tr>

</table>


