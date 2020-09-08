---

copyright:
  years: 2020
lastupdated: "2020-08-17"

keywords: IBM Event Streams, reserved disk usage

subcollection: EventStreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}


# Understanding reserved disk usage
{: #ES_understanding_reserved_disk_usage}

This section describes how the usable storage of an Event Streams instance is utilised by the topics and partitions 
created and the configuration settings you apply.

First of all, it's important to note, the defined storage of an Event Streams instance is usable storage. 
That means you do not need to worry about storage used by replicas (as all topics have their replication factor set to 3), 
that is NOT taken from the usable storage. This keeps things simple and allows you to just plan how to map the retention 
of those messages to storage utilisation.

## Understanding how Kafka stores data
{: #ES_understanding_how_kafka_stores_data}

Kafka allows users to configure retention limits on topics.

The retention.bytes configuration is the total number of bytes allocated for messages for each partition of the topic. 
Once exceeded, Kafka will delete oldest messages. So for example, if you are generally sending in 200MB a day of messages 
to a single partition topic, and you want to keep them for 5 days you would set retention.bytes to 1GB (200MB x 5 days). 

If this was over 10 partitions then you would set retention.bytes = 100MB (1GB / 10 partitions).

Internally Kafka splits each partition into log segments. This again is a property you can set, log.segment.size, the default
being 512MB. When we mentioned that Kafka deletes the oldest messages, it actually deletes the oldest log segment. For this 
reason, Kafka needs to keep space for one extra log segment over and above the number of log segments required to satisfy 
the retention.bytes configuration.

For example,

     retention.bytes = 1GB
     log.segment.size = 512MB
     kafka will need approx 1.5GB per partition for the topic storage.

or 

     retention.bytes = 100MB
     log.segment.size = 512MB
     kafka will need approx 1GB per partition for the topic storage.

There is additional storage needed per partition for indexes. For each log segment, Kafka also 
stores 2 indexes. Their sizes is defined by segment.index.size which is also configurable and has a default of 10MB. 
For reference, the storage used by indexes is calculated as 

     2 x number.of.log.segments x segment.index.size

where 

     number.of.log.segments = floor(retention.bytes/segment.index.size) + 1
     
## Managing Storage with {{site.data.keyword.messagehub}}
{: #ES_managing_storage_with_event_streams}     

When doing topic administration operations, such as creating topics, creating partitions or changing topic configurations, 
Event Streams ensures enough storage is available to satisfy the operation. To do this, for each topic, Event Streams 
computes the "reserved size" per topic using the following method:

     Reserved size = retention.bytes + log.segment.size + (2 x segment.index.size x number.of.log.segments)

where 

     number.of.log.segments = floor(retention.bytes/segment.index.size) + 1.


The total reserved storage percentage is also exposed in Sysdig via the [ibm_eventstreams_instance_reserved_disk_space_percent
metric](/docs/EventStreams?topic=EventStreams-metrics#ibm_eventstreams_instance_reserved_disk_space_percent).

If there is not enough unreserved storage to satisfy the topic operation, it is rejected with a PolicyViolation error 
detailing the reason.

**Note:** The reserved size calculation may change in the future if Kafka storage requirements are updated.

## Examples
{: #ES_managing_storage_with_event_streams_examples}  

A non obvious effect of the above is that Kafka can actually reserve more storage than expected depending on your 
topic configurations.

Let's consider a few examples:

1. A topic with retention.bytes of 1GB, and with a log segment size of 512MB:

    With 1 partition, it would reserve about 1.5GB of storage
   
    In this case, the reserved size is significantly larger than the retention size.


2. A topic with retention.bytes of 50GB, and with a log segment size of 512MB:

    With 1 partition, it would reserve about 50.5GB of storage
    
    In this case, the reserved size is very close to the retention size.


3. A topic with retention.bytes of 1GB, and with a log segment size of 128MB:

    With 1 partition, it would reserve about 1.1GB of storage
    
    In this case, the reserved size is very close to the retention size.
