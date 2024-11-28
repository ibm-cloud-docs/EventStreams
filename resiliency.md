---

copyright:
  years: 2024
lastupdated: "2024-11-28" 

keywords: resiliency, cluster resiliency, availability, data corruption, deletion, data management, disaster recovery, responsibilities

subcollection: EventStreams

---

{{site.data.keyword.attribute-definition-list}}
# Maximising Resiliency for your {{site.data.keyword.messagehub}} instance 
{: #resiliency}

By default, event streams instances are built with resiliency, with numerous safeguards to prevent loss of availability or data. All instances are replicated across 3 brokers in addition to automated failover for maximum availability. In addition, Event Streams is responsible for managing resource utilisation and instance limits across the estate as well as proactively monitoring (e.g. of in-sync replicas and disk space utilization) to ensure high availability and data durability out of the box. Event streams proactively manages the security and compliance of customer clusters through threat detection and vulnerability scanning and guarantees an SLA of up to 99.99% for MZR’s. [Understanding your responsibilities when you use Event Streams](/docs/EventStreams?topic=EventStreams-event_streams_responsibilities) highlights customer responsibilities which include backup of message payload data and instance data including topic names, data and schema registry data if this is required. 

If a disaster recovery plan including Event Streams on IBM Cloud is required, this plan can include provisioning a new cluster in a new region if a disaster occurs and restoring any configuration or data to that cluster, or, pre-provisioning a cluster in another region and using the Event Streams Mirroring feature.  The customer is responsible for maintaining and executing this disaster recovery plan if the service is lost. This page outlines additional steps users can take to maximise the resiliency of their Event Streams instance at both the cluster and cluster data level.  

## Cluster resiliency
{: #cluster_resiliency}

### 1. Instance Deletion Recovery
{: #instance_deletion_recovery}

All Event Streams plans (excluding satellite) can recover a deleted instance within reclamation period of three days, after which the data is irreversibly destroyed.  You can check the status of a reclamation, and force or cancel a scheduled reclamation by using  the [IBM Cloud CLI](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_reclamations).   

### 2. Application/Client Configuration
{: #resiliency_clientconfig}

Applying these parameters to your applications can significantly improve resiliency and optimize resource usage. These settings are a guidance and ultimately should be traded off against your application needs. The [open source Apache Kafka documentation](https://kafka.apache.org/documentation/) provides a more detailed explanation into these parameters and their importance.  

| Setting | Explanation |
|----------|-----------------------|
|‘fetch.min.bytes=1 fetch.max.wait.ms=500’  |  Empty fetch requests are wasteful because they consume server resources without actually retrieving meaningful data. The default value of 500ms is recommended for fetch.max.wait.ms however, if your application is experiencing high CPU , then consider running less clients, or increasing this.|
|‘enable.idempotence=true retries=Integer.MAX_VALUE’   |  Idempotent producers enable retries and prevent duplicate messages, ensuring exactly-once semantics during data production and improving data durability.  |
|‘acks=all’    |  This guarantees that messages are delivered and acknowledged across all replicas for maximum fault tolerance.    |

### 3. Monitoring and Alerting for early anomaly detection
{: #resiliency_monitoring}

Client observability: It is important to validate that your clients are active and not network isolated. In some cases, customers pump a lot of data into the clients but clients don’t receive the data therefore it is advisable to instrument your clients, check whether the data reaches the server or not and establish a baseline e.g. using throughput and number of unsent messages queued up. The ways you can instrument your clients will vary depending on which client you use.   

Consumer lag: If consumers fall significantly behind and the retention period is approaching its limit, consumers risk missing data because log segments may be deleted in line with the retention policy. 

Disk Usage: It is important to monitor disk usage in your event streams instance. When Disk usage reaches the maximum level, you won’t be able to create anymore topic partitions and only reading (not write) of data will be possible. This risk’s a loss of application availability if it cannot tolerate this.  You must either scale your instance or truncate messages when you get to the maximum disk usage.  

CPU Utilization: Event Streams advise operating at a maximum of 2/3rds CPU Utilisation to protect against the loss of an availability zone. An event streams cluster which is working close or near its recommended max CPU usage is at risk of inefficient processing and may lead to some loss of data.  

Throughput/Capacity Management: Similar to CPU Utilization, Event Streams recommend not to exceed the 2/3rds of the maximum throughput, even when working at Peak capacity. This is buffer is crucial to safeguard the instance during maintenance periods or in the event of an availability zone failure. See more in [Scaling enterprise plan capacity](/docs/EventStreams?topic=EventStreams-ES_scaling_capacity). 

### 4. Automation via Terraform
{: #resiliency_terraform}

Event Streams recommend using Terraform which enables you to rapidly and predictably create and change your instance following Infrastructure as Code (IaC) principles. You must store all terraform configurations in a safe and easily accessibly repository as part of a comprehensive disaster recovery plan.  

### 4. Use Schema Registry
{: #resiliency_schemas}

Event Streams provide a schema registry as part of the enterprise plan which works as a layer of re-enforcement in your Kafka cluster, ensuring data is validated between producers and consumers and reducing the likelihood of un-processable data entering the system. Learn more about using the Event Streams schema registry here.  

 ## Topics, schemas and instance data resiliency  
{: #instance_data-resiliency}

The recommendations for maximising cluster resiliency will help with maximising resiliency of cluster data but in some cases, a single topic, set of topics or a single application can be affected and the following methods can help in prevention and/or recovery of cluster data.  

### 1. Keeping client libraries up to date for vulnerabilities and fixes.
{: #resiliency_clientlib}

Using the latest client libraries ensures you are up to date with latest testing and you are not missing out on fixes which may harm your clients.  The latest client library will provide the best usability and better error messages, maximising the health and reliability of your client and client data.  

### 2. Application Configuration
{: #resiliency_retention}

To maximise topic resiliency, the retention period should be configured for potential downtime to ensure consumers can catch up without missing data. We advise configuring the retention period to exceed the maximum expected downtime for consumers. For example, if a retention period is less than 3 days and applications experience an extended shut own e.g over a long weekend, there is significant risk of missing data upon restart.  

### 3. Soft delete (Schemas only)
{: #resiliency_disable_schema}

 Schema deletion is a two-stage process. The first stage of deletion preserves the schema in the registry, but hides it from some operations. In the event of accidentally deleting a schema, it can be recovered by enabling the disabled schema. Find out more [here](docs/EventStreams?topic=EventStreams-ES_schema_registry#set_schema_state).
