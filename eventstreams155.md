---

copyright:
  years: 2015, 2019
lastupdated: "2019-09-25b"

keywords: IBM {{site.data.keyword.messagehub}}, Kafka as a service, managed Apache Kafka, BYOK

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}


# Managing encryption
{: #managing_encryption}

Data in {{site.data.keyword.messagehub}} is encrypted at REST using a randomly generated key. Although this default encryption model provides at-rest security, some workloads need a higher level of control. For these use cases, {{site.data.keyword.messagehub}} supports customer-managed encryption (often known as Bring Your Own Key or BYOK), which allows a customer-provided key to be used to control the encryption. By revoking access to or deleting this key, customers can prevent any further access to the data stored by the service, because it will no longer be possible to decrypt.

Consider using customer-managed Keys if you require:
- Encryption of data at rest controlled by your own key
- Explicit control of the lifecycle of data stored at rest by deleting or removing access to the key for example, crypto-shredding
- Using your {{site.data.keyword.messagehub}} instance within a PCI environment

Be aware of the following information when deciding to enable customer-managed keys: 
- This feature is available on the Enterprise plan only
- Enablement is disruptive and results in the loss of any existing message data and topic definitions
- Deletion of the customer-managed key is non-recoverable.

## How it works

A root key must be created within the {{site.data.keyword.keymanagementserviceshort}} service and a support ticket raised instructing {{site.data.keyword.messagehub}} to re-create its storage using this key. The supplied key is used to perform envelope encryption. Envelope encryption is a multi-layered practise. The key used to encrypt the actual data is known as a data encryption key (DEK), the DEK itself is never stored, it instead is encrypted using a second key known as the Key Encryption Key (KEK) to create a 'wrapped DEK'. In order to un-encrypt data, the wrapped DEK must first be un-encrypted to get the DEK. This process is only possible by accessing the KEK, which in this case is the customer's root key stored in {{site.data.keyword.keymanagementserviceshort}}. If the customer revokes access to this key, or deletes the key the data can no longer be un-encrypted.

Keys are secured in {{site.data.keyword.keymanagementserviceshort}} using FIPS 140-2 Level 3 certified cloud-based hardware security modules (HSMs) that protect against the theft of information. Data is stored in {{site.data.keyword.messagehub}} using Advanced Encryption Standard (AES-256)

## How to enable

Complete the following steps to reconfigure your {{site.data.keyword.messagehub}} instance to use a customer-managed key. 

Note, this operation is destructive and results in the loss of all message and topic definitions. See notes above.
{:important}


* Provision an instance of {{site.data.keyword.messagehub}}. Note, this feature is only supported on the Enterprise plan.
* Provision an instance of {{site.data.keyword.keymanagementserviceshort}}
* Create an 'Authorization' to allow the {{site.data.keyword.messagehub}} instance to access the {{site.data.keyword.keymanagementserviceshort}} instance [add instructions or link to cloud docs]
* Create or import a root key in to {{site.data.keyword.keymanagementserviceshort}} [show how or link to KP instructions for this step]
* Retrieve the CRN (Cloud Resource Name) of the key using the 'View CRN' option in the {{site.data.keyword.keymanagementserviceshort}} Management portal
* Open a support ticket on {{site.data.keyword.messagehub}} containing the following information [include a link to the support system and the field ti fill in e.g. sev, team name]
   *The CRN of the root key created above
   *The CRN of your {{site.data.keyword.messagehub}} instance
You can provide this ID by pasting the full IBM Cloud console URL after clicking on the service, or by pasting the output from the following CLI command:
ibmcloud resource service-instance NAME

The response to the support ticket will confirm that your encryption is now enabled using your key and that the cluster is ready for use.

## Usage notes

When enabled, the cluster operates as normal, but with the following additional capabilities:

### Prevent access to data

To temporarily prevent access, remove the Authorization created between your {{site.data.keyword.messagehub}} and {{site.data.keyword.keymanagementserviceshort}} instances. {{site.data.keyword.messagehub}} will no longer be able to access the data because it can no longer access the key. 

To remove access permanently the key can be deleted. However, extreme caution must be taken because this operation is non-recoverable. 

In both cases the {{site.data.keyword.messagehub}} instance will shut down and no longer accept or process connections. An activity tracker event is generated to report the action. For more information, see [{{site.data.keyword.cloudaccesstrailshort}} events](/docs/services/EventStreams?topic=eventstreams-at_events).

Please be aware: While the instance exists charges will continue.

### Restore access to data

Access can be restored only if the key was not deleted. To restore access, re-create the Authorization between your {{site.data.keyword.messagehub}} and {{site.data.keyword.keymanagementserviceshort}} instances. After a short period of initialization your {{site.data.keyword.messagehub}} instance will be restarted and start accepting connections. All data will have been retained, subject to the normal retention limits configured in your instance.

An activity tracker event is generated to report the action. For more information, see [{{site.data.keyword.cloudaccesstrailshort}} events](/docs/services/EventStreams?topic=eventstreams-at_events).

### Rotate the key

{{site.data.keyword.keymanagementserviceshort}} supports the rotation of root keys, either on demand or on a schedule. When this occurs {{site.data.keyword.messagehub}} adopts the new key by re-wrapping the DEK <link to info on envelope encryption above>. An activity tracker event is generated to report the action. For more information, see [{{site.data.keyword.cloudaccesstrailshort}} events](/docs/services/EventStreams?topic=eventstreams-at_events).


TODO
- Will need to add the three new events above to the Activity Tracker page (info for these will follow shortly - details still being confirmed)
- Update the table on the Plan page to include customer-managed Encryption (BYOK) capable?








-------
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
* Actual key usage. For example, the customer's key is actually used to encrypt the disk's encryption key, so removing the customer key prevents the service from retrieving the actual disk key. For more information about crypto-shedding, ***see  - crypto shedding (should be able to get some words from the {{site.data.keyword.keymanagementserviceshort}} service page)***


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






