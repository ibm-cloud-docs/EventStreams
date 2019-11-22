---

copyright:
  years: 2015, 2019
lastupdated: "2019-11-22g"

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
{: #your-id}
<!-- The title of your H1 should be Understanding your responsibilities with using _service-name_, where _service-name_ is the non-trademarked short version conref. -->

Learn about the management responsibilities and terms and conditions that you have when you use {{site.data.keyword.messagehub_full}}. For a high-level view of the service types in {{site.data.keyword.Bluemix}} and the breakdown of responsibilities between the customer and {{site.data.keyword.IBM_notm}} for each type, see [Shared responsibilities for {{site.data.keyword.cloud_notm}} offerings](/docs/overview?topic=overview-shared-responsibilities).
{:shortdesc}

Review the following sections for the specific responsibilities for you and for {{site.data.keyword.IBM_notm}} when you use {{site.data.keyword.messagehub_full}}. For the overall terms of use, see [{{site.data.keyword.Bluemix}} Terms and Notices](/docs/overview/terms-of-use?topic=overview-terms).

  
## Incident and operations management
{: #incident-and-ops}

<!-- Include an introductory sentence or two about this table. Leave the cell blank for the responsible party column if they do not have responsibility for the given task.  -->

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
|Monitor environment| Perform continuous review and service improvements, code updates, and operational monitoring.  | Customer responsibility description |
|High availability| Provide high availability via multi-zone region deployment of {{site.data.keyword.messagehub}} to protect against single points of failure up to and including a data center loss to achieve IBM SLA as per IBM Cloud terms and conditions.  | Customer responsibility description |
|Deploy {{site.data.keyword.messagehub}} environment|  with IBM recommended best practice configuration options (such as replication factor, min in sync replicas, throttling, rack awareness)  | Customer responsibility description |
|Topic name backup| Topic names are backed up by {{site.data.keyword.messagehub}}  | Customer responsibility description |
{: caption="Table 1. Responsibilities for incident and operations" caption-side="top"}


## Change management
{: #change-management}

<!-- Include an introductory sentence or two about this table. Leave the cell blank for the responsible party column if they do not have responsibility for the given task.  -->

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
|Task 1| {{site.data.keyword.IBM_notm}} responsibility description  | Customer responsibility description |
|Task 2| {{site.data.keyword.IBM_notm}} responsibility description  | Customer responsibility description |
|Task 3| {{site.data.keyword.IBM_notm}} responsibility description  | Customer responsibility description |
{: caption="Table 2. Responsibilities for change management" caption-side="top"}


## Identity and access management
{: #iam_responsibilities}

<!-- Include an introductory sentence or two about this table. Leave the cell blank for the responsible party column if they do not have responsibility for the given task.  -->

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
|Task 1| {{site.data.keyword.IBM_notm}} responsibility description  | Customer responsibility description |
|Task 2| {{site.data.keyword.IBM_notm}} responsibility description  | Customer responsibility description |
|Task 3| {{site.data.keyword.IBM_notm}} responsibility description  | Customer responsibility description |
{: caption="Table 3. Responsibilities for identity and access management" caption-side="top"}

## Security and regulation compliance
{: #security_compliance}

<!-- Include an introductory sentence or two about this table. Leave the cell blank for the responsible party column if they do not have responsibility for the given task.  -->

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
|Maintain controls| {{site.data.keyword.IBM_notm}} maintains controls commensurate to various industry compliance standards for which we are certified.  | Customer responsibility description |
|IBM Cloud Identity and Access Management (IAM).| IBM provides security and access control service with IBM Cloud Identity and Access Management (IAM)  | Customer responsibility description |
|Security and vulnerability patch updates to client {{site.data.keyword.messagehub}} cluster| IBM applies the provided security and vulnerability patch updates to client {{site.data.keyword.messagehub}} cluster - according to IBM X-Force timeframes  | Customer responsibility description |
{: caption="Table 4. Responsibilities for security and regulation compliance" caption-side="top"}

## Disaster recovery
{: #disaster-recovery}

<!-- Include an introductory sentence or two about this table. Leave the cell blank for the responsible party column if they do not have responsibility for the given task.  -->

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
|Task 1| {{site.data.keyword.IBM_notm}} responsibility description  | Customer responsibility description |
|Task 2| {{site.data.keyword.IBM_notm}} responsibility description  | Customer responsibility description |
|Task 3| {{site.data.keyword.IBM_notm}} responsibility description  | Customer responsibility description |
{: caption="Table 5. Responsibilitiess for disaster recovery" caption-side="top"}

## App orchestration
{: #app_orchestration}

<!-- Include an introductory sentence or two about this table. Leave the cell blank for the responsible party column if they do not have responsibility for the given task.  -->

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
|Provide {{site.data.keyword.messagehub}} integrations with select third-party partnership technologies, such as Log Analysis with LogDNA.
|Provide the capability for service binding to other {{site.data.keyword.IBM_notm}} services.| Provide the capability for service binding to other {{site.data.keyword.IBM_notm}} services.  | Customer responsibility description |
|Manage, integrate and monitor|   | Use the provided tools and features to manage the lifecycle of customer-owned applications, integrate with other services, and monitor the health of the application (for example, Availability Monitoring
 |
{: caption="Table 5. Responsibilities for app orchestration" caption-side="top"}


## {{site.data.keyword.IBM_notm}} infrastructure and managing the environment
{: #cloud_infrastructure}

<!-- Include an introductory sentence or two about this table. Leave the cell blank for the responsible party column if they do not have responsibility for the given task.  -->

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
|Deploy| Deploy an {{site.data.keyword.messagehub}} instance consisting of all required {{site.data.keyword.messagehub}} components and storage  | Customer is responsible deciding which region to deploy into |
|Monitor and repair| Monitor and repair infrastructure non-disruptively  | Customer responsibility description |
|Manage and configure
|   | Customer is responsible for using the provided APIs, CLI, or, console to manage topics and configuration |
{: caption="Table 5. Responsibilities for {{site.data.keyword.IBM_notm}} infrastructure and managing the environment" caption-side="top"}

