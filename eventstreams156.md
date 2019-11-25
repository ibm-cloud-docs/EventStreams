---

copyright:
  years: 2015, 2019
lastupdated: "2019-11-25"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka, responsibilities

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:preview: .preview}

# Understanding your responsibilities with using {{site.data.keyword.messagehub}}
{: #event_streams_responsibilities}
<!-- The title of your H1 should be Understanding your responsibilities with using _service-name_, where _service-name_ is the non-trademarked short version conref. -->

Learn about the management responsibilities and terms and conditions that you have when you use {{site.data.keyword.messagehub_full}}. For a high-level view of the service types in {{site.data.keyword.Bluemix}} and the breakdown of responsibilities between the customer and {{site.data.keyword.IBM_notm}} for each type, see [Shared responsibilities for {{site.data.keyword.cloud_notm}} offerings](/docs/overview?topic=overview-shared-responsibilities).
{:shortdesc}

Review the following sections for the specific responsibilities for you and for {{site.data.keyword.IBM_notm}} when you use {{site.data.keyword.messagehub_full}}. For the overall terms of use, see [{{site.data.keyword.Bluemix}} Terms and Notices](/docs/overview/terms-of-use?topic=overview-terms).

  
## Incident, operations, and cluster management 
{: #incident_ops_cluster}

<!-- Include an introductory sentence or two about this table. Leave the cell blank for the responsible party column if they do not have responsibility for the given task.  -->

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
|Monitor environment|  {{site.data.keyword.messagehub}} performs continuous review, service improvements, code updates, and operational monitoring.  |  |
|High availability|  {{site.data.keyword.messagehub}} provides high availability via multi-zone region deployment  to protect against single points of failure, up to and including a data center loss to achieve the IBM SLA detailed in the {{site.data.keyword.Bluemix}} terms and conditions.  |  |
|Deploy {{site.data.keyword.messagehub}} environment|  {{site.data.keyword.messagehub}} is deployed with IBM recommended best practice configuration options.  For example, replication factor, minimum in sync replicas, throttling, and rack awareness.  | |
|Topic name backup| Topic names are backed up by {{site.data.keyword.messagehub}}  |  |
|Supported client|   | Customer is responsible for maintaining a supported version of the Kafka client. For more information, see [Support summary for all recommended clients](/docs/services/EventStreams?topic=eventstreams-kafka_using#client_summary).|
|Client configuration, deployment, and lifecycle|   | Customer is responsible for managing client configuration, deployment, and lifecycle following [IBM best practice documentation](/docs/overview?topic=overview-shared-responsibilities#software-packages).|
|Cluster management|   | Customer is responsible for managing the provided resource capacity of their clusters across their organizational user base. |
{: caption="Table 1. Responsibilities for incident, operations and cluster management" caption-side="top"}


## Security and regulation compliance
{: #security_compliance}

<!-- Include an introductory sentence or two about this table. Leave the cell blank for the responsible party column if they do not have responsibility for the given task.  -->

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
|Maintain controls| {{site.data.keyword.messagehub}} maintains controls commensurate with various industry compliance standards for which we are certified.  |  |
|IBM Cloud Identity and Access Management (IAM)| {{site.data.keyword.messagehub}} provides security and access control service with IBM Cloud Identity and Access Management (IAM).  |  |
|Security and vulnerability patch updates to cluster| {{site.data.keyword.messagehub}} applies the provided security and vulnerability patch updates to the client cluster, according to IBM X-Force timeframes.  | |
|Manage users and access|   | Customer is responsible for managing your organizational account users and related access to the {{site.data.keyword.messagehub}} instance.|
|Compliance controls|  | Customer is responsible for maintaining your organizational compliance controls.|
{: caption="Table 2. Responsibilities for security and regulation compliance" caption-side="top"}


## {{site.data.keyword.cloud_notm}} infrastructure and managing the environment
{: #cloud_infrastructure}

<!-- Include an introductory sentence or two about this table. Leave the cell blank for the responsible party column if they do not have responsibility for the given task.  -->

| Task | IBM Cloud Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
|Deploy| {{site.data.keyword.messagehub}} deploys an instance consisting of all required {{site.data.keyword.messagehub}} components and storage.  | Customer is responsible for deciding which region to deploy into. |
|Monitor and repair| {{site.data.keyword.messagehub}} monitors and repairs infrastructure non-disruptively.  | |
|Manage and configure|   | Customer is responsible for using the provided APIs, CLI, or console to manage topics and configuration. |
{: caption="Table 3. Responsibilities for {{site.data.keyword.IBM_notm}} infrastructure and managing the environment" caption-side="top"}

## Disaster recovery
{: #disaster-recovery}

<!-- Include an introductory sentence or two about this table. Leave the cell blank for the responsible party column if they do not have responsibility for the given task.  -->

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
|Disaster recovery|   | Customer is responsible for maintaining and executing a disaster recovery plan in case of loss of service. |
|Replication|   | Currently, it is the responsibility of the customer to manage their own {{site.data.keyword.messagehub}} disaster recovery. {{site.data.keyword.messagehub}} data can be replicated between an {{site.data.keyword.messagehub}} instance in one location (region) and another instance in a different location. However, the customer is responsible for provisioning a remote {{site.data.keyword.messagehub}} instance and managing the replication.|
|Message payload data backup|   | The customer is also responsible for the backup of message payload data. Although this data is replicated across multiple Kafka brokers within a cluster, which protects against the majority of failures, this replication does not cover a location-wide failure.|
|Topic name and data backup|   | It is recommended good practice that a customer backs up their topic names and configuration data for those topics. If you have configured your {{site.data.keyword.messagehub}} instance in a multi-zone region, a regional disaster is very unlikely. However, we recommend customers have a plan for such circumstances. If, due to such an event, a customer's instance is no longer available (and a remote DR instance had not been already set up), the customer should consider configuring a new instance in a new region and restoring their topics and data from backup if available. |
{: caption="Table 4. Responsibilitiess for disaster recovery" caption-side="top"}


## App orchestration
{: #app_orchestration}

<!-- Include an introductory sentence or two about this table. Leave the cell blank for the responsible party column if they do not have responsibility for the given task.  -->

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
|Integrate with select third-party partnership technologies| {{site.data.keyword.messagehub}} provides integrations with select third-party partnership technologies, such as Log Analysis with LogDNA.   |
|Provide service binding to other {{site.data.keyword.IBM_notm}} services| {{site.data.keyword.messagehub}} provides the capability for service binding to other {{site.data.keyword.IBM_notm}} services.  | |
|Manage, integrate, and monitor|   | Customer is responsible for using the provided tools and features to manage the lifecycle of customer-owned applications, for integrating with other services, and monitoring the health of the application (for example, Availability Monitoring).|
{: caption="Table 5. Responsibilities for app orchestration" caption-side="top"}


