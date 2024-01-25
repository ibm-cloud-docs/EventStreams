---

copyright:
  years: 2015, 2023
lastupdated: "2023-07-24"

keywords: BYOK, encryption, customer-managed encryption, customer-managed key, access to data, rotating key, rotate key

subcollection: EventStreams

---

{{site.data.keyword.attribute-definition-list}}

# Managing encryption in {{site.data.keyword.messagehub}}
{: #managing_encryption}

By default, message payload data in {{site.data.keyword.messagehub_full}} is encrypted at rest by using a randomly generated key. Although this default encryption model provides at-rest security, you might need a higher level of control. For these use cases, {{site.data.keyword.messagehub}} supports customer-managed encryption with the following {{site.data.keyword.cloud}} key management services:

- {{site.data.keyword.keymanagementservicefull}} (Bring Your Own Key - BYOK) helps you provision encrypted keys for apps across {{site.data.keyword.cloud_notm}} services. As you manage the lifecycle of your keys, you benefit from knowing that your keys are secured by FIPS 140-2 Level three certified cloud-based hardware security modules (HSMs) that protect against the theft of information. For more information about using {{site.data.keyword.keymanagementserviceshort}}, see the [Getting Started tutorial](/docs/key-protect?topic=key-protect-getting-started-tutorial){: external}.
- {{site.data.keyword.hscrypto}} (Keep Your Own Key - KYOK) is a single-tenant, dedicated HSM that is controlled by you. The service is built on FIPS 140-2 Level 4-certified hardware, the highest offered by any cloud provider in the industry. For more information about using {{site.data.keyword.hscrypto}}, see the [Getting Started tutorial](/docs/hs-crypto?topic=hs-crypto-get-started){: external}.

These services allow the use of a customer-provided key to control encryption. By disabling or deleting this key, you can prevent any further access to the data that is stored by the service, because it is no longer possible to decrypt it.
{: shortdesc}

Consider to use customer-managed keys, if you require the following features:

- Encryption of data at rest controlled by your own key.
- Explicit control of the lifecycle of data that is stored at rest.
{: #considerations_keys notoc}

Customer-managed keys are available on the Enterprise plan and only on clusters that were created after October 2019.
{: note}

Deletion of the customer-managed key is unrecoverable and results in the loss of any data that is stored in your {{site.data.keyword.messagehub}} instance.
{: important}

## What is not covered by customer-managed encryption
{: #encryption_what}

If customer-managed encryption feature is selected, be aware that **only** message payload data is covered by this encryption. {{site.data.keyword.messagehub}} encrypts at rest other data that is related to the use of the service. However, although encrypted, non-message payload data **is not** encrypted with the customer-managed encryption. Examples are client metadata such as topic names, topic configuration data, schemas stored in the schema registry and metadata that is stored in relation to the configuration of the Enterprise instance. 

Therefore, do not use confidential information in such client metadata.
{: important}

## How customer-managed encryption works
{: #encryption_how}

{{site.data.keyword.messagehub}} uses a concept that is called envelope encryption to implement customer-managed keys. 

Envelope encryption is the practice of encrypting one encryption key with another encryption key. The key used to encrypt the actual data is known as a data encryption key (DEK). The DEK itself is never stored, but instead is wrapped by a second key that is known as the key encryption key (KEK) to create a wrapped DEK. 

To decrypt data, the wrapped DEK must first be unwrapped to get the DEK. This process is possible only by accessing the KEK, which in this case is your root key that is stored in either [{{site.data.keyword.keymanagementserviceshort}}](/docs/key-protect?topic=key-protect-about){: external} or [{{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-overview){: external}. 

You own the KEK, which you create as a root key in the {{site.data.keyword.hscrypto}} or {{site.data.keyword.keymanagementserviceshort}} service. The {{site.data.keyword.messagehub}} service never sees the root (KEK) key. Its storage, management, and use to wrap and unwrap the DEK is performed entirely within the key management service. If you disable or delete the key, the data can no longer be decrypted.

## Enabling a customer-managed key for {{site.data.keyword.messagehub}}
{: #enabling_encryption}

Complete the following steps to provision your {{site.data.keyword.messagehub}} instance to use a customer-managed key:

1. Provision an instance of [{{site.data.keyword.keymanagementserviceshort}}](/docs/key-protect?topic=key-protect-provision){: external} or [{{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-provision){: external}.
2. Create an authorization policy to allow the {{site.data.keyword.messagehub}} service to access the key management service instance as a Reader. For more information, see [Using authorizations to grant access between services](/docs/account?topic=account-serviceauth){: external}.
3. Create or import a root key into your key management service instance.
4. Retrieve the Cloud Resource Name (CRN) of the key by using the **View CRN** option in the key management service instance GUI.
5. Provision an instance of [{{site.data.keyword.messagehub}}](/docs/EventStreams?topic=EventStreams-getting-started). This feature is supported on the Enterprise plan only. 

If provisioning through {{site.data.keyword.Bluemix}} console, select a key management service instance and then select a root key from the instance.

If provisioning through CLI, use the following command: 

```bash
ibmcloud resource service-instance-create EVENT-STREAMS-INSTANCE-NAME messagehub ibm.message.hub.enterprise.3nodes.2tb REGION -p '{"kms_key_crn":"KMS_KEY_CRN"}'
```
{: codeblock}

If you want to update your existing {{site.data.keyword.messagehub}} instance to use a customer-managed key, open a [support ticket](/docs/get-support?topic=get-support-open-case){: external} on {{site.data.keyword.messagehub}} that contains the following information:

   - The CRN of the root key that you want to use in your key management service instance.
   - The CRN of your {{site.data.keyword.messagehub}} service instance.

   You find this CRN by copying and pasting the full {{site.data.keyword.Bluemix}} console URL after you click the {{site.data.keyword.messagehub}} service in the console. 
   Alternatively, paste in the output from the following CLI command:

   ```bash
   ibmcloud resource service-instance NAME
   ```
   {: codeblock}

   The {{site.data.keyword.messagehub}} Operations team responds to your support ticket to confirm that your instance of {{site.data.keyword.Bluemix}} is now using a customer-managed key. Expect the enablement to be completed in one business day.

This operation is destructive and results in the loss of all message and topic definitions. For more information, see [deciding to enable customer-managed keys](/docs/EventStreams?topic=EventStreams-managing_encryption#considerations_keys).
{: important}

## Using a customer-managed key
{: #using_encryption}

After a customer-managed key is enabled, the cluster operates as normal, but with the following additional capabilities.

### Preventing access to data
{: #preventing_access}

To temporarily prevent access, disable your root key. As a consequence, {{site.data.keyword.messagehub}} can no longer access the data because it can no longer access the key. 

To remove access permanently, delete the key. However, you must take extreme caution because this operation is non-recoverable. You lose access to any data that is stored in your {{site.data.keyword.messagehub}} instance. It is not possible to recover this data.

In both cases, the {{site.data.keyword.messagehub}} instance shuts down and no longer accepts or processes connections. An activity tracker event is generated to report the action. For more information, see [{{site.data.keyword.cloudaccesstrailshort}} events](/docs/EventStreams?topic=EventStreams-at_events#events).

The authorization is to be left in place between your {{site.data.keyword.messagehub}} and the key management service instance at all times. While removing this authorization prevents {{site.data.keyword.messagehub}} from future access to your data, already in-use data continues to be available for a period of time.
{: note}

You are charged for your instance of {{site.data.keyword.messagehub}} until you deprovision it using the {{site.data.keyword.Bluemix}} console or CLI. These charges are still applied even if you chose to prevent access to your data.
{: important}

### Restoring access to data
{: #restoring_access}

Access can be restored only if the key was not deleted. To restore access, re-enable your root key. After a short period of initialization, your {{site.data.keyword.messagehub}} instance is restarted and starts accepting connections again. All data is retained, subject to the normal retention limits configured in your instance.

An activity tracker event is generated to report the action. For more information, see [{{site.data.keyword.cloudaccesstrailshort}} events](/docs/EventStreams?topic=EventStreams-at_events#events).

### Rotating the key
{: #rotating_key}

{{site.data.keyword.keymanagementserviceshort}} and {{site.data.keyword.hscrypto}} support the rotation of root keys, either on demand or on a schedule. When rotating the key, {{site.data.keyword.messagehub}} adopts the new key by rewrapping the DEK as described previously in [how customer-managed encryption works](/docs/EventStreams?topic=EventStreams-managing_encryption#encryption_how). 

An activity tracker event is generated to report the action. For more information, see [{{site.data.keyword.cloudaccesstrailshort}} events](/docs/EventStreams?topic=EventStreams-at_events#events). 

## Disabling customer-managed encryption
{: #stop_customer_encryption}

After you enable customer-managed encryption, it is not possible to disable it. Instead, you must delete the service instance and create a new instance.
