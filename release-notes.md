---

copyright:
  years: 2022
lastupdated: "2022-04-22"

keywords: event streams release notes

subcollection: EventStreams

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}


# Release notes for {{site.data.keyword.messagehub}}
{: #event-streams-relnotes}

Use these release notes to learn about the latest {{site.data.keyword.messagehub_full}} that are grouped by date. Release notes are available for a minimum of three years.
{: shortdesc}

## April 2022
{: #EventStreams-apr2022}
{: release-note}

Satellite plan
:   The new [Satellite plan](/docs/EventStreams?topic=EventStreams-satellite_about) enables you to create a hybrid environment that brings the scalability and on-demand flexibility of public cloud services to the applications and data that run in your secure private cloud.

## December 2021
{: #EventStreams-dec2021}
{: release-note}

Upgrade to Apache Kafka version 2.8.

## October 2021
{: #EventStreams-oct2021}
{: release-note}

[IAM IP address access restrictions](/docs/EventStreams?topic=EventStreams-restricting_access_iam).

## August 2021
{: #EventStreams-aug2021}
{: release-note}

Sao Paolo region support.

## June 2021
{: #EventStreams-jun2021}
{: release-note}

Streaming to Cloud Object Storage by using SQL Query
:   [Event Streaming general availability](/docs/EventStreams?topic=EventStreams-streaming_cos_sql). From the {{site.data.keyword.messagehub}} UI, select and link topics to Cloud Object Storage buckets, and stream data automatically and securely using the fully-managed {{site.data.keyword.sqlquery_full}} service. 

## May 2021
{: #EventStreams-may2021}
{: release-note}

Toronto region support.

## April 2021
{: #EventStreams-apr2021}
{: release-note}

[Security and compliance center support](https://cloud.ibm.com/docs/EventStreams?topic=EventStreams-manage-security-compliance).

## March 2021
{: #EventStreams-mar2021}
{: release-note}

Osaka region support.

## January 2021
{: #EventStreams-jan2021}
{: release-note}

Upgrade to Apache Kafka version 2.6 for all plans.

## September 2020
{: #EventStreams-sep2020}
{: release-note}

[Scaling support for Enterprise Plan](/docs/EventStreams?topic=EventStreams-plan_choose#plan_enterprise)
:   Scale your Enterprise Plan clusters to allow for greater throughput and higher retention.

## August 2020
{: #EventStreams-aug2020}
{: release-note}

[Mirroring support for Enterprise Plan](/docs/EventStreams?topic=EventStreams-mirroring)
:   Mirroring enables messages in one service instance to be copied continually to a second instance, allowing disaster recovery scenarios to be implemented easily.

Terraform support
:   Create your {{site.data.keyword.messagehub}} instances and subsequent configuration using Terraform.

## June 2020
{: #EventStreams-jun2020}
{: release-note}

[Schema Registry support for Enterprise plan](/docs/EventStreams?topic=EventStreams-ES_schema_registry)
:   Add structure to your messages using the {{site.data.keyword.messagehub}} Schema Registry.

## March 2020
{: #EventStreams-mar2020}
{: release-note}

Customer metrics support
:   Get visibility of metrics for your Enterprise {{site.data.keyword.messagehub}} instance through a new customer metrics dashboard.

## November 2019
{: #EventStreams-nov2019}
{: release-note}

Upgrade to Apache Kafka version 2.3.

Bring Your own key for Enterprise plan
:   Allows users to secure their data at rest with their own encryption key.

IP Allowlisting support
:   Allows users to stipulate source IPs from which users must connect to {{site.data.keyword.messagehub}}.

## September 2019
{: #EventStreams-sep2019}
{: release-note}

New Lite plan
:   Release of the [Lite plan](/docs/EventStreams?topic=EventStreams-plan_choose#plan_lite) in US-South allowing users to provision a minimal {{site.data.keyword.messagehub}} instance for free.

## 1 July 2019
{: #EventStreams-july2019}
{: release-note}

Updates to Enterprise plan
:   Apache Kafka version upgrade.
:   Support for Cloud Service Endpoints.

Kafka version upgrade
:   {{site.data.keyword.messagehub}} Enterprise will now be supporting version 2.2 of Apache Kafka to align with our recently released and upgraded Standard plan.
:   This update for {{site.data.keyword.messagehub}} will be non-disruptive and has been tested with our supported Kafka client list.
:   If your Kafka client is not on this list, then whilst we expect the upgrade to be non-disruptive, these clients have not been tested and we cannot offer any support
statement for these clients. If this is a concern, we would recommend performing any additional testing you require.
:   Note: The Standard plan has already been updated to Apache Kafka version 2.2 and can be used for additional testing.

Support for Cloud Service Endpoints
:   {{site.data.keyword.messagehub}} supports Cloud Service Endpoints.
:   This capability means that any data you publish or consume from the {{site.data.keyword.messagehub}} service will be over the private network and not public interfaces.

## 14 May 2019
{: #EventStreams-may2019}
{: release-note}

New Standard plan
:   Support for Apache Kafka version 2.2.
:   Support for fine-grained authorization to topic level.
:   Support for availability zones to further increase the resiliency of the service.
:   A brand new {{site.data.keyword.IBM}} Design Thinking-led developer and user experience.
:   Available in the US-South region.
