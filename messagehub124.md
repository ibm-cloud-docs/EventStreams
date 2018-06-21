---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Securing your {{site.data.keyword.messagehub}} resources (Enterprise plan)
{: #security }

You can secure your {{site.data.keyword.messagehub}} resources in a fine-grained manner to manage the access that you want to grant each user to each resource.

## What can I secure?

Within {{site.data.keyword.messagehub}}, you can secure access to the following resources:
* Cluster (cluster): you can control which applications and users can connect to the service [and access the UI] 
* Topics (topic): you can control the ability of users and applications to create, delete, read, and write to a topic 
* Consumer groups (group): you can control an application's ability to join a consumer group 
* Producer transactions (txnid): you can control the ability to use the transactional producer capability in Kafka 

The levels of access (also known as a role) that you can assign to a user to each resource are as follows:
* read
* write
* manage

<!-- comment from Charlie and my reply 
CM: need to confirm if hierarchical e.g. write includes read - and doc. 
KR: I think they do inherit the lower level access https://console.bluemix.net/docs/iam/users_roles.html#iamusermanrol 
-->


## How do I assign access?

Cloud Identity and Access Management (IAM) policies are attached to the resources to be controlled. Each policy defines the level of access that a particular user should have and to which resource or set of resources. A policy consists of the following information: 
* The type of service the policy applies to. For example, Message Hub. You can scope a policy to include all service types. 
* The instance of the service to be secured. You can scope a policy to include all instances of a service type. 
* The type of resource to be secured. For example, <code>cluster</code>, <code>topic</code>, <code>group</code>, or <code>txnid</code>. Specifying a type is optional. If you do not specify it, the policy then applies to all resources in the service instance. 
* The role assigned to the user. For example, Reader, Writer, or Manager. 

## What are the default security settings?

By default, when {{site.data.keyword.messagehub}} is provisioned, the user who provisioned it is granted the manager role to all the instance's resources. Additionally, any user who has a manager role for either 'All' services or 'All' Message Hub service instances' in the same account also has full access. &lt;&lt;is this actually manager role or admin role?&gt;&gt;

You can then apply additional policies to extend access to other users. You can either scope a policy to apply to {{site.data.keyword.messagehub}} as a whole or to individual resources within {{site.data.keyword.messagehub}}. For more information, see [Common scenarios](#security_scenarios).

Only users with an administration role for an account can assign policies to users . Assign policies either by using IBM Cloud dashboard or by using the **ibmcloud** commands. For example steps for {{site.data.keyword.messagehub}}, see [Examples](#security_examples).


## Common scenarios
{: #security_scenarios }

This table summarizes some common {{site.data.keyword.messagehub}} scenarios and the access you need to assign:

| Action | Reader role | Writer role | Manager role |
|---------|----------------|
| Allow full access to all resources|   |  |Service instance|
| Allow an app or user to create or delete topic |Cluster resource type    |  |Each topic resource type <br/><br/>Each topic name resource |
| List groups, topics, and offsets <br/> Describe group, topic, and broker configurations | Cluster resource type      |  |      |
| Allow an app to connect to the cluster  |Cluster resource type|      |      |
| Allow an app to produce to topics  |Cluster resource type|Each topic resource type <br/><br/>Each topic name resource|      |
| Allow an app to write to a topic  |Cluster resource type|Topic resource       |     |
| Allow an app to connect and consume from a specific topic (no consumer group)  |Cluster resource type <br/>Named topic resource |       |     |
| Allow an app to connect and consume from any topic (no consumer group)  | Cluster resource <br/>Topic resource |     |     |
| Allow an app to consume a topic (consumer group)  |Cluster resource type <br/>Topic resource <br/> Group resource<br/>Group ID resource|      |     |
| Allow an app to produce to a topic transactionally  |Cluster resource type Group resource type<br/>Group ID resource|Each topic resource type <br/>Each topic name resource <br/>Transaction ID resource type <br/>Transaction ID resource|     |
| Allow a user access to the UI|Cluster resource type - &lt;&lt;is this true, it looks like if you have the operator platform role you may see the UI but *may* not be able to see the list of topics - which would be a defect!&gt;&gt;     |  |
| Delete consumer group |Cluster resource type |  |Group resource type <br/>Group ID resource      |
| To use streams |?| ? |?     |
| Do we need to cover creating/deleting an instance of Message Hub?? [this is slightly different as not a service role as in everything else here, but a platform role] &gt;&gt;   |? | ? |?     |


## Examples
{: #security_examples }

I want to give a user access to create or delete a topic:

1. From the IBM Cloud dashboard, go to the **Manage** tab &gt; **Security** &gt; **Identity and Access**, and then select **Users**.
2. Click **Invite users**.
3. Specify the email address of the user that you want to invite.
4. In the **Access** section, expand the **Services** option.
5. Choose to assign access to a **Resource**.
6. In the **Services** section, select **Message Hub**
7. In the **Region** section, make your selection.
8. In the **Service instance** section, locate your instance and select it.
9. In the **Resource type** section, enter **cluster**.
10. In the **Select roles** section, check the **Reader** box.
11. In the **Resource type** section, enter **topic**.
12. In the **Select roles** section, check the **Manager** box.
13. Click **Invite users**.



For more information about IAM, see 
[IBM Cloud Identity and Access Management](/docs/iam/index.html#iamoverview).









