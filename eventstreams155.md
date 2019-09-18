---

copyright:
  years: 2015, 2019
lastupdated: "2019-09-18"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka, BYOK

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Bring Your Own Key (BYOK)
{: #byok}

You can use bring-your-own-key (BYOK) customer-managed encryption keys with IBM Key Protect.
{:shortdesc}


Encryption keys contain subsets of information, such as the metadata that helps you identify the key, and the _key material_ that's used to encrypt and decrypt data.


When you use {{site.data.keyword.keymanagementserviceshort}} to create keys, the service generates cryptographic key material on your behalf that's rooted in cloud-based hardware security modules (HSMs). But depending on your business requirements, you might need to generate key material from your internal solution, and then extend your on-premises key management infrastructure onto the cloud by importing keys into {{site.data.keyword.keymanagementserviceshort}}.

| Benefit | Description |
| --- | --- |
| Bring your own keys (BYOK) | You want to fully control and strengthen your key management practices by generating strong keys from your on-premises hardware security module (HSM). If you choose to export symmetric keys from your internal key management infrastructure, you can use {{site.data.keyword.keymanagementserviceshort}} to securely bring them to the cloud. 

Need a bit of scene setting on what it offers (should be able to grab some words from other services):

* Encryption for message data at REST controlled by a customer managed key.
* The customer can prevent any further access to the data by deleting or removing access to the key.
* Maybe something on the actual key usage e.g. the customers key is actually used to encrypt the disks encryption key, so removing the key prevents the service from retreiving the actual disk key - crypto shedding (should be able to get some words from the Key Protect service page)

Customers need to be aware that:

* Only supported on clusters provisioned after x on the Enterprise plan
* Enablement is disruptive and results in the deletion of all existing message data.
* If deploying for use in a PCI environment, it is recommended to enable this feature
* Deleting the key is non-recoverable

Rough outline of the enablement steps:

Based on Cloudant's approach to BYOK, our initial support will require that customers use support tickets to request BYOK related function. We will document the following steps as the process by which a customer enables BYOK for an {{site.data.keyword.messagehub}} instance:
1. Provision an instance of {{site.data.keyword.messagehub}}
2. Provision an instance of Key Protect
3. Grant the {{site.data.keyword.messagehub}} service instance access to the Key Protect service instance
4. Create or import a root key into the Key Protect instance. This is the root key that will be used to protect the data stored by the {{site.data.keyword.messagehub}} service instance.

5. Open a support ticket on {{site.data.keyword.messagehub}} containing the following information:
   * The IBM Cloud region of the Key Protect service instance
   * The crn of the root key in the Key Protect instance
   * The region of the {{site.data.keyword.messagehub}} service instance
   * The {{site.data.keyword.messagehub}} service instance ID
The response to the support ticket will confirm that BYOK is enabled.

Usage instructions:

    * If you remove access to the key, the service instance shuts down.
    If you then reenable access, the service instance is reenabled
    If you delete the key, the key is non-recoverable
    Activity Tracker events



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



