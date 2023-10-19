---

copyright:
  years: 2015, 2023
lastupdated: "2023-10-19"

keywords: client, wildcarding, wildcard, policies

subcollection: EventStreams

---

{{site.data.keyword.attribute-definition-list}}

# Managing authentication to your {{site.data.keyword.messagehub}} instances
{: #security}

{{site.data.keyword.messagehub}} supports 2 [SASL](https://en.wikipedia.org/wiki/Simple_Authentication_and_Security_Layer)(Simple Authentication and Security Layer) mechanisms as the authentication methods to {{site.data.keyword.messagehub}} instances by default: PLAIN and OAUTHBEARER.
{: shortdesc}

Kafka client configured with SASL PLAIN uses IAM API key as a plain text password in the authentication process, {{site.data.keyword.messagehub}} sends API key to IAM for verification. Once authenticated, this client will keep connected and will not require re-authentication until it is disconnected and wants to re-connect.

Kafka client configured with SASL OAUTHBEARER uses IAM access token in the authentication process, {{site.data.keyword.messagehub}} verifies the token via IAM public key. Since IAM access token has expiration time (usually at 1 hour), Kafka client is required to re-generate a new token and go through the authentication process again when previous token is approaching expiration time. This approach provides better security comparing to SASL PLAIN in 2 ways: 1. API key always stays at client side to generate access token and is no longer sent to Kafka brokers over network, this removes the risk of API key exposure. 2. Authentication process happens at a regular basis when access token is expiring, this minimizes the risk of token exposure.

For more secure authentication, SASL OAUTHBEARER is the only recommended authentication method for Kafka clients. See [Configuring your Kafka API client](/docs/EventStreams?topic=EventStreams-kafka_using#kafka_api_client) how to configure SASL OAUTHBEARER in Kafka clients.

Enterprise users have the option to disable SASL PLAIN in their Enterprise instances. Use command:

```sh
ibmcloud resource service-instance-update <instance-name> -p '{"iam_token_only":true}'
```

## Managing authorization to your {{site.data.keyword.messagehub}} resources
{: #security_resources}

You can secure your {{site.data.keyword.messagehub}} resources in a fine-grained manner to manage the access that you want to grant each user to each resource.
{: shortdesc}

When you change IAM policies and permissions, they can sometimes take several minutes to be reflected in the underlying service.
{: important}

## What can I secure?
{: #what_secure}

Within {{site.data.keyword.messagehub}}, you have secure access to the following resources:

- Cluster (cluster): You can control which applications and users can connect to the service.
- Topics (topic): You can control the ability of users and applications to create, delete, read, and write to a topic.
- Consumer groups (group): You can control an application's ability to join a consumer group.
- Producer transactions (txnid): You can control the ability to use the transactional producer capability in Kafka (that is, single, atomic writes across multiple partitions).

The levels of access (also known as a role) that you can assign to a user to each resource are as follows.

| Access role | Description of actions | Example actions |
|:-----------------|:-----------------|:-----------------|
|  Reader | Perform read-only actions within {{site.data.keyword.messagehub}} such as viewing resources. | Allow an app to connect to a cluster by assigning read access to cluster resource type. |
| Writer | Writers have permissions beyond the reader role, including editing {{site.data.keyword.messagehub}} resources. | Allow an app to produce to topics by assigning write access to topic resource and topic name types. |
| Manager | Managers have permissions beyond the writer role to complete privileged actions. In addition, you can create and edit {{site.data.keyword.messagehub}} resources. | Allow full access to all resources by assigning manage access to the {{site.data.keyword.messagehub}} instance.
{: caption="Table 1. Example {{site.data.keyword.messagehub}} user roles and actions" caption-side="bottom"}

## How do I assign access?
{: #assign_access }

Cloud Identity and Access Management (IAM) policies are attached to the resources to be controlled. Each policy defines the level of access that a particular user must have and to which resource or set of resources. A policy consists of the following information:

- The type of service the policy applies to. For example, {{site.data.keyword.messagehub}}. You can scope a policy to include all service types.
- The instance of the service to be secured. You can scope a policy to include all instances of a service type.
- The type of resource to be secured. The valid values are `cluster`, `topic`, `group`, `schema`, or `txnid`. Specifying a type is optional. If you do not specify a type, the policy then applies to all resources in the service instance. If you want to specify more than one type of resource, you must create one policy per resource.
- The resource to be secured. Specify for resources of type `topic`, `group`, `schema`, and `txnid`. If you do not specify the resource, the policy then applies to all resources of the type specified in the service instance.
- The role that is assigned to the user. For example, Reader, Writer, or Manager.

## What are the default security settings?
{: #default_settings }

By default, when {{site.data.keyword.messagehub}} is provisioned, the user who provisioned it is granted the manager role to all the instance's resources. Additionally, any user who has a manager role for either 'All' services or 'All' {{site.data.keyword.messagehub}} service instances' in the same account also has full access.

You can then apply more policies to extend access to other users. You can either scope a policy to apply to {{site.data.keyword.messagehub}} as a whole or to individual resources within {{site.data.keyword.messagehub}}. For more information, see [Common scenarios](#security_scenarios).

Only users with an administration role for an account can assign policies to users. Assign policies either by using IBM Cloud dashboard or by using the **ibmcloud** commands.

## Common actions
{: #common_actions}

The following tables summarize some common {{site.data.keyword.messagehub}} actions and the access that you need to assign.

### Cluster actions
{: #cluster_actions}

With cluster actions, you can determine which applications and users can connect to the service. Another common Kafka term for the cluster resource group is instance. You must have at least Reader role access to the cluster resource to do anything with {{site.data.keyword.messagehub}}. For most actions, access to another resource is necessary in addition.

### Producer actions
{: #producing_actions}

With producer actions, you can control the ability of users and applications to create, delete, read, and write to a topic.

| Producer actions | Topic | Group | Txnid |
| --- | --- | --- | --- |
| Allow an app to produce to a specific topic. | Writer [^tabletext1] |  |  |
| Allow an app to produce to any topic. | Writer |  |  |
| Allow an app to produce to a topic transactionally. | Writer | Reader | Writer |
| Initialize a transaction. |  |  | Writer |
| Commit a transaction. | Writer |  | Writer |
| Abort a transaction. |  |  | Writer |
| Send. | Writer |  | Writer |
| Send offsets to a transaction. |  | Reader | Writer |
{: caption="Table 2. Producer actions" caption-side="bottom"}

[^tabletext1]: Writer on txnid is only required for transactional produce.

### Consumer actions
{: #consumer_actions}

With consumer actions, you can control an application's ability to join a consumer group.

| Consumer actions | Topic  | Group  | Txnid |
| --- | --- | --- | --- |
| Allow an app to consume a topic (consumer group). | Reader | Reader |  |
| Allow an app to connect and consume from \n a specific topic (no consumer group). | Reader |  |  |
| Allow an app to connect and consume from \n any topic (no consumer group). | Reader |  |
| Use Kafka Streams. | Manager | Reader |  |
| Delete consumer group. |  | Manager |  |
| Assign. |  | Reader [^tabletext2] |  |
| Commit async. | Reader | Reader |  |
| Commit sync.| Reader | Reader |  |
| Enforce rebalance. |  | Reader |  |
| Poll. |  | Reader |  |
| Subscribe. |  | Reader |  |
| Unsubscribe. |  | Reader |  |
{: caption="Table 3. Consumer actions" caption-side="bottom"}

[^tabletext2]: Reader on group is only required if the assign causes the consumer to leave its current group.

### Administration actions
{: #administration_actions}

| Administration actions | Topic  | Group  | Txnid |
| --- | --- | --- | --- |
| Alter topic configurations. | Manager |  |  |
| Alter consumer group offsets. | Reader | Reader |  |
| Create partitions. | Manager |  |  |
| Create partitions. | Manager |  |  |
| Create topics. | Manager |  |  |
| Delete consumer group offsets. | Reader | Manager |  |
| Delete consumer groups. |  | Manager |  |
| Delete records. |  | Manager |  |
| Delete topics. |  | Manager |  |
| Describe producers. | Reader |  |  |
| Fence producers. |  |  | Writer |
| Incrementally alter topic configurations. | Manager |  |  |
| Remove members from consumer group. |  | Reader |  |
{: caption="Table 4. Administration actions" caption-side="bottom"}

### Schema Registry actions
{: #schema_registry_actions}

With Schema Registry actions, you can alter the schema version, such as create, update, and delete artifact or artifact versions (Enterprise plan only). Note that *artifact* is the general Kafka term for schemas, and they can also be referred to as *subjects*. For more information, see [Using Event Streams Schema Registry](https://cloud.ibm.com/docs/EventStreams?topic=EventStreams-ES_schema_registry).

| Schema Registry actions | Reader  | Writer  | Manager  |
| --- | --- | --- | --- |
| Get latest artifact. | ![Checkmark icon.](images/checkmark-icon.svg "Feature available")  |   |   |
| List versions. | ![Checkmark icon.](images/checkmark-icon.svg "Feature available") |   |   |
| Get version. | ![Checkmark icon.](images/checkmark-icon.svg "Feature available") |   |   |
| Get metadata by content. | ![Checkmark icon.](images/checkmark-icon.svg "Feature available")  |   |   |
| Get metadata. | ![Checkmark icon.](images/checkmark-icon.svg "Feature available") |   |   |
| Get version metadata. | ![Checkmark icon.](images/checkmark-icon.svg "Feature available") |   |   |
| Get the schema string identified by the input ID.  | ![Checkmark icon.](images/checkmark-icon.svg "Feature available") |   |   |
| Retrieve only the schema identified by the input ID. | ![Checkmark icon.](images/checkmark-icon.svg "Feature available") |   |   |
| Get the subject-version pairs identified by the input ID. | ![Checkmark icon.](images/checkmark-icon.svg "Feature available") |   |   |
| Get a list of versions registered under the \n specified subject. | ![Checkmark icon.](images/checkmark-icon.svg "Feature available") |   |   |
| Get artifact compatibility rule. | ![Checkmark icon.](images/checkmark-icon.svg "Feature available") |   |   |
| Get a specific version of the schema registered \n under this subject. | ![Checkmark icon.](images/checkmark-icon.svg "Feature available") |   |   |
| Get the schema for the specified version of this subject. | ![Checkmark icon.](images/checkmark-icon.svg "Feature available") |   |   |
| Register a new schema under the specified subject \n (if version already exists). | ![Checkmark icon.](images/checkmark-icon.svg "Feature available") |   |   |
| Check if a schema has already been registered \n under the specified subject. | ![Checkmark icon.](images/checkmark-icon.svg "Feature available") |   |   |
| Get a list of IDs of schemas that reference the schema \n with the given subject and version.  | ![Checkmark icon.](images/checkmark-icon.svg "Feature available") |   |   |
| Test input schema against a particular version \n of a subject’s schema for compatibility. | ![Checkmark icon.](images/checkmark-icon.svg "Feature available") |   |   |
| Perform a compatibility check on the schema \n against one or more versions in the subject. | ![Checkmark icon.](images/checkmark-icon.svg "Feature available") |   |   |
| Get compatibility level for a subject. | ![Checkmark icon.](images/checkmark-icon.svg "Feature available") |   |   |
| Register a new schema under the specified subject \n (if version is to be created). |  | ![Checkmark icon.](images/checkmark-icon.svg "Feature available")  |   |
| Create artifact. |   | ![Checkmark icon.](images/checkmark-icon.svg "Feature available")  |   |
| Update artifact. |   | ![Checkmark icon.](images/checkmark-icon.svg "Feature available")  |   |  
| Disable artifact. |   | ![Checkmark icon.](images/checkmark-icon.svg "Feature available")  |   | 
| Create version. |   | ![Checkmark icon.](images/checkmark-icon.svg "Feature available")  |   |
| Delete version. |   |   | ![Checkmark icon.](images/checkmark-icon.svg "Feature available") |
| Update artifact state. |   |   | ![Checkmark icon.](images/checkmark-icon.svg "Feature available")  |
| Update version state. |   |   | ![Checkmark icon.](images/checkmark-icon.svg "Feature available") |
| Delete artifact. |   |   | ![Checkmark icon.](images/checkmark-icon.svg "Feature available")  |
| Create artifact compatibility rule. |   |   | ![Checkmark icon.](images/checkmark-icon.svg "Feature available") |
| Update artifact compatibility rule. |   |   | ![Checkmark icon.](images/checkmark-icon.svg "Feature available") |
| Update compatibility level for the specified subject. |   |   | ![Checkmark icon.](images/checkmark-icon.svg "Feature available") |
| Delete artifact compatibility rule. |   |   | ![Checkmark icon.](images/checkmark-icon.svg "Feature available") |
| Deletes the specified subject and its associated \n compatibility level if registered. |   |   | ![Checkmark icon.](images/checkmark-icon.svg "Feature available") |
| Delete a specific version of the schema \n registered under this subject. |  |   | ![Checkmark icon.](images/checkmark-icon.svg "Feature available") |
| Delete the specified subject-level compatibility level \n config and reverts to the global default. |   |   | ![Checkmark icon.](images/checkmark-icon.svg "Feature available") |
{: caption="Table 5. Schema Registry actions" caption-side="bottom"}

### TransactionId actions 
{: #transactionId_actions}

With TransactionId actions (txnid), you can control the ability to use the transactional producer capability in Kafka (that is, single, atomic writes across multiple partitions). TransactionId actions are also referred to as *producer transactions*.

| TransactionId actions | Reader  | Writer  | Manager  |
| --- | --- | --- | --- |
| Create transactionId. |  | ![Checkmark icon.](images/checkmark-icon.svg "Feature available") |  |
| Initialize producerId transaction. |  | ![Checkmark icon.](images/checkmark-icon.svg "Feature available") |  |
| Add partitions to transactionId. |  | ![Checkmark icon.](images/checkmark-icon.svg "Feature available") |  |
| Add offsets to transactionId. |  | ![Checkmark icon.](images/checkmark-icon.svg "Feature available") |  |
| End transactionId. |  | ![Checkmark icon.](images/checkmark-icon.svg "Feature available") |  |
| Transaction offset commit. |  | ![Checkmark icon.](images/checkmark-icon.svg "Feature available") |  |
{: caption="Table 6. TransactionId actions" caption-side="bottom"}

For more information about IAM, see [IBM Cloud Identity and Access Management](/docs/account?topic=account-iamoverview).

For an example of how to set policies, see [IBM Cloud IAM Service IDs and API Keys](https://www.ibm.com/cloud/blog/introducing-ibm-cloud-iam-service-ids-api-keys){: external}.

## Wildcarding
{: #wildcarding }

You can take advantage of the IAM wildcarding facility to set policies for groups of resources on {{site.data.keyword.messagehub}}. For example, if you give all your topics names like `Dept1_Topic1` and `Dept1_Topic2`, you can set policies for topics that are called `Dept1_*` and these policies are applied to all topics with that prefix. For more information, see [Assigning access by using wildcard policies](/docs/account?topic=account-wildcard){: external}.

## Connecting to {{site.data.keyword.messagehub}}
{: #connect_message_enterprise }

For more information about how to get a security key credential for an external application, see [Connecting to {{site.data.keyword.messagehub}}](/docs/EventStreams?topic=EventStreams-connecting).

## Managing access to the schema registry
{: #managing_access_schemas}

The authorization model for the schema registry used the same style of policies that are described in the [Managing Access To {{site.data.keyword.messagehub}} Resources](#security) section of this document.

### IAM resources
{: #iam_resources}

With the new `schema` IAM resource type, it is possible to create policies that control access by using varying degrees of granularity, as in the following examples.

- A specific schema.
- A set of schemas selected by a wildcard expression.
- All of the schemas stored by an instance of IBM {{site.data.keyword.messagehub}}.
- All of the schemas stored by all of the instances of IBM {{site.data.keyword.messagehub}} in an account.

{{site.data.keyword.messagehub}} already has the concept of a cluster resource type. It is used to control all access to the service instance, with the minimum role of Reader being required to access any Kafka or HTTPS endpoint. This use of the cluster resource type is also applied to the schema registry whereby a minimum role of Reader is required to access the registry.

### Example authorization scenarios
{: #example_authorization_scenarios}

The following table describes some examples of scenarios for interacting with the {{site.data.keyword.messagehub}} schema registry, together with the roles that are required by the actors involved. The process of managing schemas is handled separately to deploying applications. So policies are required for both the service ID that manages schemas in the registry and the application that connects to the registry.

Scenario | Person or process role | Person or process resource| Application role | Application resource
--- | --- | --- | --- | ---
 New schema versions are placed into the registry by a person or process that is separate from the applications that use the schemas.| `Reader`  \n `Writer`| `cluster`  \n `schema` | `Reader`  \n `Reader` | `cluster`   \n `schema`
Adding a schema to the registry needs to specify a nondefault rule that controls how versions of the schema are allowed to evolve. |`Reader`  \n `Manager` | `cluster`  \n `schema` | Not applicable |  Not applicable
Schemas are managed alongside the application code that uses the schema. New schema versions are created at the point that an application tries to use the new schema version. | Not applicable | Not applicable | `Reader`  \n `Writer`| `cluster`  \n `schema`
The global default rule that controls schema evolution is changed. | `Manager` | `cluster` | Not applicable | Not applicable
{: caption="Table 3. Examples authorization scenarios" caption-side="bottom"}
