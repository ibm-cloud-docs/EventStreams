---

copyright:
  years: 2015, 2019
lastupdated: "2019-05-24"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka, service endpoints

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Managing service endpoints using the Enterprise plan
{: #manage_endpoints}

By using an internal or private endpoint, {{site.data.keyword.Bluemix_short}} Service Endpoint enables the connection to the {{site.data.keyword.messagehub}} service through the internal IBM Cloud network. This capability means that any data you publish or consume from the {{site.data.keyword.messagehub}} 
service is over the private network and not public interfaces.
{:shortdesc}

You can now add a private endpoint to access and manage your {{site.data.keyword.messagehub}} service instance.

## Prerequisites
{: #prereqs_endpoint}

Ensure that you meet the following requirements:
- Create your service instance by using the Enterprise plan. For more information, see [Choosing your plan](/docs/services/EventStreams?topic=eventstreams-plan_choose).
- Create your service instance in the {{site.data.keyword.Bluemix_notm}} Dallas (us-south) or Frankfurt (eu-de) regions.
- Enable [Virtual Route Forwarding (VRF)](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) for your {{site.data.keyword.Bluemix_notm}} account.

## Adding a private endpoint
{: #add_endpoint}

To add a private endpoint:

* Raise a [ticket ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/get-support?topic=get-support-getting-customer-support#using-avatar){:new_window} to request a private endpoint. Provide the following information in the ticket:

    * Your cluster ID, if you know it.

    If you don't know the cluster ID, please provide your dashboard URL, the Kafka broker endpoints, or your service instance ID instead.
  

For more information about service endpoints, see the [{{site.data.keyword.Bluemix_notm}} Service Endpoint documentation](/docs/resources?topic=resources-service-endpoints#about){:new_window}.


## After switching to a private endpoint
{: #after_endpoint}

When you have switched to a private endpoint, the external or public endpoints are no longer available to you.


### Accessing the IBM {{site.data.keyword.messagehub}} console

When a cluster has private endpoints enabled, the admin URL that you use to access the {{site.data.keyword.messagehub}} console changes.

The {{site.data.keyword.messagehub}} console is reachable only from a private admin URL. To discover your private endpoints, including the private admin URL, you can create a new service credential.

<!--
1. On the service details page, click **Manage endpoints**. You can see the external endpoint assigned to your service instance.
2. Click  **Add internal endpoint**. An internal endpoint is assigned to your service instance.
3. **Optional.** Use the endpoint toggle to enable or disable endpoints as needed.
-->

