---

copyright:
  years: 2015, 2019
lastupdated: "2019-05-15"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}

# Upgrading to the new {{site.data.keyword.messagehub}} Standard plan 
{: #migrate_classic_plan}

This new release of the standard multi-tenant brings offers significant improvements in resiliency, functionality, and usability. For more informtion, see [New plan blog announcement ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/blog/announcements/ibm-event-streams-releases-a-new-and-enhanced-standard-plan) 
{: shortdesc}

To migrate applications from the previous Standard plan (now called the Classic plan) to the new plan, consider the following information.

Service instances are now provisioned as {{site.data.keyword.cloud_notm}} Services rather then Cloud Foundry Services. This enables the service to support the latest {{site.data.keyword.cloud_notm}} standards and capabilities, including multi-zone deployments and granular access controls, but has implications for how the service is used. In particular:

* **Creating, deleting, and listing services**
    As previously, the lifecycle of services can be managed using either the {{site.data.keyword.cloud_notm}} portal or the {{site.data.keyword.cloud_notm}} CLI command line tool. If the portal is used, services are now listed under 'Services' rather then 'Cloud Foundry Services'. If the CLI is used, instances are managed using the resource commands for example,  ```ibmcloud resource service-instance-create``` rather then the cf commands, for example ```ibmcloud cf create-service```.

* **Controlling access**
    Authentication and authorization is now managed using the Cloud Identity and Access Management (IAM) service. As well as controlling a user's ability to connect, IAM also enables granular access to underlying resources, such as topics, to be configured. Access is controlled by assigning policies to users. For more information, see 
    [Managing access to your {{site.data.keyword.messagehub}} resources](/docs/services/EventStreams?topic=eventstreams-security).

* **Connecting Applications**
    The information an application needs to connect has not changed, that is, a list of 'bootstrap.servers', 'username' and 'password'. However, the way these properties are retrieved has changed.

* **For native applications**
    You must create a Credentials or Service Key object using either the IBM Cloud console or CLI respectively, from which the above properties can be retrieved 
    [Connecting applications](/docs/services/EventStreams?topic=eventstreams-connecting#connect_enterprise_external).
    

* **For Cloud Foundry applications**
    The service must first be bound to the applications organisation and space by creating a service alias. The above properties can then be retrieved from the VCAP_SERVICES environment variable in the normal way, for further information see 
    [Connecting to {{site.data.keyword.messagehub}}](/docs/services/EventStreams?topic=eventstreams-connecting).

Other changes to be aware of:

* **Kafka version**
    This plan provides access to the latest stable Kafka release 2.2. Applications developed against Kafka 1.1 can run unchanged, but refer to the following information for recommended client versions: <Using the Kafka API> for information on tested combinations.
    [Choosing a Kafka client to use with {{site.data.keyword.messagehub}} {{site.data.keyword.messagehub}}](/docs/services/EventStreams?topic=eventstreams-kafka_using#kafka_clients).


* **Supported regions**
    The plan will initially be available in us-south only. The remaining regions will be introduced over the coming few weeks.

* **Integrations**
    Connection from other services, such as {{site.data.keyword.iot_short_notm}} or {{site.data.keyword.openwhisk_short}}, which bind to the service using a Cloud Foundry organization and space will require a service alias to be created. For further information, see
    [Connect Cloud Foundry applications {{site.data.keyword.messagehub}}](/docs/services/EventStreams?topic=eventstreams-connecting#connect_enterprise_cf).
    

* **Supported capabilities**
    There are differences in the capabilities between the Classic plan and the new Standard plan. To align the product offerings, adopt new technology choices and remove less used features, not all capabilities are carried forward. A comparison of the features is available at [Choosing your plan](/docs/services/EventStreams?topic=eventstreams-plan_choose). If you rely on these functions, further information will be provided shortly to help migrate.
   
Small code deltas are shipped daily to production, as a result, you can expect to see many further improvements to our user experience (and other areas) throughout the rest of 2019 and beyond. Coming soon:

* **Customer metrics**
    The ability to monitor activity in a service instance.




