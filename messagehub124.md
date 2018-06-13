---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Securing your {{site.data.keyword.messagehub}} resources (Enterprise plan)
{: #security }

You can secure your {{site.data.keyword.messagehub}} resources in a fine-grained method to manage the access that you want to grant each user to each resource.

## What can I secure?

Within a service instance, you can secure access to the following resources:
* Cluster (cluster): you can control which applications and users can connect to the service [and access the UI] 
* Topics (topic): you can control the ability of users and applications to create, delete, read, and write to a topic 
* Consumer groups (group): you can control an application's ability to join a consumer group 
* Producer transactions (txnid): you can control the ability to use the transactional producer capability in Kafka 

The levels of access (role) that you can assign to a user to each resource are as follows:
* read
* write
* manage. &lt;&lt;need to confirm if hierarchical e.g. write includes read - and doc. I think they do inherit the lower level access https://console.bluemix.net/docs/iam/users_roles.html#iamusermanrol &gt;&gt;


## How do I assign access?

Cloud Identity and Access Management (IAM) policies are attached to the resources to be controlled. Each policy defines the level of access (service role) a particular user should have and to which resource or set of resources. A policy consists of the following information: 
* The type of service the policy applies to. For example, Message Hub. You can scope a policy to include all service types. 
* The instance of the service to be secured. You can scope a policy to include all instances of a service type. 
* The type of resource to be secured. For example, <code>cluster</code>, <code>topic</code>, <code>group</code>, or <code>txnid</code>. Specifying a type is optional. If you do not specify it, the policy then applies to all resources in the service instance. 
* The role assigned to the user. For example, Reader, Writer, or Manager. 

## What are the default security settings?

By default, when a service instance is provisioned, the user who provisioned it is granted the manager role to all the instance's resources. Additionally, any user who has a manager role for either 'All' services or 'All' Message Hub service instances' in the same account also has full access. &lt;&lt;is this actually manager role or admin role?&gt;&gt;

You can then apply additional policies to extend access to other users. You can either scope a policy to apply to the service instance as a whole or to individual resources within the service instance. For more information, see common scenarios.

You can only assign policies by users with an administration role for an account. They can either be assigned using the portal &lt;&lt;link&gt;&gt; or by using the bx command &lt;&lt;details&gt;&gt;

Further details on IAM &lt;&lt;link&gt;&gt; 

## Recommendations



## Common scenarios
{: #security_scenarios }

| Action | Reader role | Writer role | Manager role |
|---------|----------------|
| Create or delete topic |Cluster resource type    |  |<ul><li>Each topic resource type</li><li>Each topic name resource</li></ul> |
| List groups, topics, and offsets, and describe group, topic, and broker configurations | Cluster resource type      |  |      |
| Groups |      |  |      |
| Transactions  |      |  |      |

* To allow full access to all resources, assign [Manager role on the service instance] 
* To allow a user access to the UI, assign [Reader role on the 'cluster' resource &lt;&lt;is this true, it looks like if you have the operator platform role you may see the UI but *may* not be able to see the list of topics - which would be a defect!&gt;&gt;] 
* To allow an application to connect to the cluster, assign [Reader role on the 'cluster' resource] 
* To allow a user or app to create and delete topics, assign [Reader role on the 'cluster' resource and (manager role on the 'topic' resource)] 
* To allow an application to connect and consume (no group) from a particular topic, assign [Reader role on the 'cluster' resource and named 'topic' resource] 
* To allow an application to connect and consume (no group) from any topic, assign [Reader role on the 'cluster' resource and 'topic' resource] 
* To allow an application to connect and consume (group) from a topic, assign [Reader role on the 'cluster' resource, 'topic' resource and 'group' resource] 
* To allow an application to write to a topic, assign [Reader role on the 'cluster' resource and writer role on the 'topic' resource] 
* To use streams &lt;&lt;need to check what this needs&gt;&gt; 
&lt;&lt; Do we need to cover Creating/Deleting an instance of Message Hub?? [this is slightly different as not a service role as in everything else here, but a platform role] &gt;&gt; 


Here are some common {{site.data.keyword.messagehub}} scenarios and the access you need to assign:

* If you want a user to create or delete a topic, assign the following:
    * Reader role on the cluster resource type
    * Manager role on each topic resource type and topic name resource

If you want a user to be able to list groups, topics, and offsets, and describe group, topic, and broker configurations, assign the following:
* Reader role on the cluster resource type

If you want a user to be able to be producer to some topics (same for idempotent), assign the following:
* Reader role on the cluster resource type
* Writer role on each topic resource type and topic name resource

If you want a user to be able to be a transactional producer, assign the following:
* Same access as producer plus
* Writer role on transaction ID resource type and transaction ID resource
* Reader role on group resource type and group ID resource

If you want a user to be able to be a consumer (no consumer group), assign the following:
* Reader role on the cluster resource type
* Reader role on each topic resource type and topic name resource

If you want a user to be able to be a consumer with consumer group, assign the following:
* Same access as consumer (no group)
* Reader role on group resource type and group ID resource

If you want a user to be able to delete a consumer group, assign the following:
* Reader role on the cluster resource type
* Manager role on group resource type and group ID resource




For more information about IAM, see: 
[IBM Cloud Identity and Access Management](/docs/iam/index.html#iamoverview).

For an example about how to set policies, see: 
[Introducing IBM Cloud IAM Service IDs and API Keys ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2017/10/introducing-ibm-cloud-iam-service-ids-api-keys/){:new_window}.








