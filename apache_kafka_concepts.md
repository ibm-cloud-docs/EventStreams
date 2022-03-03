---

copyright:
  years: 2015, 2021
lastupdated: "2021-06-22"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: EventStreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Apache Kafka concepts
{: #apache_kafka}


![Kafka architecture diagram.](kafka_overview.png "Diagram that shows a Kafka architecture. A producer is feeding into a Kafka topic over 3 partitions and the messages are then being subscribed to by consumers.")

The following list defines some Apache Kafka concepts:

## Brokers
{: #kafka_brokers}

Apache Kafka is a distributed messaging system. A Kafka cluster consists of a set of brokers.
A cluster has a minimum of 3 brokers.

![Brokers diagram.](concepts_brokers.png "Diagram that shows an example broker.")

## Messages
{: #kafka_messages}

A message is a unit of data in Kafka. Each message is represented as a record, which comprises two parts: key and value. The key is commonly used for data about the message and the value is the body of the message. Kafka uses the terms record and message interchangeably. 

## Topics and partitions
{: #kafka_topics_partitions}

Each topic is a named stream of messages. A topic is made up of one or more partitions. The messages on a partition are ordered by a number that is called the offset. By having multiple partitions distributed across the brokers, the scalability of a topic is increased.

If a topic has more than one partition, it allows data to be fed through in parallel to increase throughput by distributing the partitions across the cluster. The number of partitions also influences the balancing of workload among consumers.

For more information, see [Partition leadership](/docs/EventStreams?topic=EventStreams-partition_leadership#partition_leadership).

![Topics and partitions diagram.](concepts_topics_and_partitions.png "Diagram that shows 1 topic with 3 partitions spread across 3 brokers.")

## Replication
{: #kafka_replication}

To improve availability, each topic can be replicated onto multiple brokers. For each partition, one of the brokers is the leader, and the other brokers are the followers.

Replication works by the followers repeatedly fetching messages from the leader.

![Replication diagram.](concepts_replication.png "Diagram that shows a topic partition being replicated across 3 brokers.")

## In-sync replicas
{: #kafka_isr}

A follower replica that is keeping up with the partition leader is in-sync. Any follower with an in-sync replica can become the leader without losing any messages.

If the partition leader fails, another leader is chosen from the followers. All the replicas should usually be in-sync. It is acceptable for a replica to be temporarily not in-sync while it is catching up after a failure.

![In-sync-replicas diagram.](concepts_in_sync_replicas.png "Diagram that shows a topic partition being replicated across three brokers and staying in-sync across all replicas.")

## Producers
{: #kafka_producers}

A producer publishes messages to one or more topics. A producer can publish to one or more topics and can optionally choose the partition that stores the data.

You can also configure your producer to prioritize speed or reliability by choosing the level of acknowledgement the producer receives for messages it publishes.

For more information, see [Producing Messages](/docs/EventStreams?topic=EventStreams-producing_messages#producing_messages).

![Producers diagram.](concepts_producers.png "Diagram that shows a producer publishing messages to one topic across three brokers.")

## Consumers
{: #kafka_consumers}

A consumer reads messages from one or more topics and processes them. The difference between a consumer's current position and the newest message on a partition is known as the offset lag.

If the lag increases over time, it is a sign that the consumer is not able to keep up. Over the short term, this is not an issue but eventually the consumer might miss messages if the retention period is exceeded.

For more information, see [Consuming Messages](/docs/EventStreams?topic=EventStreams-consuming_messages#consuming_messages).

![Consumers diagram.](concepts_consumers.png "Diagram that shows a consumer processing messages from one topic across three brokers.")

## Consumer groups
{: #kafka_consumer_groups}

A consumer group contains one or more consumers working together to process the messages. The messages from a single partition are processed by one consumer in each group.

At any time, each partition is assigned to only one consumer in the group. This ensures that the messages on each partition are processed in order.

If more partitions than consumers exist in a group, some consumers have multiple partitions. If more consumers than partitions exist, some consumers have no partitions.

![Consumer groups diagram.](concepts_consumer_groups.png "Diagram that shows a consumer processing messages from 1 topic across 3 brokers.")

## More information
{: #kafka_information}

To learn more, see the following information:
- [Apache Kafka documentation](http://kafka.apache.org/documentation.html){: external}



