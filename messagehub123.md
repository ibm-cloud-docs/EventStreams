---

copyright:
  years: 2015, 2018
lastupdated: "2018-04-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Using {{site.data.keyword.iamshort}} (IAM) with the Alpha program
{: #alpha_iam }

{{site.data.keyword.messagehub}} permissions are configured using IAM policies. An IAM policy consists of the following information:

* a service ID
* an {{site.data.keyword.Bluemix_short}} resource defined by a service name, service instance, region, IAM resourceType, and IAM resource
* a role (Reader, Writer, Manager)

For more information about IAM, see: 
[IBM Cloud Identity and Access Management](/docs/iam/index.html#iamoverview).

For an example about how to set policies, see: 
[Introducing IBM Cloud IAM Service IDs and API Keys ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2017/10/introducing-ibm-cloud-iam-service-ids-api-keys/){:new_window}.

## {{site.data.keyword.messagehub}} IAM resources:
{: iam_resources}

{{site.data.keyword.messagehub}} exposes 4 types of IAM resourceTypes:

* cluster
* topic
* group
* txnid

You can identify unique resources for topic, group, and txnid by setting the IAM resource. The cluster resourceType is a singleton, so it does not need to be uniquely identified.

## Common scenarios
{: iam_scenarios}

Here are some common {{site.data.keyword.messagehub}} scenarios and the permissions you need to grant:

Producer to some topics (same for idempotent):
* Reader on the cluster resourceType
* Writer on each topic resourceType and topic name resource

Transactional producer:
* same as producer
* Writer on txnid resourceType and transaction id resource
* Reader on group resourceType and group id resource

Consumer (no group):
* Reader on the cluster resourceType
* Reader on each topic resourceType and topic name resource

Consumer with group:
* same as consumer
* Reader on group resourceType and group id resource

Create or delete topic:
* Reader on the cluster resourceType
* Manager on each topic resourceType and topic name resource

Delete consumer group:
* Reader on the cluster resourceType
* Manager on group resourceType and group id resource

List groups/topics/offsets, Describe group/topic/broker configs
* Reader on the cluster resourceType









