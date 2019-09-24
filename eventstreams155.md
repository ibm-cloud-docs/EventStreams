---

copyright:
  years: 2015, 2019
lastupdated: "2019-09-24c"

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

You can use bring-your-own-key (BYOK) customer-managed encryption keys using [{{site.data.keyword.keymanagementservicefull}} 
 ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/services/key-protect?topic=key-protect-about). The service helps you provision encrypted keys for apps across {{site.data.keyword.Bluemix}} services. 
Encryption keys contain subsets of information, such as the metadata that helps you identify the key, and the _key material_ that's used to encrypt and decrypt data. When you use {{site.data.keyword.keymanagementserviceshort}} to create keys, the service generates cryptographic key material on your behalf that's rooted in cloud-based hardware security modules (HSMs). But depending on your business requirements, you might need to generate key material from your internal solution, and then extend your on-premises key management infrastructure onto the cloud by importing keys into {{site.data.keyword.keymanagementserviceshort}}.

Use BYOK if you want to fully control and strengthen your key management practices by generating strong keys from your on-premises hardware security module (HSM). If you choose to export symmetric keys from your internal key management infrastructure, you can use {{site.data.keyword.keymanagementserviceshort}} to securely bring them to the cloud. 

By managing your own keys, you can better protect your data and improve compliance. We understand that customers in regulated industries, such as financial services and healthcare, value peace of mind. That's why we’re committed to providing you with more control over how you manage your data and security on IBM Cloud Databases through integrations with the {{site.data.keyword.keymanagementserviceshort}}.

*** 
By managing your own keys, you can better protect your data and improve compliance. We understand that customers in regulated industries, such as financial services and healthcare, value peace of mind. That's why we’re committed to providing you with more control over how you manage your data and security on {{site.data.keyword.Bluemix}} Databases through integrations with the {{site.data.keyword.keymanagementserviceshort}}.

Simply bring your own disk encryption key to the IBM Cloud—AKA Bring Your Own Key (BYOK)! 

Encryption with Bring Your Own Key (BYOK) enables businesses to retain control over access to their encrypted data at rest. When companies have concerns about how their data is shared, encryption with BYOK is one way to mitigate the risk of unintentional or unknown exposure.***
{:shortdesc}

BYOK offers the following benefits:

* Encryption for message data at rest is controlled by a customer-managed key.
* You can prevent any further access to the data by deleting or removing access to the key.
* Actual key usage. For example, the customer's key is actually used to encrypt the disk's encryption key, so removing the customer key prevents the service from retrieving the actual disk key. For more information about crypto-shedding, ***see  - crypto shedding (should be able to get some words from the Key Protect service page)***


## Using BYOK
{: #byok_using}

Be aware of the following information before deciding to implement BYOK:

* BYOK is supported only on clusters provisioned after ***x*** on the {{site.data.keyword.messagehub}} Enterprise plan.
* Note that enablement is disruptive and results in the deletion of all your existing message data.
* If you are deploying {{site.data.keyword.messagehub}} for use in a PCI environment, you are recommended to enable BYOK.
* If you delete the key, the key is non-recoverable.
* If you remove access to the key, the service instance shuts down.
* If you then reenable access to the key, the service instance is reenabled.
* BYOK logs events in {{site.data.keyword.cloudaccesstrailshort}}. For more information, see [{{site.data.keyword.cloudaccesstrailshort}} events](/docs/services/EventStreams?topic=eventstreams-at_events).

## Enabling BYOK for {{site.data.keyword.messagehub}}
{: #byok_steps}

If you want to enable BYOK-related function for an {{site.data.keyword.messagehub}} instance, complete the following steps: 

1. Provision an instance of 
[{{site.data.keyword.messagehub}}](/docs/services/EventStreams?topic=eventstreams-getting_started).
2. Provision an instance of 
[{{site.data.keyword.keymanagementserviceshort}}](/docs/services/key-protect?topic=key-protect-provision).
3. Grant the {{site.data.keyword.messagehub}} service instance access to the {{site.data.keyword.keymanagementserviceshort}} service instance.
4. Create or import a root key into the {{site.data.keyword.keymanagementserviceshort}} instance. This is the root key that will be used to protect the data stored by the {{site.data.keyword.messagehub}} service instance.
5. Open a support ticket on {{site.data.keyword.messagehub}} that contains the following information:
    * The {{site.data.keyword.Bluemix}} region of the {{site.data.keyword.keymanagementserviceshort}} service instance
    * The CRN of the root key in the {{site.data.keyword.keymanagementserviceshort}} instance
    * The region of the {{site.data.keyword.messagehub}} service instance
    * The {{site.data.keyword.messagehub}} service instance ID

You'll then receive confirmation via the support ticket that BYOK is enabled.





