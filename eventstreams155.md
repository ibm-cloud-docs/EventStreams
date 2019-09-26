---

copyright:
  years: 2015, 2019
lastupdated: "2019-09-26d"

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

By default, message payload data in {{site.data.keyword.messagehub}} is encrypted at rest using a randomly generated key. Although this default encryption model provides at-rest security, some customers need a higher level of control. For these use cases, {{site.data.keyword.messagehub}} supports customer-managed encryption (often known as Bring Your Own Key or BYOK), which allows a customer-provided key to be used to control the encryption. By deleting or revoking access to this key, you can prevent any further access to the data stored by the service, because it is no longer possible to decrypt.
{:shortdesc}


Consider using customer-managed keys if you require the following features:
- Encryption of data at rest controlled by your own key
- Explicit control of the lifecycle of data stored at rest achieved by deleting or removing access to the key. For example, crypto-shredding
- Use of your {{site.data.keyword.messagehub}} instance in a PCI environment

Be aware of the following information when deciding to enable customer-managed keys: 
- This feature is available on the Enterprise plan only
- Enablement is disruptive and results in the loss of any existing message data and topic definitions
- Deletion of the customer-managed key is non-recoverable.

## How customer-managed encryption works
{: #encryption_how}

{{site.data.keyword.messagehub}} uses a concept called envelope encryption to implement customer-managed keys. Envelope encryption is a multi-layered practice. The key used to encrypt the actual data is known as a Data Encryption Key (DEK). The DEK itself is never stored, but instead is encrypted using a second key known as the Key Encryption Key (KEK) to create a 'wrapped DEK'. To decrypt data, the wrapped DEK must first be decrypted to get the DEK. This process is possible only by accessing the KEK, which in this case is your root key stored in {{site.data.keyword.keymanagementserviceshort}}. 

You own the KEK. You create a root key in the {{site.data.keyword.keymanagementserviceshort}} service. The root key is the KEK. The {{site.data.keyword.messagehub}} service never sees the root (KEK) key. {{site.data.keyword.messagehub}} requests that the {{site.data.keyword.keymanagementserviceshort}} service wraps or unwraps a DEK with the customer root key. If you revoke access to this key, or delete the key the data can no longer be decrypted.

Keys are secured in {{site.data.keyword.keymanagementserviceshort}} using FIPS 140-2 Level 3 certified cloud-based hardware security modules (HSMs) that protect against the theft of information. Data is stored in {{site.data.keyword.messagehub}} using Advanced Encryption Standard (AES-256).

## Enabling a customer-managed key for {{site.data.keyword.messagehub}}
{: #enabling_encryption}

This operation is destructive and results in the loss of all message and topic definitions. See notes above.
{:important}

Complete the following steps to reconfigure your {{site.data.keyword.messagehub}} instance to use a customer-managed key. 

Create a root key in an instance of the {{site.data.keyword.keymanagementservicefull}} service in your account and then raise a support ticket to have the storage within your {{site.data.keyword.messagehub}} instance re-created using this key. The supplied key is used to perform envelope encryption.

1. Provision an instance of [{{site.data.keyword.messagehub_full}}](/docs/services/EventStreams?topic=eventstreams-getting_started). This feature is supported only on the Enterprise plan.
2. Provision an instance of [{{site.data.keyword.keymanagementservicefull}} ! [External link icon](../../icons/launch-glyph.svg "External link icon")]](/docs/services/key-protect?topic=key-protect-provision).
3. Create an authorization to allow the {{site.data.keyword.messagehub}} instance to access the {{site.data.keyword.keymanagementserviceshort}} instance. For more information, see [Using authorizations to grant access between services ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/iam?topic=iam-serviceauth){:new_window}.
4. Create or import a root key in to {{site.data.keyword.keymanagementserviceshort}}. For more information, see [Creating root keys ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/services/key-protect?topic=key-protect-create-root-keys){:new_window} or [Importing root keys ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/services/key-protect?topic=key-protect-import-root-keys){:new_window}.
5. Retrieve the CRN (Cloud Resource Name) of the key using the 'View CRN' option in the {{site.data.keyword.keymanagementserviceshort}} Management portal.
6. Open a [support ticket ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/get-support?topic=get-support-getting-customer-support#using-avatar){:new_window} on {{site.data.keyword.messagehub}} that contains the following information:
   * The CRN of the root key created above
   * The CRN of your {{site.data.keyword.messagehub}} instance
   You can provide this ID by pasting the full {{site.data.keyword.Bluemix}} console URL after clicking on the {{site.data.keyword.messagehub}} service, or by pasting the output from the following CLI command:

   ```ibmcloud resource service-instance NAME```

   The response to the support ticket confirms that your encryption is now enabled using your key and that the cluster is ready for use.

## Using a customer-managed key
{: #using_encryption}

When enabled, the cluster operates as normal, but with the following additional capabilities:

### Preventing access to data

To temporarily prevent access, remove the Authorization created between your {{site.data.keyword.messagehub}} and {{site.data.keyword.keymanagementserviceshort}} instances. {{site.data.keyword.messagehub}} can no longer access the data because it can no longer access the key. 

To remove access permanently you can delete the key. However, extreme caution must be taken because this operation is non-recoverable. You will lose all access to message data.

In both cases the {{site.data.keyword.messagehub}} instance shuts down and no longer accepts or processes connections. An activity tracker event is generated to report the action. For more information, see [{{site.data.keyword.cloudaccesstrailshort}} events](/docs/services/EventStreams?topic=eventstreams-at_events).

***Important:*** As long as the instance exists charges will continue.

### Restoring access to data

Access can be restored only if the key was not deleted. To restore access, re-create the Authorization between your {{site.data.keyword.messagehub}} and {{site.data.keyword.keymanagementserviceshort}} instances. After a short period of initialization your {{site.data.keyword.messagehub}} instance is restarted and starts accepting connections. All data is retained, subject to the normal retention limits configured in your instance.

An activity tracker event is generated to report the action. For more information, see [{{site.data.keyword.cloudaccesstrailshort}} events](/docs/services/EventStreams?topic=eventstreams-at_events).

### Rotating the key

{{site.data.keyword.keymanagementserviceshort}} supports the rotation of root keys, either on demand or on a schedule. When this occurs, {{site.data.keyword.messagehub}} adopts the new key by re-wrapping the DEK <link to info on envelope encryption above>. An activity tracker event is generated to report the action. For more information, see [{{site.data.keyword.cloudaccesstrailshort}} events](/docs/services/EventStreams?topic=eventstreams-at_events).


<!--
-------
You can use bring-your-own-key (BYOK) customer-managed encryption keys using [{{site.data.keyword.keymanagementservicefull}} 
 ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/services/key-protect?topic=key-protect-about). The service helps you provision encrypted keys for apps across {{site.data.keyword.Bluemix}} services. 
Encryption keys contain subsets of information, such as the metadata that helps you identify the key, and the _key material_ that's used to encrypt and decrypt data. When you use {{site.data.keyword.keymanagementserviceshort}} to create keys, the service generates cryptographic key material on your behalf that's rooted in cloud-based hardware security modules (HSMs). But depending on your business requirements, you might need to generate key material from your internal solution, and then extend your on-premises key management infrastructure onto the cloud by importing keys into {{site.data.keyword.keymanagementserviceshort}}.


BYOK offers the following benefits:

* Encryption for message data at rest is controlled by a customer-managed key.
* You can prevent any further access to the data by deleting or removing access to the key.
* Actual key usage. For example, the customer's key is actually used to encrypt the disk's encryption key, so removing the customer key prevents the service from retrieving the actual disk key. For more information about crypto-shedding, ***see  - crypto shedding (should be able to get some words from the {{site.data.keyword.keymanagementserviceshort}} service page)***



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

-->




