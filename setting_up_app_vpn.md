---

copyright:
  years: 2022, 2023
lastupdated: "2023-02-15"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka, AWS, location, VPN

subcollection: EventStreams

---

{{site.data.keyword.attribute-definition-list}}

# Connecting applications that run outside AWS with VPN access to the Satellite location
{: #satellite_vpn}

To connect applications that run outside Amazon Web Services (AWS) with VPN access to the Satellite location to an {{site.data.keyword.messagehub}} instance, complete the following set of steps.

![VPN diagram](satellite_vpn.png "VPN"){: caption="Figure 1. Diagram showing an app that connects to clients by using a VPN endpoint." caption-side="bottom"}

## Set up the Satellite plan for {{site.data.keyword.messagehub_full}} in a Satellite location by using AWS
{: #prepare-satellite-aws}
{: step}

Complete the steps in [Provisioning Event Streams for Satellite](/docs/EventStreams?topic=EventStreams-satellite-provisioning){: external} to set up the plan for {{site.data.keyword.messagehub}} in a Satellite location that is using AWS infrastructure.

## Create a Client VPN endpoint
{: #create_vpn_endpoint}
{: step}

1. Create a Client VPN endpoint with the following criteria.
   * Provides all clients with access to a single VPC.
   * Provides all clients with access to the internet.
   * Uses mutual authentication.
2. Complete the steps that are detailed in [Getting started with Client VPN](https://docs.aws.amazon.com/vpn/latest/clientvpn-admin/cvpn-getting-started.html){: external}.

## (Optional) Test the {{site.data.keyword.messagehub}} producer and consumer sample applications
{: #test_sample_apps}
{: step}

To test sending and receiving messages, you can optionally use the {{site.data.keyword.messagehub}} Java sample. The sample shows how a producer sends messages to a consumer by using a topic. The same sample program is used to consume messages and produce messages.

Use the steps that are detailed in [{{site.data.keyword.messagehub}} Getting Started](/docs/EventStreams?topic=EventStreams-getting-started){: external} to run the sample application.

Alternatively, you can also use your own applications to perform this validation.

## (Optional) Test the {{site.data.keyword.messagehub}} CLI
{: #test_cli}
{: step}

In the previous step, you used the sample application to produce and consume messages. You can optionally use the information in [{{site.data.keyword.messagehub}} CLI reference](/docs/EventStreams?topic=EventStreams-cli_reference) to verify that the {{site.data.keyword.messagehub}} CLI can communicate with your {{site.data.keyword.messagehub}} deployment. With the {{site.data.keyword.messagehub}} CLI you can easily work with topics and consumer groups.

Alternatively, you can also use your own applications to perform this validation.
