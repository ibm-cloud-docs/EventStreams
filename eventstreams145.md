---

copyright:
  years: 2015, 2020
lastupdated: "2020-03-18"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka, service endpoints, VSIs, VPC, CSE, disruptive

subcollection: EventStreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}


# Restricting network access using the Enterprise plan
{: #restrict_access}

By default, {{site.data.keyword.messagehub}} instances are configured to use the {{site.data.keyword.Bluemix_short}} public network so they are accessible over the public internet. 

If your workload is running entirely within the {{site.data.keyword.Bluemix_short}}, and public access to the service is not required, {{site.data.keyword.messagehub}} instances can instead be configured to only be accessible over the {{site.data.keyword.Bluemix_short}} private network. This offers increased isolation and does not incur the egress bandwidth charges associated with public traffic. If required, further isolation is also possible by specifying a white-list of the IP addresses (source IPs) from which private traffic will be accepted, for instance, the IPs of the VSIs or VPCs within the {{site.data.keyword.Bluemix_short}} where your workload is running.

Instances can also be configured to be accessible over both the {{site.data.keyword.Bluemix_short}} public and private networks, where your workload can use the most appropriate interface for its location.

Private network access is achieved using {{site.data.keyword.Bluemix_notm}}. See the following link to enable [Cloud Service Endpoints (CSE) ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/docs/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud){:new_window}.

When you switch to an {{site.data.keyword.Bluemix_notm}} service endpoint, the external or public endpoints are no longer available, making this enablement a disruptive change. Consequently, although existing credentials continue to be valid, the Kafka endpoints and HTTP endpoints in any pre-existing service credentials are no longer valid.
{:important}


## Prerequisites
{: #prereqs_restrict_access}

Ensure that you complete the following tasks:
* Create your service instance by using the Enterprise plan. For more information, see 
[Choosing your plan ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/EventStreams?topic=EventStreams-plan_choose){:new_window}.
* Enable [Virtual Route Forwarding (VRF) ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud){:new_window} for your {{site.data.keyword.Bluemix_short}} account.
* Ensure Virtual Private Cloud instance is Cloud Service endpoint enabled.

## Obtaining Virtual Private Cloud CSE source IP addresses
{: #vpc_ip}

If you want to restrict access to VSIs hosted within a specific VPC, you first have to discover the VPC source IP addresses. 

1. Obtain the ID of the VPC from the {{site.data.keyword.Bluemix_notm}} Infrastructure console:

   ```
   export VPC_ID=<vpc_id>
   ```
  {: codeblock}

2. Obtain a bearer token from IAM using the ibmcloud CLI:
   
   ```
   export IAM_TOKEN=$(bx iam oauth-tokens --output json | jq -r .iam_token)
   ```
   {: codeblock}

3. Use the VPC REST API to obtain the source IP addresses:

   ```
   curl -H "Authorization: $IAM_TOKEN" "https://us-south.iaas.cloud.ibm.com/v1/vpcs/$VPC_ID?version=2019-10-15&generation=1" 2>/dev/null | jq -r'.cse_source_ips | .[] | "\(.ip)/32"'
   ```
   {: codeblock}
   
## Enabling {{site.data.keyword.Bluemix_notm}} Service endpoints 
{: #enable_endpoints}

There are a number of options you have for selecting endpoints on your Enterprise cluster.

1. Do not use {{site.data.keyword.Bluemix_notm}} service endpoints - Endpoints are accessible on public internet
2. Use {{site.data.keyword.Bluemix_notm}} service endpoints to enable private endpoints and disable public endpoints - Endpoints are not visible on publc internet.
3. Use {{site.data.keyword.Bluemix_notm}} service endpoints to enable both private endpoints and public endpoints.

You can select your endpoints at provision time through the {{site.data.keyword.messagehub}} catalog provisioning page. Use the Service Endpoints menu pull down to select either "Public" (default), "Private" or "Public and Private".

Alternatively, if you wish to use the CLI to provision an {{site.data.keyword.messagehub}} service then you would use the following command: 

```
ibmcloud resource service-instance-create <instance-name> <plan-name> <region> --service-endpoints public
```
  {: codeblock}
  
```
ibmcloud resource service-instance-create <instance-name> <plan-name> <region> --service-endpoints private
```
{: codeblock}

```
ibmcloud resource service-instance-create <instance-name> <plan-name> <region> --service-endpoints public-and-private
```
{: codeblock}

use plan-name = messagehub ibm.message.hub.enterprise.3nodes.2tb


In addition to the above, if you select private endpoints and wish to further restrict access to only known VSIs with specific VPCs you can add an IP whitelist via the CLI by appending as follows.

```
ibmcloud resource service-instance-create <instance-name> <plan-name> <region> --service-endpoints private -p '{"private_ip_whitelist":["CIDR1","CIDR2"]}' "
```
{: codeblock}

where CIDR1, 2 are .......????? ip addresses of the form ww.xx.yy.zz.? 

## Updating Cloud Service Endpoints or IP Whitelists
{: #update_endpoints}

You are also able to switch the endpoints that your Enterprise cluster uses after provisioning. To do this you use the following CLI commands


To enable private endpoints
```
ibmcloud resource service-instance-update <instance-name> --service-endpoints private
```
{: codeblock}

NB - switching to private endpoints whilst the cluster is in use is NOT recommended. It will disable all public endpoints and your applications will lose access to the cluster.
 
An initial first step would be to enable both public and private
```
ibmcloud resource service-instance-update <instance-name> --service-endpoints public-and-private
```
{: codeblock}

and then once applications migrated to the private endpoints, one can issue the following to turn off the public endpoints.
```
ibmcloud resource service-instance-update <instance-name> --service-endpoints private
```
{: codeblock}


To change the IP whitelist use the following command
```
ibmcloud resource service-instance-update <instance-name> --service-endpoints private -p '{"private_ip_whitelist":["CIDR1","CIDR2"]}'
```
{: codeblock}

where CIDR1, 2 are .......????? ip addresses of the form ww.xx.yy.zz.? 
?????This is not additive right? All old and new need to be listed, any old not listed are removed form whitelist ???****


NB:  If the private endpoint is enabled via CLI, then next time when updating private IP whitelist, --service-endpoints private can be omitted.


NB:  switching IP Whitelists will disable any whitelisted IP address not in the new list. Applications accessing the cluster from those addresses will lose access to the cluster.


## How to check if instance update is completed
{: #check_endpoints}
Typically we would expect the above updates to take less than an hour. To check status use the following command
```
ibmcloud resource service-instance <instance-name>
```
{: codeblock}

when Last Operation.Status shows "sync succeeded", instance update is complete.


## Migrate Applications to use Private Endpoints
{: #migrate_endpoints}
Once you have enable private endpoints then you will need new access credentials.  Create a new service key with private service endpoint:
```
ibmcloud resource service-key-create <private-key-name> <role> --instance-name <instance-name> --service-endpoint private
```
{: codeblock}

and update the credentials in the application to use the newly created one

## After switching to an {{site.data.keyword.Bluemix_notm}} service endpoint 
{: #after_endpoints}

When you have switched to an {{site.data.keyword.Bluemix_notm}} service endpoint, the external or public endpoints are no longer available to you. This means that although existing credentials continue to be valid, the Kafka endpoints and HTTP endpoints in any pre-existing service credentials are no longer valid.

### Accessing the IBM {{site.data.keyword.messagehub}} console
{: #access_console}

When a cluster has private endpoints enabled, the admin URL that you use to access the {{site.data.keyword.messagehub}} console changes.

The {{site.data.keyword.messagehub}} console is reachable only from a private admin URL. To discover your private endpoints, including the private admin URL, you can create a new service credential.

Because the {{site.data.keyword.messagehub}} instance endpoints have now been converted to be accessed from the {{site.data.keyword.Bluemix_notm}} only, the {{site.data.keyword.messagehub}} console is accessible only using a web browser that is hosted on the {{site.data.keyword.Bluemix_notm}} network.



.




