---

copyright:
  years: 2015
lastupdated: "2025-10-06"

keywords: replication, failover, scenario, disaster recovery, mirroring, setup, backup, geo-replication, bindings

subcollection: EventStreams

---

{{site.data.keyword.attribute-definition-list}}

# Enabling mirroring
{: #mirroring_setup}

This information describes how to set up two {{site.data.keyword.messagehub}} Enterprise clusters as a mirrored pair. Use cases include disaster recovery, backups, and geo-replication.
{: shortdesc}

When you build a solution involving mirroring in {{site.data.keyword.messagehub}}, consider how your solution will deal with the following two scenarios:

Data loss
:  Mirroring is asynchronous. That is, messages must be successfully produced to the source cluster before being mirrored to the target cluster. If a failure occurs on the source cluster before those messages are mirrored, applications will need to deal with the loss of those messages.

At least once
:  Message duplication can occur in the mirroring process. Consumer group offsets committed in the source cluster might not be converted to checkpoints in the target cluster. At failover, a consumer might need to reprocess messages already consumed and committed on the source cluster.

Using mirroring with {{site.data.keyword.messagehub}} incurs an extra charge for each mirroring capacity unit hour. For more information, go to the [Catalog](https://cloud.ibm.com/catalog#services) and search for `Event Streams`. You can then view pricing plans.

Currently, enabling mirroring for an {{site.data.keyword.messagehub}} service instance requires the use of the {{site.data.keyword.cloud_notm}} CLI.

To install the CLI, see [Extending IBM Cloud CLI with plug-ins](/docs/cli?topic=cli-plug-ins).

The {{site.data.keyword.cloud_notm}} CLI uses the **service-instance-update** command to update your {{site.data.keyword.messagehub}} service instance resource. The user ID in the account used to run the **service-instance-update** command must be assigned the same access policies that are needed when you create resources. For information about access requirements, see [Required access for creating resources](/docs/account?topic=account-manage_resource#creating-resources).

The time required to enable mirroring for the {{site.data.keyword.messagehub}} service instance varies, but under normal circumstances it does not exceed 2 hours.

## Setup 
{: #step1_setup}
{: step}

Ensure that you provision two Enterprise plan clusters. Both clusters must have the same throughput and storage capacity and have service-to-service bindings (see [Step 2](#step2_bindings) for more information).

Because mirroring is unidirectional, decide which direction of mirroring you want. One cluster is the source and the other cluster is the target.

Decide which topics from your source cluster you want to mirror. By default, no topics are mirrored and you can enable mirroring by using the user controls after mirroring is enabled as shown in [step 4](#step4_validation). You must specify the selection as one or more patterns.

Consider your bandwidth requirements; is there enough bandwidth available in the source cluster? Your source cluster needs to have some headroom to run mirroring. See [Choosing your plan](/docs/EventStreams?topic=EventStreams-plan_choose) for cluster bandwidth limits and use [Event Streams metrics](/docs/EventStreams?topic=EventStreams-metrics) to determine how busy your source cluster is and whether it has the headroom for mirroring.

Although mirroring from an Enterprise multi-zone-region cluster to an Enterprise single-zone-region cluster and vice versa is allowed, this configuration is not recommended unless you have specific residency requirements and are aware of the implications. The Service Level Agreement (SLA) policy of an Enterprise multi-zone-region cluster to an Enterprise single-zone-region cluster might be lower or vice versa. 
{: important}

## Enable service-to-service bindings
{: #step2_bindings}
{: step}

You must configure a service-to-service binding between both instances to allow both instances to communicate. To configure, complete the following steps:

When you create a service-to-service binding, IAM uses the terminology 'source' and 'target' in the opposite way to that of {{site.data.keyword.messagehub}}. In that the IAM source account contains the {{site.data.keyword.messagehub}} mirroring target instance, and vice-versa.
{: note}

1. Select the IBM Cloud account containing the {{site.data.keyword.messagehub}} mirroring source service instance.
2. Navigate to the **Authorizations** panel in IAM and click **Create**. 
3. For the **Source** section:
    - If you are mirroring to a target instance in a different account, select "another account" under the source heading, then pick the account containing the mirroring target instance. If you a mirroring between service instances in the same account, you can leave the default of "this account" selected.
    - Select the mirroring target {{site.data.keyword.messagehub}} instance as the IAM source service instance.
4. For the **Target** selection, select the mirroring source {{site.data.keyword.messagehub}} instance as the IAM target service instance.
5. Assign the **Reader** role and click **Authorize**.

If your requirement is to fail back, you also need the service-to-service binding in the opposite direction.
{: important}

The following example shows how to use the command line to configure service-to-service binding. 

1. Log in to the IBM Cloud account containing the {{site.data.keyword.messagehub}} instance that you want to act as the mirroring source instance:
   
    ```sh
    ibmcloud login -c <account containing mirroring source instance>
     ```
    {: codeblock}

3. Set up an authorization policy, as follows:
   
    ```sh
    ibmcloud iam authorization-policy-create messagehub messagehub Reader --source-service-instance-id <instance id of the mirroring target cluster> [--source-service-account <account containing mirroring target instance>] --target-service-instance-id <instance id of the mirroring source cluster>
    ```
    {: codeblock}
   
    Note that the `--source-service-account` option can be omitted if you are setting up mirroring between two {{site.data.keyword.messagehub}} instances in the same IBM Cloud account.

For more information about service-to-service bindings, see the [**Manage authorizations** panel](https://cloud.ibm.com/iam/authorizations) and [Using authorizations to grant access between services](/docs/account?topic=account-serviceauth).

## Enable mirroring and select the topics to mirror
{: #step3_enable}
{: step}

To enable mirroring, you need to run a **`service-instance-update`** command against your target cluster by using the CLI with the following required parameters:

| Required parameters | Description |
| ---------- | ----------- |
| source_crn | The crn of the source cluster to be mirrored |
| source_alias | The alias used for the source cluster | 
| target_alias | The alias used for the target cluster | 
{: caption="Required parameters when enabling mirroring" caption-side="bottom"}

- The `source_crn` is in this format: `crn:v1:bluemix:public:messagehub:us-south:a/aaa:aaaa::`
- The `source_alias` and the `target_alias` are the aliases that you want to configure for each of the two service instances when you enable mirroring. The aliases appear in topic names. Choose short and descriptive names. For example, "us-south" and "us-east".

### Example CLI command
{: #example_cli_command}

```sh
ibmcloud resource service-instance-update "Event Streams resource instance name" -p '{"mirroring":{"source_crn":"<source_crn>", "source_alias":"<source_alias>", "target_alias":"<target_alias>"}}'
```
{: codeblock}

### Select the topics to mirror
{: #select_topics}
{: step}

When the service instance update is complete, you must select which topics will be mirrored from the source to the target cluster. This is done with the CLI by using the 'ibmcloud es mirroring-topic-selection-set' command. Any consumer groups used to consume from these selected topics will be mirrored from the source to the target cluster.
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

After topic selection is complete, the target cluster shows the topics that are selected for mirroring using the **Mirroring user controls** suffixed with the source cluster's alias.

### Step 3.1: Specify how topic and group names are transformed
{: #renametopics}

You can specify transformation rules that allow you to mirror data into topics with different names in the target cluster. The following three scenarios describe possible transformations, and explain the use-cases for each.

You can specify which topics or consumer groups are mirrored at anytime once mirroring has been enabled, however topic or group transformation is only possible at the point mirroring is enabled. If mirroring is already enabled, it will need to be disabled first before a subsequent enable request is made to specify topic or group transformation.
{: note}

### Scenario 1: Transforming topics by removing the old prefix or suffix and adding a new prefix or suffix
{: #transformtopic_1}

Configure the following four additional parameters.

| Required parameters for topic renaming | Description | 
| -- | -- |
| remove_prefix | the prefix to remove from topic names in the source cluster |
| remove_suffix | the suffix to remove from topic names in the source cluster |
| add_prefix | the prefix to add to topic names in the target cluster |
| add_suffix | the suffix to add to topic names in the target cluster |

The `ibmcloud resource service-instance-update` command needs to be specified via the `-p` command line argument. When these options are specified, only topics with the matching prefixes or suffixes will be eligible for mirroring. For example, if you have a `remove_prefix` of `app1-`, and specify a topic selection of `abc.*`, only topics that start with `app1-abc` will be mirrored.

If you specify the "rename" type of transformation and don't specify either the parameters for `add_prefix` or `add_suffix`, the mirrored topic in the target cluster will have these parameters removed. Topic patterns are applied to the topic name after any source prefix or suffix is removed and before any prefix or suffix has been added.

See the following CLI command example:

```sh
{
  "mirroring": {
    "source_crn": "crn:v1:...",
    "source_alias": "source",
    "target_alias": "target",
    "options": {
      "topic_name_transform": {
        "type": "rename",
        "rename": {
          "add_prefix": "newprefix-",
          "remove_prefix": "oldprefix-",
          "add_suffix": "-newsuffix",
          "remove_suffix": "-oldsuffix"
        }
      }
    }
  }
}
```
{: pre}

### Scenario 2: Adding the source alias as a suffix to mirrored topics
{: #transformtopic_2}

Apply a topic name transformation with the topic_name_transform type set to `use_alias`. With this configuration, a topic called `app1-topic` in the source cluster will be mirrored to a topic called `app1-topic.source` in the target cluster, because the source alias specified in the configuration is `source`.

See the following CLI command example:

```sh
{
  "mirroring": {
    "source_crn": "crn:v1:...",
    "source_alias": "source",
    "target_alias": "target",
    "options": {
        "topic_name_transform": {
            "type": "use_alias"
      }
    }
  }
}
```
{: pre}

### Scenario 3: Topics are mirrored with their names unchanged
{: #transformtopic_3}

In this scenario, you also apply the `topic_name_transform` with the type set to `none`. With this configuration, a topic called `app1-topic` in the source cluster will be mirrored to a topic called `app1-topic` in the target cluster.

See the following CLI command example:

```sh
{
  "mirroring": {
    "source_crn": "crn:v1:...",
    "source_alias": "source",
    "target_alias": "target",
    "options": {
        "topic_name_transform": {
            "type": "none"
      }
    }
  }
}
```
{: pre}

### Step 3.2: Transforming corresponding consumer group IDs
{: #transformgroupid}

By default, Mirror Maker will not modify consumer group IDs when mirroring to the target cluster. However, {{site.data.keyword.messagehub}} allows you to modify group IDs' data, as outlined in the following two scenarios. Similar to topics, group ID patterns are applied after removing any source prefix or suffix and before adding any prefix or suffix. If you specify the "rename" type of transformation and don't specify either the parameters for `add_prefix` or `add_suffix`, the mirrored group ID in the target cluster will have these parameters removed.

The `ibmcloud resource service-instance-update` command needs to be specified via the `-p` command line argument.

### Scenario 1: Transform group ID by removing the old prefix or suffix and adding a new prefix or suffix
{: #transformgroupid_1}

Configure the following four additional parameters.

| Required parameters for group ID renaming | Description |
| -- | -- |
| remove_prefix | the prefix to remove from group id in the source cluster |
| remove_suffix | the suffix to remove from group id in the source cluster |
| add_prefix | the prefix to add to group id in the target cluster |
| add_suffix | the suffix to add to group id in the target cluster |

When these options are specified, only group IDs with the matching prefixes or suffixes will be eligible for mirroring. For example, if you have a `remove_prefix` of `aaa` and `add_prefix` of `bbb`, consumer groups that start with `aaa-group-id` in the source cluster will be mirrored to `bbb-group-id` in the target cluster.

See the following CLI command example:

```sh
{
  "group_id_transform": {
    "type": "rename",
    "rename": {
       "add_prefix": "newprefix-",
       "remove_prefix": "oldprefix-",
       "add_suffix": "-newsuffix",
       "remove_suffix": "-oldsuffix"
    }
  }
}
```
{: pre}

### Scenario 2: Consumer group IDs are mirrored with their names unchanged
{: #renamegroupid_2}

In this scenario, you also apply the `topic_name_transform` with the type set to `none`. With this configuration, a topic called `aaa-group-id` in the source cluster will be mirrored to a topic called `aaa-group-id` in the target cluster.

See the following CLI command example:

```sh
"group_id_transform": {
  "type": "none"
}
```
{: pre}


## Schema Migration Approaches in Event Streams
{: #schema migration}
{: step}

Event Streams provide two approaches to schema migration, each utilising a different strategy. 

1. Bulk Schema Import/Export Tool: This method preserves schema IDs exactly as they exist in the source cluster.  Use this approach where no transformations are taking place between the source and target clusters or for straight forward lift and shift scenarios where schema compatability must be maintained end to end. [Find out more.](/docs/EventStreams?topic=EventStreams-ES_schema_registry#importing_data_from_other_schema_registries) 

2. Schema Sync via Mirroring with ID Transformation. This method, [outlined below](/docs/EventStreams?topic=EventStreams-mirroring_setup#schema), transforms schema IDs during migration from source to target cluster. Use this approach for phased migrations, or where transformations are necessary. This method ensures schemas are in sync between registry clusters, meaning consumers on the target cluster can read messages immediately. It also allows new schemas to be registered without risk of ID collisions with schemas that might be migrated later. 

## Schema Synchronization via Mirroring with ID Transformation
{: #schema migration}

Schema sync via mirroring works by forwarding schema registry requests from one instance to another. This enables users to read from and write to a source instance through the target instance, as the target schema registry operates in a special "mirroring mode" - transparently proxying schema-related requests to the source registry and applying ID transformations as needed. This approach simplifies cross-instance data access and supports seamless schema synchronization across environments.

### Cautions
{: #schemamigration_caution}
Before synchronizing schemas using mirroring, review the following precautions:
1. A maintenance window is required while schemas are bulk exported/imported between the
two registries – this would be in the order of a few hours or less.
2. For topic renaming to work, schemas must use Confluent Avro Serdes, so the subject can be derived from the topic name. 
Confluent Avro Serdes because the subject associated with a schema can be derived from
the topic name (E.g., for topic and topic/record subject naming strategies).
3. Mirroring S2S authorization must be uninterrupted; disabling s2s authorization or mirroring will prevent schema registry requests from being forwarded.
4. If transformation is required, the target instance schema registry must be configured with topic renaming rules before any migration takes place.
5. Renaming rules cannot be changed until migration is complete. Making changes during migration will result in inconsistencies between registries.


### Instructions
{: #schemamigration_caution}
The following instructions outline how you can use schema registry mirroring to move schemas between two instances.

An export utility has not yet been added to the CLI.
{: note}

#### Permitted schemas values 
| Value | Description | 
| -- | -- |
| proxied | Requests are forwarded from the target instance to the source instance. |
| read-only | Requests requiring the Reader IAM role are permitted. All others are rejected (403). |
| inactive/omitted | Request forwarding is disabled. Default. |

#### Example request

See the following CLI command example:

```sh
ibmcloud resource service-instance-update \
"trgt-instance-name" \
-p '{
"mirroring": {
"source_crn": "<src instance crn>",
"source_alias": "source",
"target_alias": "target",
"schemas": "proxied"
}
}'
```
{: pre}

### Topic Name Transformation 
{: #schemamigration_topicnametransformation}

Topic names can be transformed during forwarding. For example, with the right rules,`old-my-topic` could become `new-my-topic`. When enabled, the source instance only recognises the
original name, whilst the target instance only recognises the new/transformed topic name. All
results returned are transformed accordingly.

If no transformation rules are supplied, `use_alias` is used, in line with existing mirroring behaviour
in Event Streams. To forward without changing topic names, [use `topic_name_transform` type `none`](/docs/EventStreams?topic=EventStreams-mirroring_setup#transformtopic_3).
Transformation is configured using the [existing CLI transformation fields](/docs/EventStreams?topic=EventStreams-mirroring_setup#transformtopic_1).

### Migration Flow 
{: #schemamigration_migration flow}
When migrating between two Event Streams instances, the following flow is suggested.
1. Enable mirroring between two instances, specifying `schemas: proxied`.
2. Update your applications to use the target schema registry.
3. Block any writes to the target registry by switching to `schemas: read-only`. Before
making this change, mirroring must be disabled momentarily.
4. Export all schemas from the source instance.
5. Import all schemas exported from the source instance into the target. This can be done
using the IBM Cloud CLI: `ibmcloud [...]`
6. Disable mirroring. Complete.

### Exporting schemas
{: #schemamigration_export}

For more detailed information, see the [Confluent
documentation](https://docs.confluent.io/platform/current/schema-registry/sr-client-configs.html). 

Note: the Event Streams CLI requires that schema imports have a `v1` `exportVersion` value.
1. Download latest `v2.x.x` source code, e.g: https://github.com/Apicurio/apicurio-registry/archive/refs/tags/2.6.13.Final.zip.
2. Build the export client: `mvn -pl utils/exportConfluent -am -DskipTests -Pprod package`
3. Run the exporter (saves output to confluent-schema-registry-export.zip):
```sh 
java -jar utils/exportConfluent/target/apicurio-registry-utils-exportConfluent-2.6.13.Final.jar \
"https://token:<password>@<my-event-streams-instance.com>/confluent" \
--client-props basic.auth.credentials.source=URL
``` 

### Importing schemas
{: #schemamigration_import}

Schemas can be imported using the IBM Cloud CLI.
1. Ensure you have the `event-streams[es]` plugin installed: `ibmcloud plugin list`
2. Login to IBM Cloud: `ibmcloud login [...]`
3. Initialize the Event Streams instance you'd like to import in to: `ibmcloud es init`
4. Import the schema:
``` sh 
ibmcloud es schema-import \
-f confluent-schema-registry-export.zip
```

## Validation
{: #step5_validation}
{: step}

You can get the current service instance information by running the following command:

```sh
ibmcloud resource service-instance "Event Streams resource instance name" --output=json
```
{: codeblock}

Review the **last operation** section of the output. The information is continuously updated as the update proceeds. When the mirroring enablement process is complete, the last operation information indicates whether the update succeeded or the sync succeeded.

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
