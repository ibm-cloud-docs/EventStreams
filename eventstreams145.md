---

copyright:
  years: 2015, 2019
lastupdated: "2019-05-02"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Managing service endpoints using the Enterprise plan
{: #manage_endpoints}

By using an internal endpoint, {{site.data.keyword.Bluemix_short}} Service Endpoint enables the connection to the {{site.data.keyword.messagehub}} service through the internal IBM Cloud network.
{:shortdesc}

You can now add an internal endpoint to access and manage your {{site.data.keyword.messagehub}} service instance.

## Prerequisites
{: #prereqs notoc}

Ensure that you meet the following requirements:
- Create your service instance by using the Enterprise plan. For more information, see [Choosing your plan](/docs/services/EventStreams?topic=eventstreams-plan_choose).
- Create your service instance in the {{site.data.keyword.Bluemix_short}} United Kingdom (London) or Germany (Frankfurt) regions.
- Enable [Virtual Route Forwarding (VRF)](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) for your {{site.data.keyword.Bluemix_short}} account.


To add an internal endpoint:

1. On the service details page, click **Manage endpoints**. You can see the external endpoint assigned to your service instance.
2. Click  **Add internal endpoint**. An internal endpoint is assigned to your service instance.
3. **Optional.** Use the endpoint toggle to enable or disable endpoints as needed.


For more information about service endpoints, check out the [{{site.data.keyword.Bluemix_short}} Service Endpoint documentation](/docs/services/service-endpoint?topic=service-endpoint-about#about){:new_window}.
