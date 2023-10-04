---

copyright:
  years: 2023
lastupdated: "2023-10-04"

keywords: api, rest api

subcollection: EventStreams

---

{{site.data.keyword.attribute-definition-list}}

# API overview
{: #api_reference}

{{site.data.keyword.messagehub_full}} provides a REST API to help connect your existing systems to your {{site.data.keyword.messagehub}} Kafka cluster. Using the API, you can 
integrate {{site.data.keyword.messagehub}} with any system that supports RESTful APIs.
{: shortdesc}

The following API versions are available:

- [Kafka API](https://kafka.apache.org/documentation/): Kafka exposes all its functionality over a language independent protocol that has clients available in many programming languages. Kafka includes three protocol APIs (Producer, Consumer, Admin) and two additional framework APIs (Streams, Connect).
- [{{site.data.keyword.messagehub}} REST Producer](/apidocs/event-streams/restproducer): Producer RESTful API that you can use for writing (publishing) data to topics.
- [{{site.data.keyword.messagehub}} REST Producer v2 endpoint](/apidocs/event-streams/restproducer_v2): 
- [{{site.data.keyword.messagehub}} Admin REST API](/apidocs/event-streams/adminrest): Administration RESTful API that you can use to create, delete, list, and update topics.

![Apache Kafka API and CLI](https://www.kaltura.com/p/1773841/sp/177384100/embedIframeJs/uiconf_id/27941801/partner_id/1773841?iframeembed=true&entry_id=1_18293q1v){: video output="iframe" data-script="none" id="mediacenterplayer" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen}

In addition to the different API versions that are available, you also have the option to use the CLI reference and the console tools:

- [{{site.data.keyword.messagehub}} CLI reference](/docs/EventStreams?topic=EventStreams-cli_reference): It provides a seamless mechanism by which to view and administer the topics, partitions, consumer groups, and configuration of your {{site.data.keyword.messagehub}}'s Kafka instances.
- [Using Kafka console tools with {{site.data.keyword.messagehub}}](/docs/EventStreams?topic=EventStreams-kafka_console_tools): Apache Kafka comes with various console tools for simple administration and messaging operations. These tools are helpful when you just get started with Kafka.
