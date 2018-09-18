---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-04"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Managing access to your {{site.data.keyword.messagehub}} resources (Enterprise plan)
{: #security }

You can secure your {{site.data.keyword.messagehub}} resources in a fine-grained manner to manage the access that you want to grant each user to each resource.

## What can I secure?

Within {{site.data.keyword.messagehub}}, you can secure access to the following resources:
* Cluster (cluster): you can control which applications and users can connect to the service
* Topics (topic): you can control the ability of users and applications to create, delete, read, and write to a topic 
* Consumer groups (group): you can control an application's ability to join a consumer group 
* Producer transactions (txnid): you can control the ability to use the transactional producer capability in Kafka (that is, single, atomic writes across multiple partitions)

The levels of access (also known as a role) that you can assign to a user to each resource are as follows:

| Access role | Description of actions | Example actions |
|:-----------------|:-----------------|:-----------------|
|  Reader | Perform read-only actions within {{site.data.keyword.messagehub}} such as viewing resources | Allow an app to connect to a cluster by assigning read access to cluster resource type |
| Writer | Writers have permissions beyond the reader role, including creating and editing {{site.data.keyword.messagehub}} resources. | Allow an app to produce to topics by assigning write access to topic resource and topic name types|
| Manager | Managers have permissions beyond the writer role to complete privileged actions. In addition, you can create and edit {{site.data.keyword.messagehub}} resources. | Allow full access to all resources by assigning manage access to the {{site.data.keyword.messagehub}} instance|
{: caption="Table 1. Example {{site.data.keyword.messagehub}} user roles and actions" caption-side="top"}

<!-- comment from Charlie and my reply 
CM: need to confirm if hierarchical e.g. write includes read - and doc. 
KR: I think they do inherit the lower level access https://console.bluemix.net/docs/iam/users_roles.html#iamusermanrol 
-->


## How do I assign access?

Cloud Identity and Access Management (IAM) policies are attached to the resources to be controlled. Each policy defines the level of access that a particular user should have and to which resource or set of resources. A policy consists of the following information: 
* The type of service the policy applies to. For example, {{site.data.keyword.messagehub}}. You can scope a policy to include all service types. 
* The instance of the service to be secured. You can scope a policy to include all instances of a service type. 
* The type of resource to be secured. The valid values are <code>cluster</code>, <code>topic</code>, <code>group</code>, or <code>txnid</code>. Specifying a type is optional. If you do not specify a type, the policy then applies to all resources in the service instance. 
* The resource to be secured. Specify for resources of type <code>topic</code>, <code>group</code> and <code>txnid</code>. If you do not specify the resource, the policy then applies to all resources of the type specified in the service instance. 
* The role assigned to the user. For example, Reader, Writer, or Manager. 

## What are the default security settings?

By default, when {{site.data.keyword.messagehub}} is provisioned, the user who provisioned it is granted the manager role to all the instance's resources. Additionally, any user who has a manager role for either 'All' services or 'All' {{site.data.keyword.messagehub}} service instances' in the same account also has full access. 

You can then apply additional policies to extend access to other users. You can either scope a policy to apply to {{site.data.keyword.messagehub}} as a whole or to individual resources within {{site.data.keyword.messagehub}}. For more information, see [Common scenarios](#security_scenarios).

Only users with an administration role for an account can assign policies to users . Assign policies either by using IBM Cloud dashboard or by using the **ibmcloud** commands. 
<!--
For example steps for {{site.data.keyword.messagehub}}, see [Examples](#security_examples).
-->


## Common scenarios
{: #security_scenarios }

This table summarizes some common {{site.data.keyword.messagehub}} scenarios and the access you need to assign:

| Action | Reader role | Writer role | Manager role |
|---------|----------------|
| Allow full access to all resources|Not applicable   |Not applicable  |Service instance: <var class="keyword varname">your_service_instance</var>|
| Allow an app or user to create or delete topic |Resource type: <code>cluster</code>   |Not applicable  |Resource type: topic <br/><br/>Optional: Resource ID: <var class="keyword varname">name_of_topic</var> |
| List groups, topics, and offsets <br/> Describe group, topic, and broker configurations | Resource type: <code>cluster</code>      |Not applicable  |Not applicable      |
| Allow an app to connect to the cluster  |Resource type: <code>cluster</code>| Not applicable     |Not applicable      |
| Allow an app to produce to any topic  |Resource type: <code>cluster</code>|Resource type: <code>topic</code> |Not applicable     |
| Allow an app to produce to a specific topic  |Resource type: <code>cluster</code>|Resource type: <code>topic</code><br/>Resource ID: <var class="keyword varname">name_of_topic</var>      |Not applicable     |
| Allow an app to connect and consume from any topic (no consumer group)  |Resource type: <code>cluster</code> <br/>Resource type: <code>topic</code> |Resource type: <code>topic</code>|Not applicable     |
| Allow an app to connect and consume from a specific topic (no consumer group)  | Resource type: <code>cluster</code> <br/>Resource type: <code>topic</code><br/>Resource ID: <var class="keyword varname">name_of_topic</var> |Not applicable     |Not applicable     |
| Allow an app to consume a topic (consumer group)  |Resource type: <code>cluster</code> <br/>Resource type: <code>topic</code><br/> Resource type: <code>group</code> |Not applicable      |Not applicable     |
| Allow an app to produce to a topic transactionally  |Resource type: <code>cluster</code> <br/> Resource type: <code>group</code>|Resource type: <code>topic</code> <br/>Resource ID: <var class="keyword varname">name_of_topic</var> <br/>Resource type: <code>txnid</code> |Not applicable     |
| Delete consumer group |Resource type: <code>cluster</code> |Not applicable  |Resource type: <code>group</code> <br/>Resource ID: <var class="keyword varname">group_ID</var>      |
| To use Streams |Resource type: <code>cluster</code></br>Resouce type: <code>group</code>| Not applicable  |Resouce type: <code>topic</code>    |

For more information about IAM, see 
[IBM Cloud Identity and Access Management](/docs/iam/index.html#iamoverview).

For an example of how to set policies, see: 
[IBM Cloud IAM Service IDs and API Keys ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2017/10/introducing-ibm-cloud-iam-service-ids-api-keys/){:new_window}.


## Connecting to {{site.data.keyword.messagehub}}
{: #connect_message_enterprise }

For information about how to bind a Cloud Foundry application or get a security key credential for an external application, see 
[Connecting to {{site.data.keyword.messagehub}}](/docs/services/EventStreams/eventstreams127.html#connect_messagehub).

<!-- 28/06/18 - Karen: draft info only

## Examples
{: #security_examples }

I want to give a user access to create or delete a topic:

1. From the IBM Cloud dashboard, go to the **Manage** tab &gt; **Security** &gt; **Identity and Access**, and then select **Users**.
2. Click **Invite users**.
3. Specify the email address of the user that you want to invite.
4. In the **Access** section, expand the **Services** option.
5. Choose to assign access to a **Resource**.
6. In the **Services** section, select **{{site.data.keyword.messagehub}}**
7. In the **Region** section, make your selection.
8. In the **Service instance** section, locate your instance and select it.
9. In the **Resource type** section, enter **cluster**.
10. In the **Select roles** section, check the **Reader** box.
11. In the **Resource type** section, enter **topic**.
12. In the **Select roles** section, check the **Manager** box.
13. Click **Invite users**.

-->










