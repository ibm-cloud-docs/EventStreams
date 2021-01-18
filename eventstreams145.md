---

copyright:
  years: 2015, 2021
lastupdated: "2021-01-18"

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

By default, {{site.data.keyword.messagehub}} instances are configured to use the {{site.data.keyword.Bluemix_short}} public network, so they are accessible over the public Internet. 

If your workload is running entirely within the {{site.data.keyword.Bluemix_short}}, and public access to the service is not required, {{site.data.keyword.messagehub}} instances can instead be configured to only be accessible over the {{site.data.keyword.Bluemix_short}} private network. This offers increased isolation and does not incur the egress bandwidth charges associated with public traffic. If required, further isolation is also possible by specifying an allowlist of the IP addresses (source IPs) from which private traffic will be accepted, for instance, the IPs of the VSIs or VPCs within the {{site.data.keyword.Bluemix_short}} where your workload is running.

Instances can also be configured to be accessible over both the {{site.data.keyword.Bluemix_short}} public and private networks, where your workload can use the most appropriate interface for its location.

Further information about IBM Cloud private networking setup can be found here:[Cloud Service Endpoints (CSE) ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/docs/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud){:new_window}.


## Prerequisites
{: #prereqs_restrict_access}

Ensure that you complete the following tasks:
* Create your service instance by using the Enterprise plan. For more information, see
[Choosing your plan ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/EventStreams?topic=EventStreams-plan_choose){:new_window}.
* Enable [Virtual Route Forwarding (VRF) ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud){:new_window} for your {{site.data.keyword.Bluemix_short}} account.
* Enable service endpoints connectivity by running this command: 
```
ibmcloud account update --service-endpoint-enable true
```

To check if prerequisites are completed, run the following command and then check if the following two properties are true:
```
ibmcloud account show

VRF Enabled:                        true
Service Endpoint Enabled:           true
```

   
## Selecting a network configuration 

{: #enable_endpoints}

There are a number of options you have for selecting the network configuration of your Enterprise cluster.

1. Use the {{site.data.keyword.Bluemix_notm}} public network - Endpoints are accessible on the public Internet. This is the default.

2. Use the {{site.data.keyword.Bluemix_notm}} private network - Endpoints are not visible on the public Internet.

3. Use the {{site.data.keyword.Bluemix_notm}} public and private network - Endpoints are visible on both the public Internet and internally within the {{site.data.keyword.Bluemix_notm}}.

This slection can be made at provision time through the {{site.data.keyword.messagehub}} catalog provisioning page. Use the Service Endpoints menu pull down to select either "Public" (default), "Private" or "Public and Private".

Alternatively, if you want to use the CLI to provision an {{site.data.keyword.messagehub}} service, use the following commands:

To enable public endpoints (this is the default):

```
ibmcloud resource service-instance-create <instance-name> <plan-name> <region> --service-endpoints public
```
  {: codeblock}

To enable private only endpoints:
```
ibmcloud resource service-instance-create <instance-name> <plan-name> <region> --service-endpoints private
```
{: codeblock}

To enable both, private and public endpoints:

```
ibmcloud resource service-instance-create <instance-name> <plan-name> <region> --service-endpoints public-and-private
```
{: codeblock}

use plan-name = **messagehub ibm.message.hub.enterprise.3nodes.2tb**


In addition, if you select private endpoints and want to further restrict access to only known VSIs with specific VPCs, you can add an IP allowlist via the CLI by appending as follows:

```
ibmcloud resource service-instance-create <instance-name> <plan-name> <region> --service-endpoints private -p '{"private_ip_allowlist":["CIDR1","CIDR2"]}' "
```
{: codeblock}

where CIDR1, 2 are IP addressess of the form a.b.c.d/e


## Updating the network configuration or IP allowlist
{: #update_endpoints}

You are also able to switch the endpoints that your Enterprise cluster uses after provisioning. To do this,use the following CLI commands.

To enable private endpoints:

```
ibmcloud resource service-instance-update <instance-name> --service-endpoints private
```
{: codeblock}

Note that switching to private endpoints whilst the cluster is in use is **not recommended**. It will disable all public endpoints and your applications will lose access to the cluster. This can be avoided if you first enable both public and private endpoints, then re-configure applications to use private endpoints, and finally switch to private only endpoints.
{:important}


An initial first step is to enable both public and private endpoints:

```
ibmcloud resource service-instance-update <instance-name> --service-endpoints public-and-private
```
{: codeblock}


Next, once applications migrated to the private endpoints, you can issue the following to turn off the public endpoints:
```
ibmcloud resource service-instance-update <instance-name> --service-endpoints private
```
{: codeblock}


To change the IP allowlist, perform the following steps:

1. Obtain the original IP allowlist applied on the instance

```
$ibmcloud es init -i <instance-name>
API Endpoint:		https://mh-cktmqpdbvkfczhmn.us-south.containers.appdomain.cloud
Service endpoints:	public-and-private
Private IP allowlist:	"10.243.0.8/32","10.243.128.8/32","10.243.64.4/32"
Storage size:		4096 GB
Throughput:		300 MB/s
OK
```

2. Add CIDRs into or delete CIDRs from the `Private IP allowlist`.

3. Run the following command to update the service instance with a new list:

  ```
  ibmcloud resource service-instance-update <instance-name> --service-endpoints private -p '{"private_ip_allowlist":["CIDR1","CIDR2"]}'
  ```
  {: codeblock}

  where CIDR1, 2 are IP addressess of the form a.b.c.d/e

Note that if the private endpoint is enabled via CLI, next time when updating private IP allowlist, `--service-endpoints private` can be omitted.

Switching IP allowlists will disable any allowed IP address not in the new list. Applications accessing the cluster from those addresses will lose access to the cluster.


## How to check if an instance update is completed
{: #check_endpoints}

Typically, the above updates take less than an hour. To check status use the following command:

```
ibmcloud resource service-instance <instance-name>
```
{: codeblock}

when **Last Operation.Status** shows **"sync succeeded"**, instance update is complete.

## How to set private IP allowlist via Schematics
{: #schematics_integration}

Event Streams supports integration with [Schematics](https://cloud.ibm.com/docs/schematics?topic=schematics-getting-started).

Refer to this [example](https://cloud.ibm.com/docs/terraform?topic=terraform-event-streams-resources) about how to set the `private_ip_allowlist` in a Terraform script. 

Note: If the terraform script is executed from Schematics, additional IPs are required to be added into Event Streams' `private_ip_allowlist` to allow Schematics to access Event Streams' API endpoints. Find the IPs of Schematics in each region from [here](https://cloud.ibm.com/docs/schematics?topic=schematics-allowed-ipaddresses).


## Obtaining Virtual Private Cloud (VPC) CSE source IP addresses
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


## Migrate applications to use private endpoints
{: #migrate_endpoints}

Once you have enabled private endpoints, you will need new access credentials. Create a new service key with private service endpoint:

```
ibmcloud resource service-key-create <private-key-name> <role> --instance-name <instance-name> --service-endpoint private
```
{: codeblock}

and update the credentials in the application to use the newly created one:

### Accessing the IBM {{site.data.keyword.messagehub}} console
{: #access_console}

Once the required network configuration has been selected, all subsequent connections to the APIs and user console must adopt this method. The associated endpoint information can be retrieved by creating a new service credential.


.
