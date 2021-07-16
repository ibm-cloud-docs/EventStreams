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

{{site.data.keyword.messagehub}} can be used to stream data from Log Analysis to third party tools, 
such as Security Information and Event Management (SIEM) tools.
{: shortdesc}

When you enable streaming on an IBM Log Analysis instance, you configure Log Analysis to send data to an Event Streams instance. 
Then, you can configure Kafka Connect to consume the data and forward it to your destination tool. 
Once the data is persisted within Event Streams, you can configure any application or service to create a subscription 
and take action on log data being streamed.

For more information, see [Streaming data 
![External link icon](../../icons/launch-glyph.svg "External link icon")]
(/docs/log-analysis?topic=log-analysis-streaming/){:new_window}.
