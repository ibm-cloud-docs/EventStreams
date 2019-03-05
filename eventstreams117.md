---

copyright:
  years: 2015, 2019
lastupdated: "2018-06-22"

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Kafka quotas
{: #kafka_quotas }

** Kafka quotas apply to the Standard plan only.**
<br/>

{{site.data.keyword.messagehub}} uses throughput quotas to control the network bandwidth that is used by clients. The quotas are in place to minimize the impact of clients on each other. {{site.data.keyword.messagehub}} now implements Kafka quotas, that is throttling for producers and consumers.

Quotas work by measuring the throughput of producers and consumers, and then throttling those that exceed the quotas by slightly delaying the responses to their requests. The effect is to apply a gentle brake to producers and consumers that attempt to consume a lot of bandwidth.

{{site.data.keyword.messagehub}} assigns a throughput quota to each {{site.data.keyword.messagehub}} service instance. A separate quota is used for producers and consumers. The quota is proportional to the number of partitions created for that service instance and is spread approximately evenly across the brokers, although the quota is not applied to each partition.

For example, consider a service instance with 10 topics, each with 1 partition and each partition has a 1 MB/s quota. The throughput quota for producers is as follows:

```
10 x 1 MB/s = 10 MB/s
```

The quota is applied across the nodes of the Kafka cluster. The precise value applied at a point in time depends on the current distribution of partition leaders on the nodes of the cluster. For example, if all the partition leaders were by chance to exist on the same single broker, you could use 10 MB/s spread across those partitions, that is Partition 0 could use 10 MB/s and partitions 1 through 9 will be using nothing.
