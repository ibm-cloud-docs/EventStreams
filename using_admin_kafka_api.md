---

copyright:
  years: 2015, 2021
lastupdated: "2021-04-26"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: EventStreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Using the administration Kafka Java client API
{: #kafka_java_api}


<!-- 
17/10/17 - Karen: following info duplicated at faq.md
 -->

If you're using a Kafka client at 0.11 or later, or Kafka Streams at 0.10.2.0 or later, you can use APIs to create and delete topics. We've put some restrictions on the settings allowed when you create topics. Currently, you can modify the following settings only:
{: shortdesc}

cleanup.policy
:   Set to `delete` (default), `compact` or `delete,compact`

retention.ms
:   The default retention period is 24 hours. The minimum is 1 hour and the maximum is 30 days. Specify this value as multiples of hours.

    **Note:**
    In the Enterprise plan, you can set this to any value.

retention.bytes
:   The maximum size a partition (which consists of log segments) can grow to before we discard old log segments to free up space.

    **Note:**
    Enterprise plan only. Set to any value larger than 1 MB.

segment.bytes
:   The segment file size for the log.

    **Note:**
    Enterprise plan only. Set to any value larger than 100 kB.

retention.ms
:   The default retention period is 24 hours. The minimum is 1 hour and the maximum is 30 days. Specify this value as multiples of hours.

    **Note:**
    In the Enterprise plan, you can set this to any value.

retention.bytes
:   The maximum size a partition (which consists of log segments) can grow to before we discard old log segments to free up space.

    **Note:**
    Enterprise plan only. Set to any value larger than 1 MB.

segment.bytes
:   The segment file size for the log.

    **Note:**
    Enterprise plan only. Set to any value larger than 100 kB.

segment.index.bytes
:   The size of the index that maps offsets to file positions. 

    **Note:**
    Enterprise plan only. Set to any value between 100 kB and 2 GB.

segment.ms
:   The period of time after which Kafka will force the log to roll even if the segment file isn't full. 

    **Note:**
    Enterprise plan only. Set to any value between 5 minutes and 30 days

