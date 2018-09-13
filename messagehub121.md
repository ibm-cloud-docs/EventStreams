---

copyright:
  years: 2015, 2018
lastupdated: "2018-02-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

<!-- Notes from chat with Charlie 

Different plan for provisioning

Quality of service from each plan

Life of a user through cycle - APIs, feature sets

-->


# Getting started with {{site.data.keyword.messagehub}} vNext
{: vnext_started}

1. Navigate to the experimental service {{site.data.keyword.messagehub}} vNext tile in the catalog. https://console.stage1.bluemix.net/catalog/labs/?search=vnext

2. Select the Premium pricing plan from the dropdown list. This plan is available to paid accounts only.

3. Create the service for a single-tenant {{site.data.keyword.messagehub}} cluster.

The maximum cluster size and storage allocation is ...

The cluster is provisioned with a single Kafka version, a fixed number of nodes, storage, and maximum retention period, which you cannot change.

Available in US-South only.

## Pricing plans
{: pricing_plans}

* No Lite plan

* No Standard plan
	
For more information about account types, see https://console.bluemix.net/docs/account/index.html#liteaccount
	
	
## Tenants

### Single tenant (Premium plan)

 - you can define the number of partitions and storage (within maximum storage allocated to the cluster)

No quotas or throttling.

Kafka clients from 0.10 and later

Supports Kafka Streams, Kafka Connect, and KSQL.

Use REST admin interface to create, list, and delete topics



|   |Public   |Public   |Public   |Dedicated   |
|---|---|---|---|---|
|Cluster tenancy   |Multi tenant   |Single tenant   |Single tenant   |Single tenant   |
|Plan   |Lite, Standard   |Premium   |Premium++   |Premium++   |
|Pricing   |Based on usage   |Subscription   |Subscription   |Subscription   |

## Which plan is best for me?

### {{site.data.keyword.messagehub}} Public
I want to consume {{site.data.keyword.messagehub}}. Consuming a multi-tenant service with some performance limitations is not an issue for me.

### {{site.data.keyword.messagehub}} Premium
I want to consume {{site.data.keyword.messagehub}}. I have performance and other functional requirements that go beyond the public service. I am happy to pay a premium for a single-tenant version of the service on shared network and shared compute.

### {{site.data.keyword.messagehub}} Premium++
I want to consume {{site.data.keyword.messagehub}}. I require more isolation than the {{site.data.keyword.messagehub}} Premium plan. I would like an isolated network and isolated compute by having the service deployed within my IBM Cloud Dedicated.next VPC.


## Security
{: security}

IAM  service key and SASL are used as the authentication method to access {{site.data.keyword.messagehub}} resources

New and existing applications can connect to both a multi tenant & single tenant resource 

TLS certificate shared across a region.

SNI support required.


## Availability zones
{: availability_zones}

3 availability zones are used
(A location within a region that IBM Containers runs in.)


## Catalog and tiles
From the catalog page, select either single tenant or multi tenant {{site.data.keyword.messagehub}} tile.

## Resource controller management

## Compatibility

* UI

* REST APIs

New and existing applications can connect to both a multi-tenant and single-tenant resource. 


## Kafka

{{site.data.keyword.messagehub}} is based on Kafka 1.0

No quotas enforced

No multitenancy (contradicts info about "select either single tenant or multi tenant {{site.data.keyword.messagehub}} tile.")

The following Kafka client versions are supported:

* 1.0
* 0.11
* 0.10 

0.9 clients are not supported.


## Administering {{site.data.keyword.messagehub}}

### Administering {{site.data.keyword.messagehub}} using the dashboard in the IBM Cloud console

* You can create, list, and delete topics.

* You cannot change your configuration or view the current configuration.

* No metrics, logs, or usage information are available.


### Administering {{site.data.keyword.messagehub}} using the REST interface

* You can create, list, and delete topics.
* V1 is backwards compatible with existing Kafka REST admin
* V2 will allow cluster administration and options in future, but currently allows topics only.

Uses TLS 1.2

No authorization at topic level


## Samples

Samples are different during the Alpha program, compared to the existing ones. You can find samples for the Alpha: ...


## Apps that use VCAP services

If you have an existing app that uses VCAP services, you  must make the following code change to ensure it keeps working ...

## Migration and coexistence


## vNext limitations

The current limitations of vNext are as follows:

- No options: clusters are provisioned with a single Kafka version, with a fixed number of nodes, storage, and maximum retention period.

- No authorization just authentication, that is, you cannot apply fine-grained authorization on topics.

- No CLI

- No user-controlled scaling

- No config personalization

- No Kafka REST 1.0

- No Schema Registry 

- No MQ Light API

- No bridges

- No Activity Tracker (previously AccessTrail) - Investigate integration

- No VPC

- No BYOK






