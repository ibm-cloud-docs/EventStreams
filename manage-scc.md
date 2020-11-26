---
copyright:
  years: 2020
lastupdated: "2020-10-20"

keywords: security and compliance for Event Streams, security for Event streams, compliance for Event Streams,

subcollection: <!--Your subcollection value-->

---

{:external: target="_blank" .external}
{:note: .note}
{:term: .term}
{:shortdesc: .shortdesc}
{:table: .aria-labeledby="caption"}


# Managing security and compliance with Event Streams
{: #manage-security-compliance}

<!-- Name this file `manage-scc.md` and place it in the "Enhancing security" topic group. -->

Event Streams is integrated with the {{site.data.keyword.compliance_short}} to help you manage security and compliance for your organization.
{: shortdesc}

<!--Add the following sections as your service onboards to the Security and Compliance Center. You might have only monitoring or you might also have configuration enforcement. Also, if you only have one of the options, be sure to remove the bulleted list and write the following section as a sentence.-->

With the {{site.data.keyword.compliance_short}}, you can:

* Monitor for controls and goals that pertain to Event Streams.
* Define rules for Event Streams that can help to standardize resource configuration.

## Monitoring security and compliance posture with Event Streams
{: #monitor-messagehub}

As a security or compliance focal, you can use the *Event Streams* [goals](#x2117978){: term} to help ensure that your organization is adhering to the external and internal standards for your industry. By using the {{site.data.keyword.compliance_short}} to validate the resource configurations in your account against a [profile](#x2034950){: term}, you can identity potential issues as they arise.

All of the goals for Event Streams are added to the {{site.data.keyword.cloud_notm}} Best Practices Controls 1.0 profile but can also be mapped to other profiles.
{: note}

To start monitoring your resources, check out [Getting started with {{site.data.keyword.compliance_short}}](/docs/security-compliance?topic-security-compliance-getting-started)

### Available goals for Event Streams
{: #messagehub-available-goals}

* *Ensure the Event Streams instance is configured with a public service-endpoint*
* *Ensure the Event Streams instance is configured with a private service-endpoint*
* *Ensure the Event Streams instance is configured with an allow list for ip-addresses*

## Governing Event Streams resource configuration
{: #govern-messagehub}

As a security or compliance focal, you can use the {{site.data.keyword.compliance_short}} to define configuration rules for the instances of Event Streams that you create.

[Config rules](#x3084914){: term} are used to enforce the configuration standards that you want to implement across your accounts. To learn more about the about the data that you can use to create a rule for Event Streams, review the following table.

| Resource kind | Property | Operator | Value | Description |
|---------------|----------|---------------|-------|-------------|
| instance | public_network_enabled | is_true <br>is_false | - | Indicates whether access to a Event Streams instance is allowed through a public network. |
| instance | private_network_enabled | is_true <br>is_false | - | Indicates whether access to a Event Streams instance is allowed through a private network. |
| instance | private_access_allowlist | ips_in_range | - | If private networking is enabled this indicates whether access to a Event Streams instance should be restricted to a given range of private IP CIDR formatted subnets. |
{: caption="Table 1. Rule properties for Events Streams" caption-side="top"}

To learn more about config rules, check out [What is a config rule?](/docs/security-compliance?topic=security-compliance-what-is-rule).
