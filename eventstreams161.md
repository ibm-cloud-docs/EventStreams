---

copyright:
  years: 2015, 2020
lastupdated: "2020-08-06"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka, replication, failover, scenario, disaster recovery, mirroring, setup

subcollection: EventStreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}
{:deprecated: .deprecated}
{:important: .important}

# Guide to setting up mirroring
{: #mirroring_setup}

This information describes how to set up a pair of {{site.data.keyword.messagehub}} Enterprise clusters as a mirrored pair. Use cases include disaster recovery, backups, and geo-replication.
{:shortdesc}


## Step 1: setup 
{: #step1_setup}
Ensure that you have provisioned two Enterprise plan clusters. Both clusters should also have the same throughput and storage capacity and have suitable IAM access policies.

Because mirroring is currently unidirectional, decide which direction mirroring should happen. One cluster will be the source and the other cluster will be the target.

Decide which topics from your source cluster you wish to mirror. By default no topics will be mirrored and you can enable mirroring using the user controls when you are ready. Alternatively you can provide details of which topics to include at set up time. The selection should be specified as one or more patterns, see [Mirroring user controls](/docs/EventStreams?topic=EventStreams-mirroring#user_controls) for more information on making the selection.

Consider your bandwidth requirements; is there enough bandwidth available in the source cluster? Your source cluster needs to have some headroom to run mirroring. See [Choosing your plan](/docs/EventStreams?topic=EventStreams-plan_choose) for cluster bandwidth limits and use [Event Streams Metrics](/docs/EventStreams?topic=EventStreams-metrics) to determine how busy your source cluster is and whether it has the headroom for mirroring.

## Step 2: enable service-to-service bindings
{: #step2_bindings}

A service-to-service binding between both instances must be configured to allow both instances to communicate. To configure, complete the following steps:

1. Navigate to the **Authorizations** panel in IAM and click **Create**. 
2. **From the point of view of IAM, the source and target services are the opposite of mirroring**. Select both clusters accordingly, assign the Reader role, and click **Authorize**.

If your requirement is to fail back, you will need also the service-to-service binding in the opposite direction.
{: important}

Here is an example of how to use the command line to configure service-to-service binding. Note, in this command we are using IAM source and target definitions, which is the opposite to that of mirroring. That is, IAM Source cluster is the mirroring target cluster.

```
ibmcloud iam authorization-policy-create messagehub messagehub Reader --source-service-instance-id <instance id of the source cluster> --source-service-account <account id> --target-service-instance-id <instance id of target>
```

For more information about service-to-service bindings, see [Manage authorizations panel](https://cloud.ibm.com/iam/authorizations) and [Using authorizations to grant access between services](https://cloud.ibm.com/docs/iam?topic=iam-serviceauth).

## Step 3: enable mirroring
{: #step3_enable}

Raise a [support ticket](/docs/get-support?topic=get-support-getting-customer-support#using-avatar) to request enablement of mirroring. 

Include the following information in the ticket:
- CRN of both {{site.data.keyword.messagehub}} service instances.
- Whether this is: a new enablement of mirroring, failback on an existing mirroring setup, or restoring the original configuration after a failback
- Aliases that you want to use for each of the two instances. Each service instance has an alias configured by the user when enabling mirroring. The aliases will appear in topic names. We recommend choosing short and descriptive names. For example "us-south" and "us-east".
- The desired direction for mirroring.
- The set of patterns for the source topics to be mirrored.

### Example request

For example:

```
We request the {{site.data.keyword.messagehub}} team to enable mirroring between the following 2 service instances
- crn:v1:bluemix:public:messagehub:us-south:a/aaa:aaaa:: aliased with "us-south"
- crn:v1:bluemix:public:messagehub:us-east:a/bbb:bbbb:: aliased with "us-east"

Data should flow from "us-south" to "us-east".

Mirrored topics should be:
"aaa.*"
"bbb.*"
```
{:codeblock}

## Step 4: validation
{: #step4_validation}

When the ticket has been processed by the {{site.data.keyword.messagehub}} team, the target cluster shows the topics suffixed with the source clusters alias. The Sysdig dashboard "{{site.data.keyword.messagehub}} Mirroring" shows the state of mirroring.

