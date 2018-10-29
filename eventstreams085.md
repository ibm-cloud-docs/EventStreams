---

copyright:
  years: 2015, 2018
lastupdated: "2018-10-29"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Choosing your plan 
{: #plan_choose}

{{site.data.keyword.messagehub}} is available as two different plans depending on your requirements: Standard and Enterprise.

## Standard plan

The Standard plan is appropriate if you require event ingest and distribution capabilities but do not require any additional benefits of the Enterprise plan. The Standard plan offers shared access to a multi-tenant {{site.data.keyword.messagehub}} cluster.

## Enterprise plan 

The Enterprise plan is appropriate if data isolation, guaranteed performance, and increased retention are important considerations. The Enterprise plan offers exclusive access to a dedicated {{site.data.keyword.messagehub}} cluster.

## What's supported by the Standard and Enterprise plans

The following table summarizes what is supported by the plans:

<table>
    <caption>Table 1. Support in Standard and Enterprise plans</caption>
      <tr>
	        <th></th>
		    <th>Standard Plan</th>
		    <th>Enterprise Plan</th>
        </tr>
		<tr>
			<td>**Tenancy**</td>
			<td>Multi-tenant </td>
			<td>Single tenant</td>
		</tr>
        <tr>
			<td>**Availability zones**</td>
			<td>Not supported</td>
			<td>3</td>
		</tr>
	  		<tr>
			<td>**Kafka version on cluster**</td>
			<td>Kafka 0.10.2</td>
			<td>Kafka 1.1</td>
		</tr>
		<tr>
			<td>**Fine-grained access control**</td>
			<td>No</td>
			<td>Yes</td>
		</tr>
		<tr>
			<td>**Kafka Connect and Kafka Streams supported **</td>
			<td>Yes</td>
			<td>Yes</td>
		</tr>
		<tr>
			<td>**Maximum number of partitions**</td>
			<td>100</td>
			<td>1000</td>
		</tr>
		<tr>
			<td>**Maximum retention period**</td>
			<td>1 GB per partition for up to 30 days </td>
			<td>Unlimited up to the storage limit of your plan </td>
		</tr>
		<tr>
			<td>**Region availability**</td>
			<td>US South (Dallas)</br>
			UK South (London)</br>
			AP South (Sydney)</br>
			EU Central (Frankfurt) - no {{site.data.keyword.mql}} API </td>
			<td>US South (Dallas)</br>
			US East (Washington)<br/>
			EU Central (Frankfurt)<br/>
			AP North (Tokyo)<br/>
			<br/>
			</td>
		</tr>
		<tr>
     	    <td>**APIs supported**</td>
			<td>Kafka API</br>
			Admin REST API<br/>
			Kafka REST API</br>
			MQ Light API</br>
		    </td>
			<td>Kafka API<br/>
			Admin REST API</td>
		</tr>
			<td>**Cloud Object Storage bridge and<br/>
			MQ bridge supported**</td>
			<td>Yes</td>
			<td>No</td>
		</tr>
		<tr>
			<td>**Deployment timeframe**</td>
			<td>Instantaneous provisioning</td>
			<td>Expect provisioning to take up to 3 hours</td>
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

