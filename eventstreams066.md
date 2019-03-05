---

copyright:
  years: 2015, 2019
lastupdated: "2018-05-25"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# How to connect and authenticate
{: #rest_connect}

<!-- info moved to eventstreams025.md because of doc app changes -->

** The Kafka REST API is available as part of the Standard plan only.**
<br/>

To connect to {{site.data.keyword.messagehub}}, the Kafka REST API uses the <code>api_key</code> and <code>kafka_rest_url</code>
credentials from the [VCAP_SERVICES environment variable](/docs/services/EventStreams?topic=eventstreams-connecting).

To authenticate with the {{site.data.keyword.messagehub}} Kafka REST API, you must specify the <code>api_key</code> in the X-Auth-Token header of your requests.
