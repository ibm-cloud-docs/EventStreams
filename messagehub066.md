---

copyright:
  years: 2015, 2017
lastupdated: "2016-11-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# How to connect and authenticate
{: #rest_connect}

To connect to {{site.data.keyword.messagehub}}, the Kafka REST API uses the ```api_key``` and ```kafka_rest_url```
credentials from the [VCAP_SERVICES environment variable](/docs/services/MessageHub/messagehub050.html#messagehub071).

To authenticate with the {{site.data.keyword.messagehub}} Kafka REST API, you must specify the ```api_key``` in the X-Auth-Token header of your requests.
