---

copyright:
  years: 2021, 2022
lastupdated: "2022-11-22"

keywords: IBM Event Streams, Log Analysis, streaming

subcollection: eventstreams

---

{{site.data.keyword.attribute-definition-list}}

# Streaming data from {{site.data.keyword.loganalysisshort}}
{: #streaming_data_log_analysis}

{{site.data.keyword.messagehub}} can be used to stream data from {{site.data.keyword.loganalysislong}} to other corporate tools, such as Security Information and Event Management (SIEM) tools.
{: shortdesc}

When you enable streaming on an {{site.data.keyword.loganalysislong_notm}} instance, you configure {{site.data.keyword.loganalysisshort}} to send data to an {{site.data.keyword.messagehub}} instance. Then, you can configure Kafka Connect to consume the data and forward it to your destination tool. After the data is persisted within {{site.data.keyword.messagehub}}, you can configure any application, or service to create a subscription and take action on log data that is streamed.

For more information, see [Streaming data from an IBM Log Analysis instance](/docs/log-analysis?topic=log-analysis-streaming){: external}.

For step-by-step instructions for streaming to Splunk as an example SIEM system, see [Streaming log events from LogDNA to Splunk](https://ibm.github.io/cloud-enterprise-examples/log-streaming/configure-streaming-for-third-party-tools/){: external}.
