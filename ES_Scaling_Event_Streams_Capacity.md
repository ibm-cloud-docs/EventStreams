---

copyright:
  years: 2020
lastupdated: "2020-08-17"

keywords: IBM Event Streams, scaling capacity

subcollection: EventStreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}


# {{site.data.keyword.messagehub}} Scaling Capacity
{: #ES_scaling_capacity}


## Event Streams Capacity
{: #ES_capacity}

The {{site.data.keyword.messagehub}} Enterprise plan allows you to specify throughput and storage capacity when a new instance of the service is created.  If you find after using the service instance that the current capacity configuration of your service instance is not meeting the demands of your solution, throughput and/or storage capacity can be scaled-up to meet demands.

## Throughput Capacity
{: #ES_thruput_capacity}

Throughput capacity is the recommended peak MB/s maximum for producing and consuming messages. 

Our base capacity unit provides 150 MB/s of throughput (75 MB/s producing and 75 MB/s consuming)

To scale-up throughput capacity, you can add additional capacity units. Each additional capacity unit adds 150MB/s of throughput to your service instance, to a total of 450MB/s.

The recommended throughput maximum is based on a typical workload and takes into account the possible impact of operational actions or failure modes, like the loss of an availability zone. If the average throughput exceeds the recommended figure, a loss in performance might be experienced during these conditions.  It is recommended to plan your maximum throughput capacity as two-thirds of the peak maximum.  For example two-thirds of the 150 MB/s peak maximum is 100 MB/s.  For additional information on capacity recommendations and limitations, refer to [limits and quotas](/docs/EventStreams?topic=EventStreams-kafka_quotas#limits_enterprise).

Throughput scaling is independent of storage, however for each tier there is a defined minimum storage amount required. 

## Storage Capacity
{: #ES_storage_capacity}

Storage capacity is the amount of storage allocated in the service instance for retention of message data. 

Storage capacity can be scaled-up, independent of throughput capacity, when data retention is important for your architecture.

Refer to [choosing your plan](/docs/EventStreams?topic=EventStreams-plan_choose#what-s-supported-by-the-lite-standard-enterprise-and-classic-plans) for additional information on capacity options.

## Scaling Combinations
{: #ES_scaling_combinations}

The table below lists valid throughput/storage capacity unit combinations.

|**Throughput capacity**|**Available storage capacity**|
|-------------------|--------------------------|
|150 MB per second (75 MB/s producing, 75 MB/s consuming)|2TB, 4TB, 6TB, 8TB, 10TB, 12TB|
|300 MB per second (150 MB/s producing, 150 MB/s consuming)|4TB, 8TB, 12TB|
|450 MB per second (225 MB/s producing, 225 MB/s consuming)|6TB, 12TB|

For additional information on capacity limitations, refer to [limits and quotas](/docs/EventStreams?topic=EventStreams-kafka_quotas#limits_enterprise).

Throughput capacity cannot be scaled down.  To move to a lower throughput capacity would require creating a new Event Streams service instance at the lower capacity unit.
{:important}

Storage capacity cannot be scaled down.  To move to a lower storage capacity would require creating a new Event Streams service instance at the lower capacity unit.
{:important}

## How to scale capacity
{: #ES_how_to_scale_capacity}

The steps below show you how to scale-up throughput and/or storage capacity for an {{site.data.keyword.messagehub}} Enterprise plan service instance.  If you do not have an Enterprise instance, the steps below will help you create one.

At this time, scaling-up an {{site.data.keyword.messagehub}} service instance capacity requires use of the {{site.data.keyword.Bluemix_notm}} CLI.

To install this tool, see [install devtools](/docs/cli?topic=cli-install-devtools-manually#install-devtools-manually).

The {{site.data.keyword.Bluemix_notm}} CLI command will use the **service-instance-update** command to update your {{site.data.keyword.messagehub}} service instance resource.  The user ID in the account used to issue the **service-instance-update** command must be assigned the same access policies as are needed when creating resources.  See [creating resources](/docs/account?topic=account-manage_resource#creating-resources) for access requirements.

### During the scale-up process

The time required to scale-up the {{site.data.keyword.messagehub}} service instance is variable. Both throughput and storage require provisioning extra infrastructure.
  
  During this time Kafka topic/partition add/update/delete operations will be suspended.  This ensures the integrity of data is maintained during storage volume infrastructure scale-up operations.  This suspension of topic/partition operations will only occur during a brief portion of the scale-up process, not the entire process.

Valid combinations/values for the "throughput" and "storage_size" are

|**Throughput capacity units (peak maximum)**|**"throughput" value to specify**|**Storage capacity units**|**"storage_size" value to specify**|
|----------------------------------------|-----------------------------|----------------------|------------------------------|
|1  (150 MB/s )|150|2TB|2048|
| | |4TB|4096|
| | |6TB|6144|
| | |8TB|8192|
| | |10TB|10240|
| | |12TB|12288|
|2  (300 MB/s )|300|4TB|4096|
| | |8TB|8192|
| | |12TB|12288|
|3  (450 MB/s )|450|6TB|6144|
| | |12TB|12288|



### Example 1
Scale-up a service instance configured with 1 throughput capacity unit and base storage (throughput 150 MB/s, storage 2TB) to 2 throughput capacity units and 8TB usable storage (throughput 300 MB/s, storage 8TB).



1. If you don't already have one, create an {{site.data.keyword.messagehub}} service instance.
  
    a. Log in to the **{{site.data.keyword.Bluemix_notm}} console**.
    
    b. Click the **{{site.data.keyword.messagehub}} service** in the Catalog.
    
    c. Select the **Enterprise plan** on the service instance page.
    
    d. Review capacity selections (1 base capacity unit includes 150MB/s throughput capacity and 2TB storage capacity).  
        
    g. Enter a name for your service instance. You can use the default value.
    
    h. Click Create. (See [choosing your plan](/docs/EventStreams?topic=EventStreams-plan_choose#what-s-supported-by-the-lite-standard-enterprise-and-classic-plans) for information on the amount of time needed to create the service instance).

2. Login to the **{{site.data.keyword.Bluemix_notm}} CLI**.
 
     <code>ibmcloud login</code>

3. Get the resource name of your {{site.data.keyword.messagehub}} service instance.
  
     <code>ibmcloud resource service-instances</code>
     
   (you can find the name of your instance in the Name column).

4. View current capacity configuration using the {{site.data.keyword.messagehub}} CLI.
    
    To install and use the CLI plugin, refer to [cli reference](/docs/EventStreams?topic=EventStreams-cli_reference).
    
    Use the following command to display the current capacity configuration.
  
      <code>ibmcloud es init  --instance-name  "Event Streams resource instance name"</code>

      Output will be similar to the following, which shows this service instance is configured with a throughput capacity of 1 (one) (150 MB/s peak maximum) and 2TB of storage:

        API Endpoint:         https://service-instance-adsf1234asdf1234asdf1234-0000.eu-south.containers.appdomain.cloud
        Service endpoints:    public
        Storage size:         2048 GB
        Throughput:           150 MB/s

### Example 2

1. Scale-up the service instance from ** 1 base capacity unit (150 MB/s throughput, 2TB storage)** to **1 additional throughput unit (300 MB/s)** plus **Maximum storage capacity of 8TB** 
    
    a. Execute the following from the cli
    
      <code> ibmcloud resource service-instance-update "Event Streams resource instance name" -p '{"throughput":"300","storage_size":"8192"}' </code>

    b. If there is an issue running the ibmcloud resource service-instance-update command and requires contacting IBM Support for assistance, please run this command and include the output when contacting support

      <code> ibmcloud resource service-instance "Event Streams resource instance name" --output=json </code>

2. Monitor the update of the service instance.

    The scale-up process could take several minutes to complete depending on what new resources need to be allocated to the service instance.
    
    You can get the current service instance information using the command
    
      <code> ibmcloud resource service-instance "Event Streams resource instance name" --output=json </code>
        
    Review the Last Operation section of the output. The information will be continuously updated as the update proceeds. When the scale-up process has completed, the last operation information will indicate update succeeded or sync succeeded.

    Rerun the command until success is indicated.

3. Verify the scaled-up capacity configuration using the Event Streams CLI.
  
    Display the capacity configuration
    
      <code> ibmcloud es init  --instance-name  "Event Streams resource instance name" </code>
        
    Output will be similar to the following, which shows this service instance has been scaled-up to a throughput capacity of 2 (two) (300 MB/s peak maximum) and 8TB of storage:


       API Endpoint:         https://service-instance-adsf1234asdf1234asdf1234-0000.eu-south.containers.appdomain.cloud
       Service endpoints:    public
       Storage size:         8192 GB
       Throughput:           300 MB/s

