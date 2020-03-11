---

copyright:
  years: 2015, 2020
lastupdated: "2020-03-11"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka, replication, failover, scenario, disaster recovery, mirroring

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}
{:deprecated: .deprecated}
{:important: .important}

# Disaster recovery example scenario 
{: #disaster_recovery_scenario}

Let's look at an end to end disaster recovery scenario. This demonstrates how mirroring can be used to provide increased availability and keep applications working in case of a major incident affecting a full region. Two clusters have been provisioned in different regions and configured for mirroring (following the Mirroring Setup Guide) using A and B as cluster aliases. 
{:shortdesc}

A producer publishes records to a topic called accounting.invoices and a consumer reads the messages from that topic in cluster A.

![Mirroring overview diagram.](disaster1.png "Diagram that shows a Kafka architecture. A producer is feeding into a Kafka topic over 3 partitions and the messages are then being subscribed to by consumers."){: caption="Figure 1. A description that prints on the page" caption-side="bottom"}

## Source cluster becomes unavailable 
We will now consider what happens if a disaster occurs on the source cluster's region.

<diagram>

It is the responsibility of the Event Streams instance owner to determine if the impact of the event is such as to declare a disaster. The service instance owner must coordinate the failover of applications including their reconfiguration, redeployment and restart if necessary.

## Failing over producers 

To failover:
stop the producers that were pointing to cluster A
restart the producers pointing to cluster B's endpoints

<diagram>

The producer is now switched to cluster B and sends messages to a new local topic with the same name as the original.

## Failing over consumers
To fail over:

- Stop the consumers that were pointing to cluster A
- Restart the consumers to point to cluster B's endpoints

<diagram>

The consumer is now able to continue consuming the existing messages from the `accounting.invoices.A` topic from cluster B while new messages will come from `accounting.invoices`.

## Resetting a mirroring environment

At that point, the Event Streams service instance owner is responsible for deciding what happens when cluster A has been recovered. 

In case cluster A is not recoverable, the Event Streams service instance owner is responsible for enabling mirroring between cluster B and a newly provisioned instance.

Typically a user returns operations to cluster A after it has recovered. Below is the recommended way to return primary operations to cluster A.

Before failing back, mirroring has to be enabled in the opposite direction:
- Enable mirroring between cluster B (now the source) and cluster A (now the target)
- The source cluster A now becomes the target cluster.
- The target cluster B becomes the new source cluster.

Now make sure data is being replicated into cluster A by examining the topics from cluster B appearing on cluster A. Remember these will have the suffix from the new source cluster, B.

<diagram>

## Failback

The decision to fail back is again owned by the Event Streams instance owner. The service instance owner must coordinate the failback of applications including their reconfiguration, redeployment, and restart if necessary.

Unlike the failover case, in this case there has been no disaster on cluster B. Therefore failback should be a controlled operation and can be achieved without data loss. 

<diagram>

Finally you should now switch the mirroring back to the original configuration, this means cluster A is again the source and cluster B resumes as the target.