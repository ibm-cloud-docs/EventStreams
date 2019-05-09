---

copyright:
  years: 2015, 2019
lastupdated: "2019-05-09"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# The Classic plan 
{: #plan_choose_classic}

{{site.data.keyword.messagehub}} is available as different plans depending on your requirements. For information about the Standard and Enterprise plans, see [Choosing your plan](/docs/services/EventStreams?topic=eventstreams-plan_choose#plan_choose).
{: shortdesc}
 
## Classic plan overview
The Classic plan is appropriate if you require event ingest and distribution capabilities but do not require any additional benefits of the Enterprise plan. The Classic plan offers shared access to a multi-tenant {{site.data.keyword.messagehub}} cluster.


## What's supported by the Classic plan

The following table summarizes what is supported by the plan:

<table>
    <caption>Table 1. Support in Classic plan</caption>
      <tr>
	        <th></th>
		    <th>Classic Plan</th>
        </tr>
		<tr>
			<td>**Tenancy**</td>
			<td>Multi-tenant </td>
		</tr>
        <tr>
			<td>**Availability zones**</td>
			<td>Not supported</td>
		</tr>
        <tr>
			<td>**Availability**</td>
			<td>99.5%</td>
		</tr>
	  		<tr>
			<td>**Kafka version on cluster**</td>
			<td>Kafka 1.1</td>
		</tr>
		<tr>
			<td>**Fine-grained access control**</td>
			<td>No</td>
		</tr>
				<tr>
			<td>**Cloud Service Endpoint support**</td>
			<td>No</td>
		</tr>
		<tr>
			<td>**Kafka Connect and Kafka Streams supported **</td>
			<td>Yes</td>

		</tr>
		<tr>
			<td>**Maximum number of partitions**</td>
			<td>100</td>

		</tr>
		<tr>
			<td>**Maximum retention period**</td>
			<td>1 GB per partition for up to 30 days </td>

		</tr>
		<tr>
			<td>**Maximum throughput**</td>
			<td>1 MB per second per partition</td>
		</tr>
		<tr>
			<td>**Maximum message size**</td>
			<td>1 MB</td>
		</tr>
		<tr>
			<td>**Location (region) availability**</td>
			<td>Dallas (us-south)</br>
			London (eu-gb)</br>
			Sydney (au-syd)</br>
			Frankfurt (eu-de) - no {{site.data.keyword.mql}} API </td>

		</tr>
		<tr>
     	    <td>**APIs supported**</td>
			<td>Kafka API</br>
			Admin REST API<br/>
			Kafka REST API</br>
			MQ Light API</br>
		    </td>
		</tr>
			<td>**Cloud Object Storage bridge and<br/>
			MQ bridge supported**</td>
			<td>Yes</td>
		</tr>
		<tr>
			<td>**Deployment timeframe**</td>
			<td>Instantaneous provisioning</td>
		</tr>

</table>

