---

copyright:
  years: 2021
lastupdated: "2021-07-16"

keywords: IBM Event Streams, Log Analysis, streaming

subcollection: eventstreams

---

{:new_window: target="_blank"}
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
Once the data is persisted within Event Streams, you can configure any application or service to create a subscription 
and take action on log data being streamed.

For more information, see [Streaming data from an IBM Log Analysis instance
![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/log-analysis?topic=log-analysis-streaming){:new_window}.

{{site.data.keyword.messagehub}} can also be used to stream log events from LogDNA to third party tools, such as Splunk.

You can configure LogDNA to stream log events into an {{site.data.keyword.messagehub}} instance. Once in {{site.data.keyword.messagehub}}, these events can be forwarded to many third party tools using Kafka Connect.

For the step-by-step instructions, see [Streaming log events from LogDNA to Splunk ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://ibm.github.io/cloud-enterprise-examples/log-streaming/configure-streaming-for-third-party-tools/){:new_window}.
