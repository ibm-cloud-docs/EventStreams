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

# Alpha users
{: #alpha_users }

Use  the following information to get your app running with the Message Hub Alpha program:


## Getting started with the Alpha program
{: alpha_getting_started}

1. Navigate to the *Message Hub vNext - Integration* tile, which is an experimental service in the catalog: https://console.stage1.bluemix.net/catalog/labs/?search=vnext

2. Select the ```Premium``` pricing plan from the dropdown list. 

3. Create the service for a single-tenant Message Hub cluster.

The maximum cluster size and storage allocation is ...

The cluster is provisioned with a single Kafka version, a fixed number of nodes, storage, and maximum retention period, which you cannot change.

The Alpha is available in US-South only.



## Single tenant Premium plan
{: premium_plan}

The Premium plan is designed for users who have performance and other functional requirements that go beyond the public service. The Premium plan provides a single-tenant version of the service on shared network and shared compute.

For the Alpha, there is no Lite or Standard plan.
	
* You can define the number of partitions and storage (within the maximum storage allocated to the cluster)

* No quotas or throttling.

* You can use Kafka clients from 0.10 and later and it supports Kafka Streams and KSQL.

* You can use the Kafka REST admin interface to create, list, and delete topics.


## Security
{: security}

The authentication method used to access Message Hub resources is IAM service key and SASL. A TLS certificate is shared across a region and SNI support is required.

You can connect new and existing applications to both a multi-tenant and single-tenant resources.

## Resource controller management

TBD

## Availability zones
{: availability_zones}

The Alpha is available in US-South only.


## Administering Message Hub

### Administering Message Hub using the dashboard in the IBM Cloud console

* You can create, list, and delete topics.

* You cannot change your configuration or view the current configuration.

* No metrics, logs, or usage information are available.


### Administering Message Hub using the Kafka REST interface

* You can create, list, and delete topics.
* V1 is backwards compatible with existing Kafka REST admin
* V2 will allow cluster administration and options in future, but currently allows topics only.

This interface uses TLS 1.2 and there is no authorization at topic level.


## Samples

Samples are specific to the Alpha program. You can find samples for the Alpha: ...

## Compatibility

* UI

* REST APIs

New and existing applications can connect to both a multi-tenant and single-tenant resource. 


## Kafka information

Message Hub is based on Kafka 1.0.

* No quotas are enforced.

* No multitenancy 

The following Kafka client versions are supported:

* 1.0
* 0.11
* 0.10 

0.9 clients are not supported.



## Migration and coexistence

### Apps that use VCAP services
{: notoc}

If you have an existing app that uses VCAP services, you  must make the following code change to ensure it keeps working ...


## Alpha limitations

The current limitations of this Alpha program are as follows:

- No options: clusters are provisioned with a single Kafka version, with a fixed number of nodes, storage, and a maximum retention period.

- No authorization just authentication, that is, you cannot apply fine-grained authorization on topics.

- No CLI

- No user-controlled scaling

- No configuration personalization

- No Kafka REST 1.0

- No Schema Registry 

- No MQ Light API

- No bridges
-
- No integration with the Activity Tracker service (previously known as AccessTrail)  cloudaccesstraillong:

- No VPC

- No BYOK

- No Kafka Connect






