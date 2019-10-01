---

copyright:
  years: 2015, 2019
lastupdated: "2019-10-01"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:deprecated: .deprecated}

# The Classic plan 
{: #plan_choose_classic}

The Classic plan is deprecated. From November 1, 2019, you will no longer be able to provision new instances of the Classic Plan. <br/>However, existing instances will continue to be supported.
From June 30, 2020, the Classic Plan will be retired and no longer supported. Any instance of the Classic Plan still provisioned at this date will be deleted. 
<br/>
For more information, see 
[IBM {{site.data.keyword.messagehub}} Classic Plan is being retired ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/blog/announcements/ibm-event-streams-classic-plan-is-being-retired){:new_window}.
{:deprecated}

{{site.data.keyword.messagehub}} is available as different plans depending on your requirements. For information about the Standard and Enterprise plans, see [Choosing your plan](/docs/services/EventStreams?topic=eventstreams-plan_choose#plan_choose).
{: shortdesc}
 

## Migrating from the Classic plan
{: #migrating_from_classic}

For an overview of migrating from the Classic plan to the new Standard plan, see [Upgrading to the new Standard plan](/docs/services/EventStreams?topic=eventstreams-migrate_classic_plan).

For information about migrating specific capabilities, refer to the following: 
* If you currently use the REST APIs on the Classic plan, see [Migrating the REST APIs](/docs/services/EventStreams?topic=eventstreams-migrate_rest_apis).
* If you currently use the {{site.data.keyword.mql}} API on the Classic plan, see [Migrating MQ Light to Kafka](/docs/services/EventStreams?topic=eventstreams-migrate_mqlight).
* If you currently use the Cloud Object Storage bridge or the MQ bridge, see [Migrating to Kafka Connect](/docs/services/EventStreams?topic=eventstreams-migrate_bridges).

## Classic plan overview
{: #classic_overview}

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

