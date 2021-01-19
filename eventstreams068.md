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

For TLS v1.2:

      * ECDHE-RSA-AES256-GCM-SHA384
      * ECDHE-RSA-CHACHA20-POLY1305
      * ECDHE-RSA-AES128-GCM-SHA256
      * ECDHE-RSA-AES128-SHA256


For TLS v1.3:

      * ECDHE-ECDSA-AES256-GCM-SHA384
      * ECDHE-RSA-AES256-GCM-SHA384
      * DHE-DSS-AES256-GCM-SHA384
      * DHE-RSA-AES256-GCM-SHA384
      * ECDHE-ECDSA-CHACHA20-POLY1305
      * ECDHE-RSA-CHACHA20-POLY1305
      * DHE-RSA-CHACHA20-POLY1305
      * ECDHE-ECDSA-AES256-CCM8
      * ECDHE-ECDSA-AES256-CCM
      * DHE-RSA-AES256-CCM8
      * DHE-RSA-AES256-CCM
      * ECDHE-ECDSA-ARIA256-GCM-SHA384
      * ECDHE-ARIA256-GCM-SHA384
      * DHE-DSS-ARIA256-GCM-SHA384
      * DHE-RSA-ARIA256-GCM-SHA384
      * ADH-AES256-GCM-SHA384
      * ECDHE-ECDSA-AES128-GCM-SHA256
      * ECDHE-RSA-AES128-GCM-SHA256
      * DHE-DSS-AES128-GCM-SHA256
      * DHE-RSA-AES128-GCM-SHA256
      * ECDHE-ECDSA-AES128-CCM8
      * ECDHE-ECDSA-AES128-CCM
      * DHE-RSA-AES128-CCM8
      * DHE-RSA-AES128-CCM
      * ECDHE-ECDSA-ARIA128-GCM-SHA256
      * ECDHE-ARIA128-GCM-SHA256
      * DHE-DSS-ARIA128-GCM-SHA256
      * DHE-RSA-ARIA128-GCM-SHA256
      * ADH-AES128-GCM-SHA256
      * ECDHE-ECDSA-AES256-SHA384
      * ECDHE-RSA-AES256-SHA384
      * DHE-RSA-AES256-SHA256
      * DHE-DSS-AES256-SHA256
      * ECDHE-ECDSA-CAMELLIA256-SHA384
      * ECDHE-RSA-CAMELLIA256-SHA384
      * DHE-RSA-CAMELLIA256-SHA256
      * DHE-DSS-CAMELLIA256-SHA256
      * ADH-AES256-SHA256
      * ADH-CAMELLIA256-SHA256
      * ECDHE-ECDSA-AES128-SHA256
      * ECDHE-RSA-AES128-SHA256
      * DHE-RSA-AES128-SHA256
      * DHE-DSS-AES128-SHA256
      * ECDHE-ECDSA-CAMELLIA128-SHA256
      * ECDHE-RSA-CAMELLIA128-SHA256
      * DHE-RSA-CAMELLIA128-SHA256
      * DHE-DSS-CAMELLIA128-SHA256
      * ADH-AES128-SHA256
      * ADH-CAMELLIA128-SHA256
      * ECDHE-ECDSA-AES256-SHA
      * ECDHE-RSA-AES256-SHA
      * DHE-RSA-AES256-SHA
      * DHE-DSS-AES256-SHA
      * DHE-RSA-CAMELLIA256-SHA
      * DHE-DSS-CAMELLIA256-SHA
      * AECDH-AES256-SHA
      * ADH-AES256-SHA
      * ADH-CAMELLIA256-SHA
      * ECDHE-ECDSA-AES128-SHA
      * ECDHE-RSA-AES128-SHA
      * DHE-RSA-AES128-SHA
      * DHE-DSS-AES128-SHA
      * DHE-RSA-SEED-SHA
      * DHE-DSS-SEED-SHA
      * DHE-RSA-CAMELLIA128-SHA
      * DHE-DSS-CAMELLIA128-SHA
      * AECDH-AES128-SHA
      * ADH-AES128-SHA
      * ADH-SEED-SHA
      * ADH-CAMELLIA128-SHA
      * RSA-PSK-AES256-GCM-SHA384
      * DHE-PSK-AES256-GCM-SHA384
      * RSA-PSK-CHACHA20-POLY1305
      * DHE-PSK-CHACHA20-POLY1305
      * ECDHE-PSK-CHACHA20-POLY1305
      * DHE-PSK-AES256-CCM8
      * DHE-PSK-AES256-CCM
      * RSA-PSK-ARIA256-GCM-SHA384
      * DHE-PSK-ARIA256-GCM-SHA384
      * AES256-GCM-SHA384
      * AES256-CCM8
      * AES256-CCM
      * ARIA256-GCM-SHA384
      * PSK-AES256-GCM-SHA384
      * PSK-CHACHA20-POLY1305
      * PSK-AES256-CCM8
      * PSK-AES256-CCM
      * PSK-ARIA256-GCM-SHA384
      * RSA-PSK-AES128-GCM-SHA256
      * DHE-PSK-AES128-GCM-SHA256
      * DHE-PSK-AES128-CCM8
      * DHE-PSK-AES128-CCM
      * RSA-PSK-ARIA128-GCM-SHA256
      * DHE-PSK-ARIA128-GCM-SHA256
      * AES128-GCM-SHA256
      * AES128-CCM8
      * AES128-CCM
      * ARIA128-GCM-SHA256
      * PSK-AES128-GCM-SHA256
      * PSK-AES128-CCM8
      * PSK-AES128-CCM
      * PSK-ARIA128-GCM-SHA256
      * AES256-SHA256
      * CAMELLIA256-SHA256
      * AES128-SHA256
      * CAMELLIA128-SHA256
      * ECDHE-PSK-AES256-CBC-SHA384
      * ECDHE-PSK-AES256-CBC-SHA
      * SRP-DSS-AES-256-CBC-SHA
      * SRP-RSA-AES-256-CBC-SHA
      * SRP-AES-256-CBC-SHA
      * RSA-PSK-AES256-CBC-SHA384
      * DHE-PSK-AES256-CBC-SHA384
      * RSA-PSK-AES256-CBC-SHA
      * DHE-PSK-AES256-CBC-SHA
      * ECDHE-PSK-CAMELLIA256-SHA384
      * RSA-PSK-CAMELLIA256-SHA384
      * DHE-PSK-CAMELLIA256-SHA384
      * AES256-SHA
      * CAMELLIA256-SHA
      * PSK-AES256-CBC-SHA384
      * PSK-AES256-CBC-SHA
      * PSK-CAMELLIA256-SHA384
      * ECDHE-PSK-AES128-CBC-SHA256
      * ECDHE-PSK-AES128-CBC-SHA
      * SRP-DSS-AES-128-CBC-SHA
      * SRP-RSA-AES-128-CBC-SHA
      * SRP-AES-128-CBC-SHA
      * RSA-PSK-AES128-CBC-SHA256
      * DHE-PSK-AES128-CBC-SHA256
      * RSA-PSK-AES128-CBC-SHA
      * DHE-PSK-AES128-CBC-SHA
      * ECDHE-PSK-CAMELLIA128-SHA256
      * RSA-PSK-CAMELLIA128-SHA256
      * DHE-PSK-CAMELLIA128-SHA256
      * AES128-SHA
      * SEED-SHA
      * CAMELLIA128-SHA
      * IDEA-CBC-SHA
      * PSK-AES128-CBC-SHA256
      * PSK-AES128-CBC-SHA
      * PSK-CAMELLIA128-SHA256
      * ECDHE-ECDSA-NULL-SHA
      * ECDHE-RSA-NULL-SHA
      * AECDH-NULL-SHA
      * NULL-SHA256
      * ECDHE-PSK-NULL-SHA384
      * ECDHE-PSK-NULL-SHA256
      * ECDHE-PSK-NULL-SHA
      * RSA-PSK-NULL-SHA384
      * RSA-PSK-NULL-SHA256
      * DHE-PSK-NULL-SHA384
      * DHE-PSK-NULL-SHA256
      * RSA-PSK-NULL-SHA
      * DHE-PSK-NULL-SHA
      * NULL-SHA
      * NULL-MD5
      * PSK-NULL-SHA384
      * PSK-NULL-SHA256
      * PSK-NULL-SHA


* To be a fully supported configuration, all clients must support the following:
    * TLS v1.2 or v1.3
    * elliptic curve cryptography
    * TLS server name indication (SNI)

* Additionally, you must use TLS v1.2 or v1.3 in the following cases:
    * for making connections to the Kafka native and REST interfaces 
    * the browser that you use to access the {{site.data.keyword.messagehub}} dashboard must support TLS v1.2 or v1.3

   
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
