---

copyright:
  years: 2025
lastupdated: "2025-01-13"

keywords: HA for Event Streams, DR for Event Streams, Event Streams recovery time objective, high availability, disaster recovery

subcollection: content-kit

---

{{site.data.keyword.attribute-definition-list}}



# Understanding high availability and disaster recovery for Event Streams
{: #eventstreams-ha-dr}





[High availability](#x2284708){: term} (HA) is the ability for a service to remain operational and accessible in the presence of unexpected failures. [Disaster recovery](#x2113280){: term} is the process of recovering the service instance to a working state.
{: shortdesc}



Event Streams is a global service and you can find the available region and data center locations in the [Service and infrastructure availability by location](/docs/overview?topic=overview-services_region) documentation. As a global service, Event Streams fulfills the defined [Service Level Objectives (SLO)](/docs/resiliency?topic=resiliency-slo) with the Standard and Enterprise plans. The SLO is not a warranty and IBM will not issue credits for failure to meet an objective.



## High availability architecture
{: #ha-architecture}



### High availability features
{: #ha-features}

Event Streams supports the following high availability features: 



| Feature | Description | Consideration |
| -------------- | -------------- | -------------- |
| Multi-zone region reployment  | Distributed across three availability zones for fault tolerance and high availability | In Event Streams, each partitions data is distributed across three availability zones (for MZR deployments) to ensure business continuity in the event of the loss of an availability zone data. |
| Minimum In-Sync replicas | A minimum of two in-sync replicas is required at all times | Event Streams continuosly monitor and ensures that at least two replicas are synchronized across availability to make sure that messages are not lost in the case of a broker or zone failure, ensuring critical data remains durable.|
{: caption="HA features for Event Streams" caption-side="bottom"}


## Disaster recovery architecture
{: #disaster-recovery-intro}






### Disaster recovery features
{: #dr-features}

Event Streams supports the following disaster recovery features:



| Feature | Description | Consideration |
| -------------- | -------------- | -------------- |
| Mirroring | Mirroring for cluster replication| Event Streams provides a Mirroring feature which enables messages in one event streams instance to be continuously copied into a second instance. Customer can use the Event Streams [Mirroring feature](/docs, or choose to manage their own mirroring solution. |
{: caption="DR features for Event Streams" caption-side="bottom"}

#### Mirroring for Event Streams
{: #dr-feature-1}

Mirroring enables messages in one Event Streams service instance to be continuously copied to a second instance. Application resilience can be improved by using mirroring as if the first service instance becomes unavailable, applications can reconnect to the second instance and continue their normal operation.

This feature is part of the fully managed service and can only be used between service instances that use the Event Streams Enterprise plan.

1. Features of mirroring:

- Mirror topics, message data, and consumer group offsets between two Event Streams service instances, which can be provisioned in different IBM Cloud accounts.
SLA of 99.99% availability, consistent with the Event Streams service.
- Can be monitored using IBM Cloud® Monitoring.


2. Limitations of mirroring:

- Unidirectional: Data can only be mirrored in one direction at a time between a pair of service instances. This means that mirroring offers a "active-passive" style of high availability, not "active-active".
- Asynchronous: Messages must be successfully produced to the source instance before they can be mirrored to the target instance. This means that when a failure occurs, some message data may be lost.
- At-least-once message consumption: When a consumer moves between instances, it may need to reprocess messages that it has already processed.
  


### Planning for DR
{: #features-for-disaster-recovery}

The DR steps must be practiced regularly. As you build your plan, consider the following failure scenarios and resolutions.



| Failure | Resolution |
| -------------- | -------------- |
| Hardware failure (single point) | IBM Event Streams is resilient to a single point of hardware failure within a zone - no configuration required. |
| Zone failure | An Event Streams instance that is deployed in a multi-zone region is resilient to the failure of a single zone - no configuration required. For single zone deployments, set up another event streams cluster as a mirrored pair to mitigate against a zone failure.|
| Data corruption |Event Streams does not include any built-in mechanisms to recover from data corruption. Customer is required to plan for such circumstances as a part of a disaster recovery plan and may need to use the Mirroring feature or configure a new instance.  |
| Regional failure | If you configured your Event Streams instance in a multi-zone region, a regional disaster is unlikely. If a regional failure does occur, Customer is required to configure a new instance in another region. Learn more in (Understanding your responsibilities](/docs/EventStreams?topic=EventStreams-event_streams_responsibilities)|
{: caption="DR scenarios for Event Streams" caption-side="bottom"}


## Your responsibilities for HA and DR
{: #feature-responsibilities}

The following information can help you create and continuously practice your plan for HA and DR.



It is important to understand the management responsibilities and terms and conditions that you have when you use IBM® Event Streams for IBM Cloud. The [customer responsibilities](/docs/EventStreams?topic=EventStreams-event_streams_responsibilities) page helps as a starting point for creating a plan for high availability and disaster recovery. 

As part of disaster recovery, it is recommended that you grant users and processes the IAM roles and actions with the least privilege required for their work. See [How can I prevent accidental deletion of services?](/docs/resiliency?topic=resiliency-dr-faq#prevent-accidental-deletion). 

All Event Streams plans (excluding satellite) can recover a deleted instance within reclamation period of three days, after which the data is irreversibly destroyed. You can check the status of a reclamation, and force or cancel a scheduled reclamation by using  the [IBM Cloud CLI](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_reclamations).



If {{site.data.keyword.messagehub}} can’t restore the service instance, the customer must restore as described in [mirroring in a disaster recovery scenario](/docs/EventStreams?topic=EventStreams-disaster_recovery_scenario).

## How {{site.data.keyword.IBM_notm}} maintains services
{: #ibm-service-maintenance}


All upgrades follow the {{site.data.keyword.IBM_notm}} service best practices and have a recovery plan and rollback process in-place. Regular upgrades for new features and maintenance occur as part of normal operations. Such maintenance can occasionally cause short interruption intervals that are handled by [client availability retry logic](/docs/resiliency?topic=resiliency-high-availability-design#client-retry-logic-for-ha). Changes are rolled out sequentially, region by region and zone by zone within a region. Updates are backed out at the first sign of a defect.


Complex changes are enabled and disabled with feature flags to control exposure.


Changes that impact customer workloads are detailed in notifications. For more information, see [monitoring notifications and status](/docs/account?topic=account-viewing-cloud-status) for planned maintenance, announcements, and [release notes](/docs/EventStreams?topic=EventStreams-event-streams-relnotes) that impact Event Streams.
