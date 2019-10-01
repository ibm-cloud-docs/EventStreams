---

copyright:
  years: 2015, 2019
lastupdated: "2019-10-01"

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

By default, message payload data in {{site.data.keyword.messagehub}} is encrypted at rest using a randomly generated key. Although this default encryption model provides at-rest security, you might need a higher level of control. For these use cases, {{site.data.keyword.messagehub}} supports customer-managed encryption (often known as Bring Your Own Key or BYOK), which allows the use of a customer-provided key to control encryption. By deleting or revoking access to this key, you can prevent any further access to the data stored by the service, because it is no longer possible to decrypt it.
{:shortdesc}

{: #considerations_keys notoc}
Consider using customer-managed keys if you require the following features:
- Encryption of data at rest controlled by your own key
- Explicit control of the lifecycle of data stored at rest

Be aware of the following information when deciding to enable customer-managed keys: 
- This feature is available on the Enterprise plan only
- Enablement is disruptive and results in the loss of any existing message data and topic definitions

Deletion of the customer-managed key is non-recoverable and will result in the loss of any data stored in your {{site.data.keyword.messagehub}} instance
{:important}

## How customer-managed encryption works
{: #encryption_how}

{{site.data.keyword.messagehub}} uses a concept called envelope encryption to implement customer-managed keys. Envelope encryption is the practice of encrypting one encryption key with another encryption key. The key used to encrypt the actual data is known as a data encryption key (DEK). The DEK itself is never stored, but instead is wrapped by a second key known as the key encryption key (KEK) to create a wrapped DEK. To decrypt data, the wrapped DEK must first be unwrapped to get the DEK. This process is possible only by accessing the KEK, which in this case is your root key stored in [{{site.data.keyword.keymanagementservicefull}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/services/key-protect?topic=key-protect-about){:new_window}. 

You own the KEK, which you create as a root key in the {{site.data.keyword.keymanagementserviceshort}} service. The {{site.data.keyword.messagehub}} service never sees the root (KEK) key. Its storage, management, and use to wrap and unwrap the DEK is performed entirely within the {{site.data.keyword.keymanagementserviceshort}} service. If you revoke access to this key or delete the key, the data can no longer be decrypted.

Keys are secured in {{site.data.keyword.keymanagementserviceshort}} using FIPS 140-2 Level 3 certified cloud-based hardware security modules (HSMs) that protect against the theft of information. Data is stored in {{site.data.keyword.messagehub}} using Advanced Encryption Standard (AES-256).

You can find out more about using {{site.data.keyword.keymanagementserviceshort}} in the [Getting Started tutorial ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/services/key-protect?topic=key-protect-getting-started-tutorial){:new_window}.

## Enabling a customer-managed key for {{site.data.keyword.messagehub}}
{: #enabling_encryption}

This operation is destructive and results in the loss of all message and topic definitions. For more information, see [deciding to enable customer-managed keys](/docs/services/EventStreams?topic=eventstreams-managing_encryption#considerations_keys).
{:important}

Complete the following steps to reconfigure your {{site.data.keyword.messagehub}} instance to use a customer-managed key:

1. Provision an instance of [{{site.data.keyword.messagehub_full}}](/docs/services/EventStreams?topic=eventstreams-getting_started). This feature is supported on the Enterprise plan only.
2. Provision an instance of [{{site.data.keyword.keymanagementservicefull}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/services/key-protect?topic=key-protect-provision).
3. Create an authorization to allow the {{site.data.keyword.messagehub}} instance to access the {{site.data.keyword.keymanagementserviceshort}} instance. For more information, see [Using authorizations to grant access between services ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/iam?topic=iam-serviceauth){:new_window}.
4. Create or import a root key into {{site.data.keyword.keymanagementserviceshort}}. For more information, see [Creating root keys ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/services/key-protect?topic=key-protect-create-root-keys){:new_window} or [Importing root keys ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/services/key-protect?topic=key-protect-import-root-keys){:new_window}.
5. Retrieve the Cloud Resource Name (CRN) of the key using the **View CRN** option in the {{site.data.keyword.keymanagementserviceshort}} GUI.
6. Open a [support ticket ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/get-support?topic=get-support-getting-customer-support#using-avatar){:new_window} on {{site.data.keyword.messagehub}} that contains the following information:
   * The CRN of the root key that you want to use in your instance of the {{site.data.keyword.keymanagementserviceshort}} service 
   * The CRN of your {{site.data.keyword.messagehub}} service instance
   <br/>
   You can find this CRN by copying and pasting the full {{site.data.keyword.Bluemix}} console URL after clicking the {{site.data.keyword.messagehub}} service in the console. 
   Alternatively, paste in the output from the following CLI command:

      ```
      ibmcloud resource service-instance NAME
      ```
      {: codeblock}

   The {{site.data.keyword.messagehub}} Operations team will respond to your support ticket to confirm that your instance of {{site.data.keyword.Bluemix}} is now using a customer-managed key. Expect the enablement to be completed in one business day.

## Using a customer-managed key
{: #using_encryption}

After a customer-managed key is enabled, the cluster operates as normal, but with the following additional capabilities:

### Preventing access to data

To temporarily prevent access, remove the authorization created between your {{site.data.keyword.messagehub}} and {{site.data.keyword.keymanagementserviceshort}} instances. As a consequence, {{site.data.keyword.messagehub}} can no longer access the data because it can no longer access the key. 

To remove access permanently you can delete the key. However, you must take extreme caution because this operation is non-recoverable. You will lose access to any data stored in your {{site.data.keyword.messagehub}} instance. There is no way to recover this data.

In both cases the {{site.data.keyword.messagehub}} instance shuts down and no longer accepts or processes connections. An activity tracker event is generated to report the action. For more information, see [{{site.data.keyword.cloudaccesstrailshort}} events](/docs/services/EventStreams?topic=eventstreams-at_events).

***Important:*** You are charged for your instance of {{site.data.keyword.messagehub}} until you deprovision it using the {{site.data.keyword.Bluemix}} console or CLI. These charges are still applied even if you have chosen to prevent access to your data by removing authorization to your key or by deleting your key.

### Restoring access to data

Access can be restored only if the key was not deleted. To restore access, re-create the authorization between your {{site.data.keyword.messagehub}} and {{site.data.keyword.keymanagementserviceshort}} instances. After a short period of initialization your {{site.data.keyword.messagehub}} instance is restarted and starts accepting connections again. All data is retained, subject to the normal retention limits configured in your instance.

An activity tracker event is generated to report the action. For more information, see [{{site.data.keyword.cloudaccesstrailshort}} events](/docs/services/EventStreams?topic=eventstreams-at_events).

### Rotating the key

{{site.data.keyword.keymanagementserviceshort}} supports the rotation of root keys, either on demand or on a schedule. When this occurs, {{site.data.keyword.messagehub}} adopts the new key by rewrapping the DEK as described previously in [how customer-managed encryption works](/docs/services/EventStreams?topic=eventstreams-managing_encryption#encryption_how). 

An activity tracker event is generated to report the action. For more information, see [{{site.data.keyword.cloudaccesstrailshort}} events](/docs/services/EventStreams?topic=eventstreams-at_events). 

## Disabling customer-managed encryption
{: #stop_customer_encryption}

After enabling customer-managed encryption, it is not possible to disable it. Instead, you must delete the service instance and create a new instance.

<!--If you no longer want to use customer-managed encryption for an {{site.data.keyword.messagehub}} instance, complete the following steps:
1. Delete your customer-managed key.
2. Provision a new instance of {{site.data.keyword.messagehub}}.-->







