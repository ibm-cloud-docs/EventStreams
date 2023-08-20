---

copyright:
  years: 2015, 2023
lastupdated: "2023-08-15"

keywords: replication, failover, scenario, disaster recovery, mirroring, setup, backup, geo-replication, bindings

subcollection: EventStreams

---

{{site.data.keyword.attribute-definition-list}}

# Enabling mirroring
{: #mirroring_setup}

This information describes how to set up a pair of {{site.data.keyword.messagehub}} Enterprise clusters as a mirrored pair. Use cases include disaster recovery, backups, and geo-replication.
{: shortdesc}

Using mirroring with {{site.data.keyword.messagehub}} incurs an extra charge for each mirroring capacity unit hour. For more information, go to the [Catalog](https://cloud.ibm.com/catalog#services) and search for `Event Streams`. You can then view pricing plans.

## Step 1: Setup 
{: #step1_setup}

Ensure that you provisioned two Enterprise plan clusters. Both clusters must have the same throughput and storage capacity and have suitable IAM access policies.

Because mirroring is unidirectional, decide which direction mirroring you want. One cluster is the source and the other cluster is the target.

Decide which topics from your source cluster that you want to mirror. By default no topics are mirrored and you can enable mirroring by using the user controls when you are ready. Alternatively you can provide details of which topics to include at set up time. 
The selection must be specified as one or more patterns. For more information about making the selection, see [Mirroring user controls](/docs/EventStreams?topic=EventStreams-mirroring#user_controls).

Consider your bandwidth requirements; is there enough bandwidth available in the source cluster? Your source cluster needs to have some headroom to run mirroring. See [Choosing your plan](/docs/EventStreams?topic=EventStreams-plan_choose) for cluster bandwidth limits and use [Event Streams Metrics](/docs/EventStreams?topic=EventStreams-metrics) to determine how busy your source cluster is and whether it has the headroom for mirroring.

## Step 2: Enable service-to-service bindings
{: #step2_bindings}

A service-to-service binding between both instances must be configured to allow both instances to communicate. To configure, complete the following steps:

1. Navigate to the **Authorizations** panel in IAM and click **Create**. 
2. **From the point of view of IAM, the source and target services are the opposite of mirroring**. Select both clusters, assign the Reader role, and click **Authorize**.

If your requirement is to fail back, you need also the service-to-service binding in the opposite direction.
{: important}

The following example shows how to use the command line to configure service-to-service binding. 

In this command we are using IAM source and target definitions, which are the opposite to that of mirroring. That is, IAM Source cluster is the mirroring target cluster.
{: note}

```text
ibmcloud iam authorization-policy-create messagehub messagehub Reader --source-service-instance-id <instance id of the source cluster> --source-service-account <account id> --target-service-instance-id <instance id of target>
```

For more information about service-to-service bindings, see [Manage authorizations panel](https://cloud.ibm.com/iam/authorizations) and [Using authorizations to grant access between services](https://cloud.ibm.com/docs/iam?topic=iam-serviceauth).

## Step 3: Enable mirroring
{: #step3_enable}

Raise a [support ticket](/docs/get-support?topic=get-support-open-case&interface=ui#creating-support-case) to request enablement of mirroring. 


Include the following information in the ticket:
- CRN of both {{site.data.keyword.messagehub}} service instances.
- Whether it is a new enablement of mirroring, failback on an existing mirroring setup, or restoring the original configuration after a failback.
- Aliases that you want to use for each of the two instances. You configure an alias for each service instance when you enable mirroring. The aliases appear in topic names. Choose short and descriptive names. For example, "us-south" and "us-east".
- The wanted direction for mirroring.
- The set of patterns for the source topics to be mirrored.

When you raise a ticket to enable mirroring, be aware that the ticket will only be processed during weekday business hours. Please plan ahead and assume it will take 1-2 days for mirroring to be enabled.
{: note}

### Example request
{: #example_request}

```text
We request the Event Streams team to enable mirroring between the following 2 service instances:
- crn:v1:bluemix:public:messagehub:us-south:a/aaa:aaaa:: aliased with "us-south"
- crn:v1:bluemix:public:messagehub:us-east:a/bbb:bbbb:: aliased with "us-east"

Data is to flow from "us-south" to "us-east".

Mirrored topics are:
"aaa.*"
"bbb.*"
```
{: codeblock}

## Step 4: Validation
{: #step4_validation}

When the ticket is processed by the {{site.data.keyword.messagehub}} team, the target cluster shows the topics that are suffixed with the source clusters alias. The {{site.data.keyword.mon_full_notm}} dashboard "{{site.data.keyword.messagehub}} Mirroring" shows the state of mirroring.

