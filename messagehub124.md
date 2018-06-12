---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Securing your {{site.data.keyword.messagehub}} resources (Enterprise plan)
{: #alpha_iam }

You can secure your {{site.data.keyword.messagehub}} resources in a fine-grained manner.


## What can I secure?

You can secure access the following resources within a service instance:
* Cluster: to control which applications and users can connect to the service [and access the UI] 
* Topics: to control the ability of users and applications to create, delete, read, and write to a topic 
* Consumer groups: to control the ability for an application to join a consumer group 
Producer transactions: to control the ability to use the transactional produce capability in Kafka 

The levels of access (role) that you can assign to a user to each resource can be one of the following:
* read
* write
* manage. &lt;&lt;need to confirm if hierarchical e.g. write includes read - and doc&gt;&gt;


## How do I assign access?

Cloud Identity and Access Management (IAM) policies are attached to the resources to be controlled. Each policy defines the level of access (service role) a particular user should have and to what resource or set of resources. A policy consists of the following information: 
* The type of service the policy applies to e.g. Message Hub (can be scoped to include all service types) 
* The instance of the service to be secured (can be scoped to include all instances of a service type) 
* The type of resource to be secured e.g. 'cluster', 'topic', 'group' or 'txnid' (optional, if not specified then applies to all resources in the service instance) 
* The role to be assigned to the user e.g. Reader, Writer, or Manager. 

## What are the default security settings?

By default, when a service instance is provisioned, the user who provisioned it is granted the manager role to all its resources. Additionally, any user who has a manager role for either 'All' services or 'All' Message Hub service instances' in the same account also has full access. &lt;&lt;is this actually manager role or admin role?&gt;&gt;

You can then apply additional policies to extend access to other users. These can either be scoped to apply to the service instance as a whole or to individual resources within the service instance. See below for some common scenarios.

You can only assign policies by users with an administration role for an account. They can either be assigned using the portal &lt;&lt;link&gt;&gt; or by using the bx command &lt;&lt;details&gt;&gt;

Further details on IAM &lt;&lt;link&gt;&gt; 

## Recommendations



## Common scenarios


Resource Read Write Manage 
Cluster     create/delete authority to cluster 
Topic ability to consume ability to produce create/ delete topic 
Groups n/a     
Transactions       

  
* To allow full access to all resources [Manager role on the service instance] 
* To allow a user access to the UI [Reader role on the 'cluster' resource &lt;&lt;is this true, it looks like if you have the operator platform role you may see the UI but *may* not be able to see the list of topics - which would be a defect!&gt;&gt;] 
* To allow an application to connect to the cluster [Reader role on the 'cluster' resource] 
* To allow a user or app to create and delete topics [Reader role on the 'cluster' resource and (manager role on the 'topic' resource)] 
* To allow an application to connect and consume (no group) from a particular topic [Reader role on the 'cluster' resource and named 'topic' resource] 
* To allow an application to connect and consume (no group) from any topic [Reader role on the 'cluster' resource and 'topic' resource] 
* To allow an application to connect and consume (group) from a topic [Reader role on the 'cluster' resource, 'topic' resource and 'group' resource] 
* To allow an application to write to a topic [Reader role on the 'cluster' resource and writer role on the 'topic' resource] 
* To use streams &lt;&lt;need to check what this needs&gt;&gt; 
&lt;&lt; Do we need to cover Creating/Deleting an instance of Message Hub?? [this is slightly different as not a service role as in everything else here, but a platform role] &gt;&gt; 





## Older words
{{site.data.keyword.messagehub}} permissions are configured using {{site.data.keyword.iamshort}} IAM policies. An IAM policy consists of the following information:

* a service ID
* an {{site.data.keyword.Bluemix_short}} resource that is defined by a service name, service instance, region, IAM resource type, and IAM resource
* a role (Reader, Writer, or Manager)



## {{site.data.keyword.messagehub}} IAM resources
{: iam_resources}

{{site.data.keyword.messagehub}} exposes four IAM resource types:

* cluster
* topic
* group
* txnid

You can identify unique resources for topic, group, and txnid by setting the IAM resource. The cluster resource type is a singleton, so it does not need to be uniquely identified.

## Common scenarios
{: iam_scenarios}

Here are some common {{site.data.keyword.messagehub}} scenarios and the access you need to assign:

Producer to some topics (same for idempotent):
* Reader role on the cluster resource type
* Writer role on each topic resource type and topic name resource

Transactional producer:
* Same as producer
* Writer role on txnid resource type and transaction ID resource
* Reader role on group resource type and group ID resource

Consumer (no group):
* Reader role on the cluster resource type
* Reader role on each topic resource type and topic name resource

Consumer with group:
* Same as consumer (no group)
* Reader role on group resource type and group ID resource

Create or delete topic:
* Reader role on the cluster resource type
* Manager role on each topic resource type and topic name resource

Delete consumer group:
* Reader role on the cluster resource type
* Manager role on group resource type and group ID resource

List groups, topics and offsets and describe group, topic, and broker configurations
* Reader role on the cluster resource type


For more information about IAM, see: 
[IBM Cloud Identity and Access Management](/docs/iam/index.html#iamoverview).

For an example about how to set policies, see: 
[Introducing IBM Cloud IAM Service IDs and API Keys ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2017/10/introducing-ibm-cloud-iam-service-ids-api-keys/){:new_window}.








