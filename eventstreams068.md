---

copyright:
  years: 2015, 2019
lastupdated: "2019-07-23"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

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
{: #cryptographic notoc}

* Connections are restricted to the following strong cipher suites:

      * ECDHE-RSA-AES128-GCM-SHA256
      * ECDHE-RSA-AES256-GCM-SHA384
      * ECDHE-RSA-AES128-SHA256
      * ECDHE-RSA-AES256-SHA384
      * ECDHE-RSA-AES256-SHA384

* To be a fully supported configuration, all clients      must support TLSv1.2, elliptic curve cryptography,     and TLS server name indication (SNI).

* You must use TLS v1.2 in the following cases:
    * to access the {{site.data.keyword.messagehub}} dashboard, your browser that supports TLS v1.2
    * to make connections to the Kafka native and REST interfaces 
   
## Encryption of message payloads, topic names, and consumer groups
{: #encryption_payloads notoc}

Message data is encrypted for transmission between {{site.data.keyword.messagehub}}
and clients as a result of TLS. {{site.data.keyword.messagehub}} stores message data
at rest and message logs on encrypted disks.

Topic names and consumer groups are encrypted for transmission between 
{{site.data.keyword.messagehub}} and clients as a result of TLS. However, 
{{site.data.keyword.messagehub}} does not encrypt these values at rest. Therefore, you are not recommended to use confidential information in your topic names.



