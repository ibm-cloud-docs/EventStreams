---

copyright:
  years: 2015, 2019
lastupdated: "2019-11-14a"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka, service endpoints

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Restricting network access using the Enterprise plan
{: #restrict_access}

By default, {{site.data.keyword.messagehub}} allows access from any IP address on the public internet. If you are using an instance of the {{site.data.keyword.vpc_full}}, you are recommended to apply the following restrictions so that only designated VSIs within your VPC can establish network connections to the {{site.data.keyword.messagehub}} instance. 

Enable [Cloud Service Endpoints (CSE)](/docs/resources?topic=resources-service-endpoints) to restrict access to any source IP addresses on the {{site.data.keyword.Bluemix_short}} network. When you implement IP addresses whitelisting on the Cloud Service endpoints, access is subsequently restricted to VSIs with specified VPCs. 

## Prerequisites

Ensure that you complete the following tasks:
* Create your service instance by using the Enterprise plan. For more information, see 
[Choosing your plan](/docs/services/EventStreams?topic=eventstreams-plan_choose).
* Enable [Virtual Route Forwarding (VRF)](/docs/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) for your {{site.data.keyword.Bluemix_short}} account.
* Ensure Virtual Private Cloud instance is Cloud Service endpoint enabled.

## Obtaining Virtual Private Cloud CSE source IP addresses

If you want to restrict access to VSIs hosted within a specific VPC, you have to discover the VPC source IP addresses. 

1. Obtain the ID of the VPC from the {{site.data.keyword.Bluemix_short}} Infrastructure UI.

   ```
export VPC_ID=<vpc_id>
   ```
   {: codeblock}

2. Obtain a bearer token from IAM using the ibmcloud CLI tooling

   ```
   export IAM_TOKEN=$(bx iam oauth-tokens --output json | jq -r .iam_token)
   ```
   {: codeblock}

3. Use the VPC REST API to obtain the source IP addresses

   ```
   curl -H "Authorization: $IAM_TOKEN" "https://us-south.iaas.cloud.ibm.com/v1/vpcs/$VPC_ID?version=2019-10-15&generation=1" 2>/dev/null | jq-r'.cse_source_ips | .[] | "\(.ip)/32"'
   ```
   {: codeblock}

## Enabling {{site.data.keyword.Bluemix_notm}} Service endpoints 

To add an {{site.data.keyword.Bluemix_notm}} service endpoint:

* Raise a [ticket ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/get-support?topic=get-support-getting-customer-support#using-avatar){:new_window} to request a cloud service endpoint. Provide the following information in the ticket:

    * Your cluster ID, if you know it. 
    
    If you don't know the cluster ID, please provide your dashboard URL, the Kafka broker endpoints, or your service instance ID instead.
* If you want to restrict access to your cloud service endpoint to individual VPCs, include the VPC CSE source IP addresses that you obtained as described in the ticket.

## After switching to an {{site.data.keyword.Bluemix_notm}} service endpoint 
When you have switched to an {{site.data.keyword.Bluemix_notm}} service endpoint, the external or public endpoints are no longer available to you. This means that although existing credentials continue to be valid, the Kafka endpoints and HTTP endpoints in any pre-existing service credentials are no longer valid.

### Accessing the IBM {{site.data.keyword.messagehub}} console

When a cluster has private endpoints enabled, the admin URL that you use to access the {{site.data.keyword.messagehub}} console changes.

The {{site.data.keyword.messagehub}} console is reachable only from a private admin URL. To discover your private endpoints, including the private admin URL, you can create a new service credential.

Because the {{site.data.keyword.messagehub}} instance endpoints have now been converted to be accessed from the {{site.data.keyword.Bluemix_short}} only, the UI is accessible only via a web browser that is hosted on the {{site.data.keyword.Bluemix_short}} network.



------------------------------------------
## Managing service endpoints using the Enterprise plan
{: #manage_endpoints_old}

By using an internal or private endpoint, {{site.data.keyword.Bluemix_short}} Service Endpoint enables the connection to the {{site.data.keyword.messagehub}} service through the internal IBM Cloud network. This capability means that any data you publish or consume from the {{site.data.keyword.messagehub}} 
service is over the private network and not public interfaces.
{:shortdesc}

You can now add a private endpoint to access and manage your {{site.data.keyword.messagehub}} service instance.

## Prerequisites
{: #prereqs_endpoint_old}

Ensure that you meet the following requirements:
- Create your service instance by using the Enterprise plan. For more information, see [Choosing your plan](/docs/services/EventStreams?topic=eventstreams-plan_choose).
- Create your service instance in the {{site.data.keyword.Bluemix_notm}} Dallas (us-south) or Frankfurt (eu-de) regions.
- Enable [Virtual Route Forwarding (VRF)](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) for your {{site.data.keyword.Bluemix_notm}} account.

## Adding a private endpoint
{: #add_endpoint_old}

To add a private endpoint:

* Raise a [ticket ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/get-support?topic=get-support-getting-customer-support#using-avatar){:new_window} to request a private endpoint. Provide the following information in the ticket:

    * Your cluster ID, if you know it.

    If you don't know the cluster ID, please provide your dashboard URL, the Kafka broker endpoints, or your service instance ID instead.
  

For more information about service endpoints, see the [{{site.data.keyword.Bluemix_notm}} Service Endpoint documentation](/docs/resources?topic=resources-service-endpoints#about){:new_window}.


## After switching to a private endpoint
{: #after_endpoint_old}

When you have switched to a private endpoint, the external or public endpoints are no longer available to you.


### Accessing the IBM {{site.data.keyword.messagehub}} console

When a cluster has private endpoints enabled, the admin URL that you use to access the {{site.data.keyword.messagehub}} console changes.

The {{site.data.keyword.messagehub}} console is reachable only from a private admin URL. To discover your private endpoints, including the private admin URL, you can create a new service credential.

<!--
1. On the service details page, click **Manage endpoints**. You can see the external endpoint assigned to your service instance.
2. Click  **Add internal endpoint**. An internal endpoint is assigned to your service instance.
3. **Optional.** Use the endpoint toggle to enable or disable endpoints as needed.
-->

