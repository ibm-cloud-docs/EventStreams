---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


#Data security and privacy
{: #data_security}


{{site.data.keyword.IBM}} uses the following methods to help ensure the security and
privacy of your data:
{:shortdesc}

## Cryptographic protocols
{: #cryptographic notoc}


*  Connections to the Kafka native and REST interfaces must be
   made using TLS 1.2.
*  Connections are restricted to the following strong cipher
   suites:

      * ECDHE-RSA-AES128-GCM-SHA256
      * ECDHE-RSA-AES256-GCM-SHA384
      * DHE-RSA-AES128-GCM-SHA256
      * kEDH+AESGCM
      * ECDHE-RSA-AES128-SHA256
      * ECDHE-RSA-AES256-SHA384
      * DHE-RSA-AES128-SHA256
      * DHE-RSA-AES256-SHA256



*  To access the {{site.data.keyword.messagehub}} dashboard, you must use a browser
   that supports TLS 1.2.
   
## Encryption of message payloads, topic names, and consumer groups
{: #encryption_payloads notoc}

Message data is encrypted for transmission between {{site.data.keyword.messagehub}}
and clients as a result of TLS. {{site.data.keyword.messagehub}} stores message data
at rest and message logs on encrypted disks.

Topic names and consumer groups are encrypted for transmission between 
{{site.data.keyword.messagehub}} and clients as a result of TLS. However, 
{{site.data.keyword.messagehub}} does not encrypt these values at rest. Therefore, you are not recommended to use confidential information in your topic names.



