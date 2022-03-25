---

copyright:
  years: 2022
lastupdated: "2022-03-25"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka, AWS, location, VPN

subcollection: EventStreams

---

{:codeblock: .codeblock}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:beta: .beta}
{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:step: data-tutorial-type='step'}
{:tutorial: data-hd-content-type='tutorial'}

# Connecting applications running outside AWS with VPN access to the Satellite location
{: #satellite_vpn}

To connect applications running outside Amazon Web Services (AWS) with VPN access to the Satellite location to an {{site.data.keyword.messagehub}} instance, complete the following set of steps.

![VPN diagram](satellite_vpn.png "VPN"){: caption="Figure 1. Diagram showing an app connecting to clients using a VPN endpoint " caption-side="bottom"}

## Set up the Satellite plan for {{site.data.keyword.messagehub_full}} in a Satellite location using AWS
{: #prepare-satellite-aws}
{: step}

Complete the steps in [Getting started with the Satellite plan for Event Streams](/docs/EventStreams?topic=EventStreams-satellite_getting_started){: external} to set up the plan for {{site.data.keyword.messagehub}} in a Satellite location that is using AWS infrastructure.

## Create a Client VPN endpoint
{: #create_vpn_endpoint}
{: step}

1. Create a Client VPN endpoint that does the following:
   * Provides all clients with access to a single VPC.
   * Provides all clients with access to the internet.
   * Uses mutual authentication.
2. Complete the steps detailed in [Getting started with Client VPN](https://docs.aws.amazon.com/vpn/latest/clientvpn-admin/cvpn-getting-started.html){: external}.

## (Optional) Test the {{site.data.keyword.messagehub}} producer and consumer sample applications
{: #test_sample_apps}
{: step}

To test sending and receiving messages, you can optionally use the {{site.data.keyword.messagehub}} Java sample. The sample shows how a producer sends messages to a consumer by using a topic. The same sample program is used to consume messages and produce messages.

Use the steps detailed in [{{site.data.keyword.messagehub}} Getting Started](/docs/EventStreams?topic=EventStreams-getting-started){: external} to run the sample application.

Alternatively, you can also use your own applications to perform this validation.

## (Optional) Test the {{site.data.keyword.messagehub}} CLI
{: #test_cli}
{: step}

In the previous step, you used the sample application to produce and consume messages. You can optionally use the information in [{{site.data.keyword.messagehub}} CLI reference](docs/EventStreams?topic=EventStreams-cli_reference) to verify that the {{site.data.keyword.messagehub}} CLI can communicate with your {{site.data.keyword.messagehub}} deployment. The {{site.data.keyword.messagehub}} CLI enables you to easily work with topics and consumer groups.

Alternatively, you can also use your own applications to perform this validation.


