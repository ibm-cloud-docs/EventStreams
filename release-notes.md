---

copyright:
  years: 2022, 2023
lastupdated: "2023-09-28"

keywords: release notes

subcollection: EventStreams

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}


# Release notes for {{site.data.keyword.messagehub}}
{: #event-streams-relnotes}

Use these release notes to learn about the latest updates to {{site.data.keyword.messagehub_full}} that are grouped by date. Release notes are available for a minimum of three years.
{: shortdesc}

## September 2023
{: #EventStreams-sep2023}
{: release-note}

Self-service mirroring enablement 
:   You can enable mirroring by running a **service-instance-update** CLI command against your target cluster, instead of raising a support ticket. To find out more, see [Enabling mirroring](/docs/EventStreams?topic=EventStreams-mirroring_setup).

## August 2023
{: #EventStreams-sep2023}
{: release-note}

UI Enhancements  
:   Topics Page Upgrade - Users interacting the UI now have improved topic overview page with core components redesigned including topic details and streamlanding wizard
:   Topic Editing - Users can configure their topics directly from the GUI
:   Topics Pagination - Topic overview page now paginates topics, providing users with a better layout and easier navigation of the UI.

## June 2023
{: #EventStreams-jun2023}
{: release-note}

Additional topic partition metrics
:   The message rate per partition is now available. For more information, see [Message rate per partition metric](/docs/EventStreams?topic=EventStreams-metrics#ibm_eventstreams_instance_message_rate_per_partition). 

Usage quotas per user available
:   Kafka administrators can now use metrics to identify users who are consuming unexpectedly large amounts of bandwidth and then apply a quota. Kafka users with a quota have visibility of how much capacity they have left before throttling starts. For more information, see [IAM ID bytes](/docs/EventStreams?topic=EventStreams-metrics#ibm_eventstreams_iam_id_bytes_in_per_second).
 
## May 2023
{: #EventStreams-may2023}
{: release-note}

Schema registry endpoints
:   An {{site.data.keyword.messagehub}} user can use a larger subset of the Confluent Schema Registry REST API to manage their schema registry. 

Lenses.io integration
: {{site.data.keyword.messagehub}} now integrates with Lenses, a third party DataOps platform for Apache Kafka. To find out how to install Lenses with {{site.data.keyword.messagehub}}, see [Getting started with {{site.data.keyword.messagehub}}](https://docs.lenses.io/5.2/installation/getting-started/managed/ibm/). 

Apache Kafka upgrade
:   Upgrade to Apache Kafka version 3.3.

## April 2023
{: #EventStreams-apr2023}
{: release-note}

{{site.data.keyword.messagehub}} Enterprise plan is certified IRAP Protected
:   The Information Security (InfoSec) Registered Assessors Program (IRAP) outlines a framework for assessing the implementation and effectiveness of {{site.data.keyword.messagehub}} and IBM Cloud's security controls against the Australian government's Information Security Manual (ISM). The {{site.data.keyword.messagehub_full_notm}} Enterprise plan has been assessed as compliant with IRAP Protected. For reports, documentation and further details on IBM Cloud IRAP Protected Offerings, see [IBM Cloud compliance: IRAP (Australia)](https://www.ibm.com/cloud/compliance/irap-australia?_gl=1*nwr26q*_ga*OTk4NjUzOTE2LjE2OTI4OTA4MDA.*_ga_FYECCCS21D*MTY5Mjg5MDgwMC4xLjEuMTY5Mjg5MjcyNC4wLjAuMA).

## March 2023
{: #EventStreams-mar2023}
{: release-note}

OAUTHBEARER users app to service authentication
:   {{site.data.keyword.messagehub}} users can configure their Kafka client with more secure and ephemeral [SASL OAUTHBEARER](/docs/EventStreams?topic=EventStreams-kafka_using#kafka_api_client), in addition to API keys.

ISMAP and C5 Certification
:   {{site.data.keyword.messagehub}} Standard and Enteprise plans were certified by the [ISMAP (Information System Security Management and Assessment Program)](/docs/EventStreams?topic=EventStreams-compliance#ismap), the Japanese government program for assessing the security of public cloud services. {{site.data.keyword.messagehub}} Standard and Enterprise plans were audited and certified to [C5 (Cloud Computing Compliance Controls Catalogue)](/docs/EventStreams?topic=EventStreams-compliance#c5) and meet the requirements for cloud security and the adoption of public cloud solutions by German government agencies.

Kafka version by using the CLI and console
:   You can now check the version of Kafka by using through the command line and console.

## January 2023
{: #EventStreams-jan2023}
{: release-note}

Quota management by using the REST API
:   You can enforce production and consumption rate limits by settings quotas using the Admin REST API. For more information, see [List each entity's quota information](/apidocs/event-streams/adminrest#list-quotas) to prevent network saturation or monopolizing broker resources.

## October 2022
{: #EventStreams-oct2022}
{: release-note}

Context-based restrictions
:   You can use network type or context-based restrictions to restrict the network connectivity on the Enterprise plan. For more information, see [Restricting Network Access](/docs/EventStreams?topic=EventStreams-restrict_access).

Apache Kafka upgrade
:   Upgrade to Apache Kafka version 3.1.

## July 2022
{: #EventStreams-jul2022}
{: release-note}

Enhanced support for matching schemas
:   Enhanced support for matching schemas when you use Confluent SerDes with the schema registry.

## May 2022
{: #EventStreams-may2022}
{: release-note}

Schema registry support on the Satellite plan
:   The new [Satellite plan](/docs/EventStreams?topic=EventStreams-satellite_about) now supports the [Schema registry API](/docs/EventStreams?topic=EventStreams-satellite-provisioning#satellite-enable-schema-registry).

## April 2022
{: #EventStreams-apr2022}
{: release-note}

Satellite plan
:   With the new [Satellite plan](/docs/EventStreams?topic=EventStreams-satellite_about), you can create a hybrid environment that brings the scalability and on-demand flexibility of public cloud services to the applications and data that run in your secure private cloud.

More topic and consumer group metrics
:   More topic and consumer group metrics are available, see [Monitoring Event Streams metrics by using IBM Cloud Monitoring](/docs/EventStreams?topic=EventStreams-metrics).

## December 2021
{: #EventStreams-dec2021}
{: release-note}

Apache Kafka upgrade
:   Upgrade to Apache Kafka version 2.8.

## October 2021
{: #EventStreams-oct2021}
{: release-note}

IAM
:  [IAM IP address access restrictions](/docs/EventStreams?topic=EventStreams-restricting_access_iam).

## August 2021
{: #EventStreams-aug2021}
{: release-note}

New region support
:   Sao Paulo region support.

## June 2021
{: #EventStreams-jun2021}
{: release-note}

Streaming to {{site.data.keyword.cos_full}}  by using {{site.data.keyword.sqlquery_full}} 
:   [Event Streaming general availability](/docs/EventStreams?topic=EventStreams-streaming_cos_sql). From the {{site.data.keyword.messagehub}} UI, select and link topics to {{site.data.keyword.cos_full}}  buckets, and stream data automatically and securely by using the fully managed {{site.data.keyword.sqlquery_short}} service. 

## May 2021
{: #EventStreams-may2021}
{: release-note}

New region support
:   Toronto region support.

## April 2021
{: #EventStreams-apr2021}
{: release-note}

Security and compliance center support
:  [Security and compliance center support](/docs/EventStreams?topic=EventStreams-manage-security-compliance) helps you manage security and compliance for your organization.

## March 2021
{: #EventStreams-mar2021}
{: release-note}

New region support
:   Osaka region support.

## January 2021
{: #EventStreams-jan2021}
{: release-note}

Apache Kafka upgrade
:   Upgrade to Apache Kafka version 2.6 for all plans.

## September 2020
{: #EventStreams-sep2020}
{: release-note}

Scaling support for Enterprise Plan
:   [Scale your Enterprise Plan clusters](/docs/EventStreams?topic=EventStreams-plan_choose#plan_enterprise) to allow for greater throughput and higher retention.

## August 2020
{: #EventStreams-aug2020}
{: release-note}

Mirroring support for Enterprise Plan
:   [Mirroring](/docs/EventStreams?topic=EventStreams-mirroring) enables messages in one service instance to be copied continually to a second instance, allowing disaster recovery scenarios to be implemented easily.

Terraform support
:   Create your {{site.data.keyword.messagehub}} instances and subsequent configuration by using Terraform.

## June 2020
{: #EventStreams-jun2020}
{: release-note}

Schema registry support for Enterprise plan
:   Add structure to your messages by using the {{site.data.keyword.messagehub}} [Schema registry](/docs/EventStreams?topic=EventStreams-ES_schema_registry).

## March 2020
{: #EventStreams-mar2020}
{: release-note}

Customer metrics support
:   Get visibility of metrics for your Enterprise {{site.data.keyword.messagehub}} instance through a new customer metrics dashboard.

## November 2019
{: #EventStreams-nov2019}
{: release-note}

Apache Kafka upgrade
:   Upgrade to Apache Kafka version 2.3.

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
:   {{site.data.keyword.messagehub}} Enterprise supports version 2.2 of Apache Kafka to align with our recently released and upgraded Standard plan.
:   This update for {{site.data.keyword.messagehub}} is nondisruptive and was tested with our supported Kafka client list.
:   If your Kafka client is not on this list, then while we expect the upgrade to be nondisruptive, these clients were not tested and we cannot offer any support
statement for these clients. If this is a concern, do any extra testing that you require.
:   Note: The Standard plan is already updated to Apache Kafka version 2.2 and can be used for extra testing.

Support for Cloud service endpoints
:   {{site.data.keyword.messagehub}} supports Cloud service endpoints.
:   This capability means that any data that you publish or consume from the {{site.data.keyword.messagehub}} service is over the private network and not public interfaces.

## 14 May 2019
{: #EventStreams-may2019}
{: release-note}

New Standard plan
:   Support for Apache Kafka version 2.2.
:   Support for fine-grained authorization to topic level.
:   Support for availability zones to further increase the resiliency of the service.
:   A brand new {{site.data.keyword.IBM}} Design Thinking-led developer and user experience.
:   Available in the US-South region.
