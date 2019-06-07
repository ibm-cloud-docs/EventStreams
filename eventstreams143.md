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

This new release of the Standard multi-tenant plan offers significant improvements in resiliency, functionality, and usability. For more information, see [New Standard plan blog announcement ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/blog/announcements/ibm-event-streams-releases-a-new-and-enhanced-standard-plan). 
{: shortdesc}

To migrate applications from the previous Standard plan (now called the Classic plan) to the new plan, consider the following information.

Service instances are now provisioned as {{site.data.keyword.cloud_notm}} Services rather than as Cloud Foundry Services. This enables the service to support the latest {{site.data.keyword.cloud_notm}} standards and capabilities, including multi-zone deployments and granular access controls, but has implications for how the service is used. In particular, consider the following aspects:

* **Creating, deleting, and listing services**
<br/>
    As before, you can manage the lifecycle of services using either the {{site.data.keyword.cloud_notm}} console or the {{site.data.keyword.cloud_notm}} CLI command line tool. If you're using the console, services are now listed under **Services** instead of **Cloud Foundry Services**. 
    
    If you're using the CLI, instances are managed using the resource commands. For example,  <code>ibmcloud resource service-instance-create</code>. This is instead of the **cf** commands, for example <code>ibmcloud cf create-service</code>.

* **Controlling access**
<br/>
    Authentication and authorization are now managed using the Cloud Identity and Access Management (IAM) service. As well as controlling a user's ability to connect, IAM also enables you to configure granular access to underlying resources, such as topics. Access is controlled by assigning policies to users. For more information, see 
    [Managing access to your {{site.data.keyword.messagehub}} resources](/docs/services/EventStreams?topic=eventstreams-security).

<ul>
<li><strong>Connecting applications</strong>
<br/>
    The information that an application needs to connect has not changed, that is, a list of <code>bootstrap.servers</code>, <code>username</code>, and <code>password</code> are required. However, the way these properties are retrieved has changed.

<ul>
<li>
      <strong>For native applications</strong>
        <br/>
        You must create a Credentials object using the IBM Cloud console or a Service Key object using the CLI. You can then retrieve the required properties. For more information, see 
        [Connecting applications](/docs/services/EventStreams?topic=eventstreams-connecting#connect_enterprise_external).
</li>
<br/>
<li><strong>For Cloud Foundry applications</strong>
        <br/>
        You must first bind the service to the application's organization and space by creating a service alias. You can then retrieve the required properties from the VCAP_SERVICES environment variable as normal. For more information, see 
        [Connecting to {{site.data.keyword.messagehub}}](/docs/services/EventStreams?topic=eventstreams-connecting).
</li>
</ul>
<br/>
Note that clients must support the SNI extension to TLS where the server's hostname is included in the TLS handshake. This feature is commonly available and is supported in all the client versions recommended in [Choosing a Kafka client to use with {{site.data.keyword.messagehub}}](/docs/services/EventStreams?topic=eventstreams-kafka_using#kafka_clients).
</li>
</ul>

<br/>
You should also be aware of some other changes as follows:

* **Kafka version**
<br/>
    This plan provides access to the latest stable Kafka release 2.2. Applications developed against Kafka 1.1 can run unchanged, but refer to the following information for recommended client versions and tested combinations: [Choosing a Kafka client to use with {{site.data.keyword.messagehub}}](/docs/services/EventStreams?topic=eventstreams-kafka_using#kafka_clients). 

* **Supported regions**
<br/>
    The plan is initially available in us-south only. The remaining regions will be introduced over the coming few weeks.

* **Integrations**
<br/>
    Connection from other services, such as {{site.data.keyword.iot_short_notm}} or {{site.data.keyword.openwhisk_short}}, which bind to the service using a Cloud Foundry organization and space require a service alias to be created. For more information, see
    [Connect Cloud Foundry applications to {{site.data.keyword.messagehub}}](/docs/services/EventStreams?topic=eventstreams-connecting#connect_enterprise_cf).
    

* **Supported capabilities**
<br/>
    There are differences between the capabilities of the Classic plan and the new Standard plan. To align the product offerings, adopt new technology choices, and remove less-used features, not all capabilities are carried forward. A comparison of the features is available at [Choosing your plan](/docs/services/EventStreams?topic=eventstreams-plan_choose). If you rely on these functions, further information will be provided shortly to help you migrate.
   
<br/>
Small code deltas are shipped daily to production. As a result, you can expect to see many further improvements to our user experience (and other areas) throughout the rest of 2019 and beyond. Coming soon:

* **Customer metrics**
<br/>
    The ability to monitor activity in a service instance.

<br/>
For a quick walkthrough of the steps to get up and running with the new Standard plan, try the [Getting started tutorial](/docs/services/EventStreams?topic=eventstreams-getting_started).


