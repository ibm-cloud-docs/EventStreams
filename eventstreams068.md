---

copyright:
  years: 2015, 2020
lastupdated: "2020-09-24"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: EventStreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Data security and privacy
{: #data_security}


{{site.data.keyword.IBM}} uses the following methods to help ensure the security and
privacy of your data:
{:shortdesc}

## Cryptographic protocols
{: #cryptographic}

* Connections are restricted to the following strong cipher suites:

      * ECDHE-RSA-AES128-GCM-SHA256
      * ECDHE-RSA-AES256-GCM-SHA384
      * ECDHE-RSA-AES128-SHA256
      * ECDHE-RSA-AES256-SHA384
      * ECDHE-RSA-AES256-SHA384

* To be a fully supported configuration, all clients must support the following:
    * TLS v1.2
    * elliptic curve cryptography
    * TLS server name indication (SNI)

* Additionally, you must use TLS v1.2 in the following cases:
    * for making connections to the Kafka native and REST interfaces 
    * the browser that you use to access the {{site.data.keyword.messagehub}} dashboard must support TLS v1.2

   
## Encryption of message payloads, topic names, and consumer groups
{: #encryption_payloads}

Message data is encrypted for transmission between {{site.data.keyword.messagehub}}
and clients as a result of TLS. {{site.data.keyword.messagehub}} stores message data
at rest and message logs on encrypted disks.

Topic names and consumer groups are encrypted for transmission between 
{{site.data.keyword.messagehub}} and clients as a result of TLS. However, 
{{site.data.keyword.messagehub}} does not encrypt these values at rest. Therefore, you are not recommended to use confidential information in your topic names.

For information about compliance on each of the {{site.data.keyword.messagehub}} plans, see 
[What's supported by the Lite, Standard, Enterprise, and Classic plans](/docs/EventStreams?topic=EventStreams-plan_choose#what-s-supported-by-the-lite-standard-enterprise-and-classic-plans).

## Data isolation model
{: #data_isolation}

{{site.data.keyword.messagehub}}'s data isolation model varies according to which plan you're using.

### Enterprise plan
The Enterprise plan provides a tenant-specific service in the IBM Service domain.

The Enterprise plan creates a single tenant instance on a Dedicated Kubernetes cluster on Shared Hardware (VSI isolation).

By default, the Enterprise plan provides Public endpoints, but it also supports Cloud Service Endpoints to enable Private Endpoints for further network isolation on request.

The Enterprise plan creates single tenant Block storage for each new instance.


### Standard plan
The Standard plan provides a Public Service with Public endpoints.

The Standard plan creates a tenant instance on a Shared Kubernetes cluster on shared hardware (VSI isolation).

The Standard plan provides Public endpoints only.

The Standard plan uses Shared Block storage and achieves tenant isolation through separation of files and access controls.

## Data retention and reclamation

When a service instance is deleted, the data is not deleted immediately. Instead, it is scheduled for reclamation, {{site.data.keyword.messagehub}} sets this retention period to three days, after which the data (both, topics and messages written to the topics) is irreversibly destroyed. It is also possible to restore a deleted instance that has not yet been reclaimed.

It is possible to check the status of a reclamation, as well as force or cancel a scheduled reclamation using [the IBM Cloud® Platform CLI](https://cloud.ibm.com/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_reclamations).
