---

copyright:
  years: 2015, 2019
lastupdated: "2019-09-19"

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

You can use bring-your-own-key (BYOK) customer-managed encryption keys with IBM Key Protect. Use BYOK if you want to fully control and strengthen your key management practices by generating strong keys from your on-premises hardware security module (HSM). If you choose to export symmetric keys from your internal key management infrastructure, you can use {{site.data.keyword.keymanagementserviceshort}} to securely bring them to the cloud. 
{:shortdesc}


Encryption keys contain subsets of information, such as the metadata that helps you identify the key, and the _key material_ that's used to encrypt and decrypt data.


When you use {{site.data.keyword.keymanagementserviceshort}} to create keys, the service generates cryptographic key material on your behalf that's rooted in cloud-based hardware security modules (HSMs). But depending on your business requirements, you might need to generate key material from your internal solution, and then extend your on-premises key management infrastructure onto the cloud by importing keys into {{site.data.keyword.keymanagementserviceshort}}.

Need a bit of scene setting on what it offers (should be able to grab some words from other services):

* Encryption for message data at REST controlled by a customer managed key.
* The customer can prevent any further access to the data by deleting or removing access to the key.
* Maybe something on the actual key usage e.g. the customers key is actually used to encrypt the disks encryption key, so removing the key prevents the service from retrieving the actual disk key - crypto shedding (should be able to get some words from the Key Protect service page)

Customers need to be aware that:

* Only supported on clusters provisioned after x on the Enterprise plan
* Enablement is disruptive and results in the deletion of all existing message data.
* If deploying for use in a PCI environment, it is recommended to enable this feature
* Deleting the key is non-recoverable

## Enabling BYOK for {{site.data.keyword.messagehub}}
{: #byok_steps}

To request BYOK-related function for an {{site.data.keyword.messagehub}} instance, complete the following steps: 

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

## Using BYOK 
{: #byok_using}

    * If you remove access to the key, the service instance shuts down.
    * If you then reenable access, the service instance is reenabled
    * If you delete the key, the key is non-recoverable
    * Activity Tracker events

* To be a fully supported configuration, all clients must support the following:
    * TLS v1.2
    * elliptic curve cryptography
    * TLS server name indication (SNI)
