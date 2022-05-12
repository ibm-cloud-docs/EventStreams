---

copyright:
  years: 2021
lastupdated: "2021-07-16"

keywords: IBM Event Streams, Log Analysis, streaming

subcollection: eventstreams

---

{:external: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Streaming data from Log Analysis
{: #streaming_data_log_analysis}

{{site.data.keyword.messagehub}} can be used to stream data from Log Analysis to other corporate tools, 
such as Security Information and Event Management (SIEM) tools.
{: shortdesc}

When you enable streaming on an IBM Log Analysis instance, you configure Log Analysis to send data to an Event Streams instance. 
Then, you can configure Kafka Connect to consume the data and forward it to your destination tool. 
After the data is persisted within Event Streams, you can configure any application or service to create a subscription 
and take action on log data being streamed.

For more information, see [Streaming data from an IBM Log Analysis instance](/docs/log-analysis?topic=log-analysis-streaming){: external}.

For step-by-step instructions for streaming to Splunk as an example SIEM system, see [Streaming log events from LogDNA to Splunk](https://ibm.github.io/cloud-enterprise-examples/log-streaming/configure-streaming-for-third-party-tools/){: external}.
