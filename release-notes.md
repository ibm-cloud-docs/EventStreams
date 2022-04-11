---

copyright:
  years: 2022
lastupdated: "2022-03-25"

keywords: event streams release notes

subcollection: EventStreams

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}


# Release notes for {{site.data.keyword.messagehub}}
{: #event-streams-relnotes}

Use these release notes to learn about the latest {{site.data.keyword.messagehub_full}} that are grouped by date. Release notes are available for a minimum of three years.
{: shortdesc}

## 1 July 2019
{: #EventStreams-july2019}
{: release-note}

Updates to Enterprise plan
:   Kafka version upgrade.
:   Support for Cloud Service Endpoints.

Kafka version upgrade
:   {{site.data.keyword.messagehub}} Enterprise will now be supporting version 2.2 of Apache Kafka to align with our recently released and upgraded Standard plan.
:   This update for {{site.data.keyword.messagehub}} will be non-disruptive and has been tested with our supported Kafka client list.
:   If your Kafka client is not on this list, then whilst we expect the upgrade to be non-disruptive, these clients have not been tested and we cannot offer any support 
statement for these clients. If this is a concern, we would recommend performing any additional testing you require.
:   Note: The Standard plan has already been updated to Kafka 2.2 and can be used for additional testing.

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
