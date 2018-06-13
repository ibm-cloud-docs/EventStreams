---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Choosing your plan 
{: #plan_choose}

{{site.data.keyword.messagehub}} is available as two different plans depending on your requirements: Enterprise and Standard.

## Enterprise plan

The Enterprise plan is appropriate if data isolation, predictable performance, and being a single tenant are important considerations. 

## Standard plan

The Standard plan is appropriate if you want an economical public cloud service where you pay for what you use and share infrastructure with others.

Depending on which plan you're using {{site.data.keyword.messagehub}} offers different APIs. On the Enterprise plan, you can use the Kafka API. On the Standard plan, you can choose from the Kafka API, the Kafka REST API, and the {{site.data.keyword.mql}} API. In most cases, the Kafka API is the best choice. For more information, see [Creating messaging applications](/docs/services/MessageHub/messagehub086.html).

## What's supported by the Enterprise and Standard plans

The following table summarizes what is supported by the plans:

<table>
    <caption>Table 1. Support in Enterprise and Standard plans</caption>
      <tr>
	        <th></th>
		    <th>Enterprise Plan</th>
		    <th>Standard Plan</th>
        </tr>
		<tr>
			<td>**Tenancy**</td>
			<td>Single tenant</td>
			<td>Multi-tenant</td>
		</tr>
        <tr>
			<td>**Availability zones**</td>
			<td>3</td>
			<td>Not supported</td>
		</tr>
	  		<tr>
			<td>**Kafka version on cluster**</td>
			<td>Kafka 1.1</td>
			<td>Kafka 0.10.2 </td>
		</tr>
		<tr>
			<td>**Fine-grained access control?**</td>
			<td>Yes</td>
			<td>No</td>
		</tr>
		<tr>
			<td>**Region availability**</td>
			<td>US South currently</br>
			Coming soon:</br>
			US East</br>
			United Kingdom</br>
			Germany</br>
			Sydney<br/>
			AP North
			</td>
			<td>US South</br>
			United Kingdom</br>
			Sydney</br>
			Germany (no MQ Light API)</td>
		</tr>
		<tr>
     	    <td>**APIs supported**</td>
			<td>Kafka API</td>
			<td>Kafka API</br>
			Kafka REST API</br>
			MQ Light API</br>
		    </td>
		</tr>
			<td>**Cloud Object Storage bridge and<br/>
			MQ bridge supported?**</td>
			<td>No</td>
			<td>Yes</td>
		</tr>
		<tr>
			<td></td>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<td></td>
			<td></td>
			<td></td>
		</tr>

</table>

<!--
## {{site.data.keyword.Bluemix_notm}} Public environment
{: notoc}

{{site.data.keyword.Bluemix_notm}} Public provides an
economical public cloud service where you pay for what you use and share infrastructure with
others.

In {{site.data.keyword.Bluemix_notm}} Public, the cost of
{{site.data.keyword.messagehub}} is determined by two factors: the
number of partitions that you use and the number of messages that you send and receive. There is no
charge for message data while it is retained on the topics, but the data that each partition retains
is capped at 1 GB.

For more information, see [{{site.data.keyword.Bluemix_notm}} Public ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud-computing/bluemix/public){:new_window}.
-->

