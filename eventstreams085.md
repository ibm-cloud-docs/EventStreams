---

copyright:
  years: 2015, 2020
lastupdated: "2020-08-04"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka, plan. Enterprise, Standard, Lite

subcollection: EventStreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:note: .note}
{:deprecated: .deprecated}

# Choosing your plan 
{: #plan_choose}

{{site.data.keyword.messagehub}} is available as different plans depending on your requirements: Lite, Standard, Enterprise, and Classic. 

<!--
For information about the Classic plan, see
[Classic plan](/docs/EventStreams?topic=EventStreams-plan_choose_classic#plan_choose_classic).
-->
{: shortdesc}

## Lite plan
{: #plan_lite}

The Lite plan is free for users who want to try out {{site.data.keyword.messagehub}} or build a proof-of-concept. We do not recommend the Lite plan for production use. The Lite plan offers shared access to a multi-tenant {{site.data.keyword.messagehub}} cluster.

## Standard plan
{: #plan_standard}

The Standard plan is appropriate if you require event ingest and distribution capabilities but do not require any additional benefits of the Enterprise plan. The Standard plan offers shared access to a multi-tenant {{site.data.keyword.messagehub}} cluster.

## Enterprise plan 
{: #plan_enterprise}

The Enterprise plan is appropriate if data isolation, guaranteed performance, and increased retention are important considerations. The Enterprise plan offers exclusive access to a dedicated {{site.data.keyword.messagehub}} cluster. You can also provision an {{site.data.keyword.messagehub}} cluster in a geographically local but [single zone location (SZR)](/docs/EventStreams?topic=EventStreams-sla#sla_szr).

## Classic plan
{: #plan_classic}

The Classic plan is deprecated. From November 1, 2019, you can no longer provision new instances of the Classic Plan. However, existing instances will continue to be supported. <br/>From June 30, 2020, the Classic Plan will be retired and no longer supported. Any instance of the Classic Plan still provisioned at this date will be deleted.<br/>
For more information, see 
[IBM {{site.data.keyword.messagehub}} Classic Plan is being retired ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/blog/announcements/ibm-event-streams-classic-plan-is-being-retired){:new_window}.
{:deprecated}

The Classic plan gives access to the previous edition of the Standard plan and is provided for existing workloads and backward compatibility only. You should provision new workloads against the Standard plan.

For information about moving from the Classic plan to either the Enterprise or Standard plans, see [Migrating](/docs/EventStreams?topic=EventStreams-plan_choose_classic#migrating_from_classic).


## What's supported by the Lite, Standard, Enterprise, and Classic plans

The following table summarizes what is supported by the plans:

<table>
    <caption>Table 1. Support in Lite, Standard, Enterprise, and Classic plans</caption>
      <tr>
	        <th></th>
		    <th>Lite Plan</th>
		    <th>Standard Plan</th>
	      	    <th>Enterprise Plan</th>
		    <th>Classic Plan [<sup>1</sup>](/docs/EventStreams?topic=EventStreams-plan_choose#footnote_classic)</th>
        </tr>
		<tr>
			<td>**Tenancy**</td>
			<td>Multi-tenant </td>
			<td>Multi-tenant </td>
			<td>Single tenant</td>			
			<td>Multi-tenant</td>
		</tr>
        <tr>
			<td>**Availability zones**</td>
			<td>3</td>
			<td>3</td>
			<td>3<br/>(1 in single zone locations)
			</td>
			<td>Not supported</td>
		</tr>
        <tr>
			<td>**Availability**</td>
			<td>99.99% [<sup>2</sup>](/docs/EventStreams?topic=EventStreams-plan_choose#footnote_lite)</td>
			<td>99.99%</td>
			<td>99.99%<br/>(99.9% in single zone locations) [<sup>3</sup>](/docs/EventStreams?topic=EventStreams-plan_choose#footnote_plans)</td>
			<td>99.5%</td>
		</tr>
	  		<tr>
			<td>**Kafka version on cluster**</td>
			<td>Kafka 2.3</td>
			<td>Kafka 2.3</td>
			<td>Kafka 2.3</td>
			<td>Kafka 1.1</td>
		</tr>
		<tr>
			<td>**Kafka Connect and Kafka Streams supported **</td>
			<td>No</td>
			<td>Yes</td>
			<td>Yes</td>
			<td>Yes</td>
		</tr>
		<tr>
			<td>**Managed schema registry supported **</td>
			<td>No</td>
			<td>No</td>
			<td>Yes</td>
			<td>No</td>
		</tr>
		<tr>
			<td>**Fine-grained access control**</td>
			<td>Yes</td>
			<td>Yes</td>
			<td>Yes</td>
			<td>No</td>
		</tr>
		<tr>
			<td>**Cloud Service Endpoint support**</td>
			<td>No</td>
			<td>No</td>
			<td>Yes</td>
			<td>No</td>
		</tr>
		<tr>
			<td>**Mirroring support**</td>
			<td>No</td>
			<td>No</td>
			<td>Yes</td>
			<td>No</td>
		</tr>
		<tr>
			<td>**Maximum number of partitions**</td>
			<td>1  [<sup>4</sup>](/docs/EventStreams?topic=EventStreams-plan_choose#footnote_partitions_lite)</td>
			<td>100</td>
			<td>3000 [<sup>5</sup>](/docs/EventStreams?topic=EventStreams-plan_choose#footnote_partitions)</td>
			<td>100</td>
		</tr>
		<tr>
			<td>**Maximum retention period**</td>
			<td>100 MB for the partition for up to 30 days </td>
			<td>1 GB per partition for up to 30 days </td>
			<td>2 TB of usable storage<!--Unlimited up to the storage limit of your plan --></td>
			<td>1 GB per partition for up to 30 days </td>
		</tr>
		<tr>
			<td>**Maximum throughput**</td>
			<td>100 KB per second per partition</td>
			<td>1 MB per second per partition (20 MB per service instance) </td>
			<td>80 MB per second per cluster (peak throughput of 150 MB per second) [<sup>6</sup>](/docs/EventStreams?topic=EventStreams-plan_choose#footnote_throughput)</td>
			<td>1 MB per second per partition</td>
		</tr>
		<tr>
			<td>**Maximum message size**</td>
			<td>1 MB</td>
			<td>1 MB</td>
			<td>1 MB</td>
			<td>1 MB</td>
		</tr>
		<tr>
			<td>**Maximum number of connected clients**</td>
			<td>5</td>
			<td>500</td>
			<td>10 000</td>
			<td>100</td>
		</tr>
		<tr>
			<td>**Location (region) availability**</td>
			<td>Dallas (us-south)</br>
			<br/>
			</td>
			<td>**Multizone location (MZR)**<br/>
			Dallas (us-south)</br>
			Washington (us-east)<br/>
			London (eu-gb)<br/>
			Sydney (au-syd)</br>
			Frankfurt (eu-de)<br/>
			Tokyo (jp-tok)<br/>
			<br/>
			</td>
			<td>**Multizone location (MZR)**</br>
			Dallas (us-south)</br>
			Washington (us-east)<br/>
			London (eu-gb)<br/>
			Sydney (au-syd)</br>
			Frankfurt (eu-de)<br/>
			Tokyo (jp-tok)<br/>
			<br/>
			**Single zone location (SZR)**</br>
			Seoul (seo01)<br/>
			Chennai (che01)<br/>
			<br/>
			</td>
			<td>Dallas (us-south)</br>
			London (eu-gb)</br>
			Sydney (au-syd)</br>
			Frankfurt (eu-de) - no {{site.data.keyword.mql}} API </td>
		</tr>
		<tr>
     	    <td>**APIs supported**</td>
			<td>Kafka API</br>
			Admin REST API<br/>
			REST Producer API</br>
		    </td>
			<td>Kafka API<br/>
			Admin REST API</br>
			REST Producer API</br>
			</td>
			<td>Kafka API</br>
			Admin REST API<br/>
			REST Producer API</br>
			Schema Registry API</br>
		    </td>
			<td>Kafka API</br>
			Admin REST API<br/>
			Kafka REST API</br>
			MQ Light API</br>
		    </td>
		</tr>
		</tr>
			<td>**Cloud Object Storage bridge and<br/>
			MQ bridge supported**</td>
			<td>No</td>
			<td>No</td>
			<td>No</td>
			<td>Yes</td>
		</tr>
		<tr>
			<td>**Deployment timeframe**</td>
			<td>Instantaneous provisioning</td>
			<td>Instantaneous provisioning</td>
			<td>Expect provisioning to take up to 3 hours. Because Enterprise has its own dedicated resources for each cluster, it requires more time for provisioning</td>
			<td>Instantaneous provisioning</td>
		</tr>
		<tr>
			<td>**Compliance**</td>
			<td>GDPR<br/>
Privacy Shield<br/></td>
			<td>GDPR<br/>
Privacy Shield<br/>
ISO 27001, 27017, 27018<br/></td>
			<td>GDPR<br/>
Privacy Shield<br/>
ISO 27001, 27017, 27018<br/>
SOC 1 Type 1<br/>
SOC 2 Type 1<br/>
HIPAA ready<br/>
PCI<br/>
</td>
			<td>GDPR<br/>
Privacy Shield<br/>
ISO 27001, 27017, 27018<br/></td>
		</tr>

</table>

### Footnotes
{: #footnote_plans notoc}

1. {: #footnote_classic notoc} The Classic plan is deprecated. For more information, see [Classic plan deprecation](/docs/EventStreams?topic=EventStreams-plan_choose#plan_classic) and [moving to the Standard plan](/docs/EventStreams?topic=EventStreams-plan_choose_classic#migrating_from_classic).
2. {: #footnote_lite notoc} After 30 days of inactivity, your instance is deleted. (Inactivity is defined as a zero bytes_out metric even though you might have created a partition or produced messages.)
3. {: #footnote_szr notoc} For more information about availability, see [single zone location deployments](/docs/EventStreams?topic=EventStreams-sla#sla_szr).
4. {: #footnote_partitions_lite notoc} If you migrate from the Lite to the Standard plan, allow a few minutes for the cached limit of 1 partition to clear so that you can take advantage of the 100 partition limit for the Standard plan.
5. {: #footnote_partitions notoc} 3000 is a hard limit for partitions on the Enterprise plan. If you reach this limit, you can no longer create topics. To increase the number of partitions beyond 3000, [contact IBM ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/get-support?topic=get-support-getting-customer-support#using-avatar){:new_window}.
6. {: #footnote_throughput notoc} A recommended maximum is 80 MB per second, that is 40 MB per second for producing and 40 MB per second for consuming. <br/>
A recommended peak limit is 150 MB per second, that is 75 MB per second for producing and 75 MB per second for consuming.




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

For more information, see [{{site.data.keyword.Bluemix_notm}} Public ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/free/){:new_window}.
-->

