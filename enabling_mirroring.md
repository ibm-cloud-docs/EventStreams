---

copyright:
  years: 2015, 2023
lastupdated: "2023-12-19"

keywords: replication, failover, scenario, disaster recovery, mirroring, setup, backup, geo-replication, bindings

subcollection: EventStreams

---

{{site.data.keyword.attribute-definition-list}}

# Enabling mirroring
{: #mirroring_setup}

This information describes how to set up two {{site.data.keyword.messagehub}} Enterprise clusters as a mirrored pair. Use cases include disaster recovery, backups, and geo-replication.
{: shortdesc}

Using mirroring with {{site.data.keyword.messagehub}} incurs an extra charge for each mirroring capacity unit hour. For more information, go to the [Catalog](https://cloud.ibm.com/catalog#services) and search for `Event Streams`. You can then view pricing plans.

Currently, enabling mirroring for an {{site.data.keyword.messagehub}} service instance requires the use of the {{site.data.keyword.Bluemix_notm}} CLI.

To install the CLI, see [Extending IBM Cloud CLI with plug-ins](/docs/cli?topic=cli-plug-ins).

The {{site.data.keyword.Bluemix_notm}} CLI uses the **service-instance-update** command to update your {{site.data.keyword.messagehub}} service instance resource. The user ID in the account used to run the **service-instance-update** command must be assigned the same access policies that are needed when you create resources. For information about access requirements, see [Required access for creating resources](/docs/account?topic=account-manage_resource#creating-resources).

The time required to enable mirroring for the {{site.data.keyword.messagehub}} service instance varies, but under normal circumstances it does not exceed 2 hours.

## Step 1: Setup 
{: #step1_setup}

Mirroring is not supported for an Enterprise single-zone-region cluster or a Satellite cluster, therefore neither can be a source nor a target cluster.
{: note}

Ensure that you provision two Enterprise plan clusters. Both clusters must have the same throughput and storage capacity and have service-to-service bindings (see [Step 2](#step2_bindings) for more information).

Because mirroring is unidirectional, decide which direction of mirroring you want. One cluster is the source and the other cluster is the target.

Decide which topics from your source cluster that you want to mirror. By default no topics are mirrored and you can enable mirroring by using the user controls after mirroring is enabled as shown in [step 4](#step4_validation). You must specify the selection as one or more patterns.

Consider your bandwidth requirements; is there enough bandwidth available in the source cluster? Your source cluster needs to have some headroom to run mirroring. See [Choosing your plan](/docs/EventStreams?topic=EventStreams-plan_choose) for cluster bandwidth limits and use [Event Streams metrics](/docs/EventStreams?topic=EventStreams-metrics) to determine how busy your source cluster is and whether it has the headroom for mirroring.

## Step 2: Enable service-to-service bindings
{: #step2_bindings}

You must configure a service-to-service binding between both instances to allow both instances to communicate. To configure, complete the following steps:

1. Navigate to the **Authorizations** panel in IAM and click **Create**. 
2. **From the point of view of IAM, the source and target services are the opposite of mirroring**. Select both clusters, assign the **Reader** role, and click **Authorize**.

If your requirement is to fail back, you also need the service-to-service binding in the opposite direction.
{: important}

The following example shows how to use the command line to configure service-to-service binding. 

In this command we are using IAM source and target definitions, which are the opposite to that of mirroring. That is, IAM Source cluster is the mirroring target cluster.
{: note}

```sh
ibmcloud iam authorization-policy-create messagehub messagehub Reader --source-service-instance-id <instance id of the mirroring target cluster> [--source-service-account <account id>] --target-service-instance-id <instance id of the mirroring source cluster>
```
{: codeblock}

For more information about service-to-service bindings, see [**Manage authorizations** panel](https://cloud.ibm.com/iam/authorizations) and [Using authorizations to grant access between services](/docs/account?topic=account-serviceauth).

## Step 3: Enable mirroring
{: #step3_enable}

To enable mirroring, you need to run a **service-instance-update** command against your target cluster by using the CLI with the following required parameters:

| Required Parameters | Description |
| ---------- | ----------- |
| source_crn | The crn of the source cluster to be mirrored |
| source_alias | The alias used for the source cluster | 
| target_alias | The alias used for the target cluster | 
{: caption="Table 1. Required parameters when enabling mirroring" caption-side="bottom"}

- The `source_crn` is in this format: "crn:v1:bluemix:public:messagehub:us-south:a/aaa:aaaa::"
- The `source_alias` and the `target_alias` are the aliases that you want to configure for each of the two service instances when you enable mirroring. The aliases appear in topic names. Choose short and descriptive names. For example, "us-south" and "us-east".

### Example CLI command
{: #example_cli_command}

```sh
ibmcloud resource service-instance-update "Event Streams resource instance name" -p '{"mirroring":{"source_crn":"<source_crn>", "source_alias":"<source_alias>", "target_alias":"<target_alias>"}}'
```
{: codeblock}

If the cluster is provisioned with or scaled up to a throughput higher than the default value of 150, the **service-instance-update** command must also include "throughput":"_current throughput value_" in the update parameter body.
{: note}

### Example CLI command with throughput
{: #example_cli_command_with_throughput}

```sh
ibmcloud resource service-instance-update "Event Streams resource instance name" -p '{"mirroring":{"source_crn":"<source_crn>", "source_alias":"<source_alias>", "target_alias":"<target_alias>"}, "throughput":"<current throughput value>"}'
```
{: codeblock}

## Step 4: Validation
{: #step4_validation}

You can get the current service instance information by running the following command:

```sh
ibmcloud resource service-instance "Event Streams resource instance name" --output=json
```
{: codeblock}

Review the **last operation** section of the output. The information is continuously updated as the update proceeds. When the mirroring enablement process has completed, the last operation information indicates whether the update succeeded or the sync succeeded.

```sh
"last_operation": {
  "type": "update",
  "state": "in progress",
  "description": "Update in progress.",
  "updated_at": null,
  "cancelable": false
}
```
{: screen}

Run the command again until success is indicated as follows:

```sh
"last_operation": {
  "type": "update",
  "state": "succeeded",
  "description": "Update succeeded.",
  "updated_at": null,
  "cancelable": false
}
```
{: screen}

The {{site.data.keyword.mon_full_notm}} dashboard **{{site.data.keyword.messagehub}} Mirroring** shows the state of mirroring.

## Step 5: Select topics
{: #step5_selecttopics}

When the service instance update has completed, we want to select some topics from the source cluster to mirror. This is done with the CLI by using the **ibmcloud es mirroring-topic-selection-set** command.

Topic selection is in the form of a regex pattern, or comma-separated list of such patterns.

The following command selects all topics to be mirrored:

```sh
ibmcloud es mirroring-topic-selection-set --select '.*'
```
{: codeblock}

You can select topics by listing the topics you want to mirror as follows:

```sh
ibmcloud es mirroring-topic-selection-set --select topic1,topic2,topic3
```
{: codeblock}

For more information about making the selection, see [Mirroring user controls](/docs/EventStreams?topic=EventStreams-mirroring#user_controls).

After the topic selection is completed, the target cluster shows the topics that are selected for mirroring using the **Mirroring user controls** suffixed with the source cluster's alias.

