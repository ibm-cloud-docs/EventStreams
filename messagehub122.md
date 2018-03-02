---

copyright:
  years: 2015, 2018
lastupdated: "2018-03-02"

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

# About the Alpha program
{: #alpha_about }

The Alpha program provides early access to the next version of the {{site.data.keyword.messagehub}} service. 

## About your Alpha cluster

Your Alpha cluster provides a Premimum plan, which enables you to provision your own single-tenant Kafka cluster. The cluster includes 3 Kafka nodes, and is capable of 90,000 KB/sec, over y partitions, and stores data for a maximum of x hours  There are no quotas enforced and there is no multitenancy.

The Kafka server is version x and supports clients from vx onwards, KSQL, and Kafka Streams. A REST API is available for creating, deleting and listing topics.

Access to the instance is managed by IAM

The Alpha program is available in the US-South region only.


## Single-tenant Premium plan
{: premium_plan}

The Premium plan is designed for users who have performance and other functional requirements that go beyond the public service. The Premium plan provides a single-tenant version of the service on a shared network and shared compute.

* You can define the number of partitions and storage (within the maximum storage allocated to the cluster).

* There are no quotas or throttling.

## Connecting your app

If you want to connect one of your apps, your client must support the following features:

* SASL Plain
* SNI

If you want to connect an existing app that works with the current version of Message Hub rather than the Alpha version, you must use different credential information from your VCAP_SERVICES environment variable. Use the ```api_key information``` instead of the ```username/password``` information.

For simple steps to get up and running with the Alpha, see [Getting started with the Alpha program](/docs/services/MessageHub/messagehub120.html).


## Security
{: security}

The authentication method used to access Message Hub resources is an IAM service access key and SASL. A TLS certificate is shared across a region and SNI support is required.

You can connect new and existing applications to a single-tenant resource.

## Resource controller management

TBD


## Administering Message Hub

<!--
### Administering Message Hub using the dashboard in the IBM Cloud console

* You can create, list, and delete topics.

* You cannot change your configuration or view the current configuration.

* No metrics, logs, or usage information are available.
-->

You can administer Message Hub using the Kafka REST interface:

* You can create, list, and delete topics.

* V1 is backwards compatible with the existing Kafka REST admin.

* V2 will allow cluster administration and options in future, but currently allows topics only.

This interface uses TLS 1.2 and there is no authorization at topic level.


## Samples

Samples are specific to the Alpha program. You can find samples for the Alpha: ...

## Compatibility

You can connect new and existing applications to a single-tenant resource. 

## Migration and coexistence

### Apps that use VCAP services
{: notoc}

If you have an existing app that uses VCAP services, you must make the following code change to ensure it keeps working ...


## Alpha limitations

The current limitations of this Alpha program are as follows:

### Not available yet, but coming soon
- A UI

- Multi availability zone support

- User-controlled scaling

- Deeper access controls, including topics

- Integration with the {{site.data.keyword.cloudaccesstrailfull_notm}} service (previously known as AccessTrail) 


### Not currently planned

- Bridges
- REST messaging
- MQ Light APIs
- A Lite or Standard plan.







