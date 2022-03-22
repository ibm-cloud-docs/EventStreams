---
copyright:
  years: 2021, 2022
lastupdated: "2022-03-21"

keywords: security and compliance for Event Streams, security for Event streams, compliance for Event Streams,

subcollection: EventStreams

---

{:external: target="_blank" .external}
{:note: .note}
{:term: .term}
{:shortdesc: .shortdesc}
{:table: .aria-labeledby="caption"}


# Managing security and compliance with {{site.data.keyword.messagehub}}
{: #manage-security-compliance}

<!-- Name this file `manage-scc.md` and place it in the "Enhancing security" topic group. -->

{{site.data.keyword.messagehub}} is integrated with the {{site.data.keyword.compliance_short}} to help you manage security and compliance for your organization.
{: shortdesc}

With the {{site.data.keyword.compliance_short}}, you can:

* Monitor for controls and goals that pertain to {{site.data.keyword.messagehub}}.
* Define rules for {{site.data.keyword.messagehub}} that can help to standardize resource configuration.

## Monitoring security and compliance posture with {{site.data.keyword.messagehub}}
{: #monitor-eventstreams}

As a security or compliance focal, you can use the *Event Streams* [goals](#x2117978){: term} to help ensure that your organization is adhering to the external and internal standards for your industry. By using the {{site.data.keyword.compliance_short}} to validate the resource configurations in your account against a [profile](#x2034950){: term}, you can identity potential issues as they arise.

All of the goals for {{site.data.keyword.messagehub}} are added to the {{site.data.keyword.cloud_notm}} Best Practices Controls 1.0 profile but can also be mapped to other profiles.
{: note}

To start monitoring your resources, check out [Getting started with {{site.data.keyword.compliance_short}}](/docs/security-compliance?topic-security-compliance-getting-started).

### Available goals for Event Streams
{: #eventstreams-available-goals}

* Check whether {{site.data.keyword.messagehub}} has at least # users with the IAM manager role
* Check whether {{site.data.keyword.messagehub}} has at least # service IDs with the IAM manager role
* Check whether {{site.data.keyword.messagehub}} is accessible through public endpoints
* Check whether {{site.data.keyword.messagehub}} is accessible only by using private endpoints
* Check whether {{site.data.keyword.messagehub}} network access is restricted to a specific IP range

## Governing Event Streams resource configuration
{: #govern-eventstreams}

As a security or compliance focal, you can use the {{site.data.keyword.compliance_short}} to define configuration rules for the instances of {{site.data.keyword.messagehub}} that you create.

[Config rules](#x3084914){: term} are used to enforce the configuration standards that you want to implement across your accounts. To learn more about the data that you can use to create a rule for {{site.data.keyword.messagehub}}, review the following table.

| Resource type | Property | Operator | Value | Description |
|---------------|----------|---------------|-------|-------------|
| instance | public_network_enabled | is_true <br>is_false | - | Indicates whether access to a {{site.data.keyword.messagehub}} instance is allowed through a public network. |
| instance | private_network_enabled | is_true   \n   is_false | - | Indicates whether access to a {{site.data.keyword.messagehub}} instance is allowed through a private network. |
| instance | private_access_allowlist | ips_in_range | - | If private networking is enabled, this property indicates whether access to a {{site.data.keyword.messagehub}} instance should be restricted to a given range of private IP CIDR formatted subnets. |
{: caption="Table 1. Rule properties for {{site.data.keyword.messagehub}}" caption-side="top"}

To learn more about config rules, check out [What is a config rule?](/docs/security-compliance?topic=security-compliance-what-is-governance)
