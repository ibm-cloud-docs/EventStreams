---

copyright:
  years: 2015, 2018
lastupdated: "2018-04-17"

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

Here are some common {{site.data.keyword.messagehub}} scenarios and the permissions you need to grant in each case:

Producer to some topics (same for idempotent):
* Reader role on the cluster resourceType
* Writer role on each topic resourceType and topic name resource

Transactional producer:
* same as producer
* Writer role on txnid resourceType and transaction ID resource
* Reader role on group resourceType and group ID resource

Consumer (no group):
* Reader role on the cluster resourceType
* Reader role on each topic resourceType and topic name resource

Consumer with group:
* Same as consumer
* Reader role on group resourceType and group ID resource

Create or delete topic:
* Reader role on the cluster resourceType
* Manager role on each topic resourceType and topic name resource

Delete consumer group:
* Reader role on the cluster resourceType
* Manager role on group resourceType and group ID resource

List groups, topics and offsets and describe group, topic, and broker configurations
* Reader role on the cluster resourceType









