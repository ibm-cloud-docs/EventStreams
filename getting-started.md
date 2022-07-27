---

copyright:
  years: 2015, 2022
lastupdated: "2022-07-26"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: EventStreams

---

{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}
{:important: .important}

# Getting started with IBM Event Streams for IBM Cloud
{: #getting-started}

{{site.data.keyword.messagehub_full}} is a high-throughput message bus that is built with Apache Kafka. To get started with {{site.data.keyword.messagehub}} and start sending and receiving messages, you can use the Java™ sample. The sample shows how a producer sends messages to a consumer by using a topic. The same sample program is used to consume messages and produce messages.
{: shortdesc}

To understand more about how {{site.data.keyword.messagehub}} works, see [{{site.data.keyword.messagehub}} overview](/docs/EventStreams?topic=EventStreams-about). {{site.data.keyword.messagehub}} was previously called Message Hub.

To access other {{site.data.keyword.messagehub}} samples, including samples for Node.js and Python, see [{{site.data.keyword.messagehub}} samples](https://github.com/ibm-messaging/event-streams-samples){: external}.

![Get started with {{site.data.keyword.messagehub_full}}](https://video.ibm.com/embed/channel/23952663/video/event-streams-intro){: video output="iframe" data-script="none" id="youtubeplayer" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen}

## Prerequisites
{: #getting_started_prereqs}

1. **If you don't already have one, create an {{site.data.keyword.messagehub}} service instance.**

   a. Log in to the {{site.data.keyword.Bluemix_notm}} console.
  
   b. Click the [**{{site.data.keyword.messagehub}} service**](https://cloud.ibm.com/catalog/event-streams){: external} in the **Catalog**.
  
   c. Select the **Lite plan** on the service instance page.
  
   d. Enter a name for your service. You can use the default value.
  
   e. Click **Create**. The {{site.data.keyword.messagehub}} **Getting started** page opens. 

2. **If you don't already have them, install the following prerequisites:**
	
	- [Git](https://git-scm.com/){: external}
	- Java™  8 or higher 

## Tutorial steps
{: #getting_started_steps}

1. In the {{site.data.keyword.Bluemix_notm}} console (UI), go to your **Resource list**, select your {{site.data.keyword.messagehub}} resource, and click on the **Get started with a sample application** tile.

2. Follow the **Configure & run starter application** steps:

     a. Click the **Download .JAR from GitHub** button to download the latest .JAR release. 
     
     b. Click the **Generate properties** button to generate and download the properties file. The **Topic** panel opens.
     
     c. Enter a name for a **New topic** that you want to create. Or, click on **Existing topic** to select an existing topic that you want to use. If you are on the Lite plan and a topic already exists, the **New topic** button is disabled. {: note}
     
     d. Select the **Service credential** that you want to use, or select **Create new** to create a new one. 
     
     e. Click the **Generate and download** button. The kafka.properties file gets downloaded to your local machine. It contains the necessary configuration to connect to {{site.data.keyword.messagehub}}. You can open it in a text editor to see how it works.
     
     f. The panel shows your selected configuration. Clicking on the **Regenerate** button starts the process again. Clicking on the **Download** button downloads the properties file again.
     
3. Navigate to the folder that contains the downloaded .JAR file by using the command line or a terminal and run the command. Replace the value `<path-to-properties>` with the file path to the kafka.properties file.

4. Once the application starts, click the **'localhost:8080'** link at the bottom of the form to open the starter app and see messages flowing through the topic.

## Next steps
{: #next_steps}

Now that ran the starter application, you can try other [{{site.data.keyword.messagehub}} samples](https://github.com/ibm-messaging/event-streams-samples){: external}. Explore [other ways to connect](/docs/EventStreams?topic=EventStreams-kafka_connect){: external} to the {{site.data.keyword.messagehub}} service or find out more about 
[{{site.data.keyword.messagehub}} on IBM Cloud Private](https://ibm.github.io/event-streams/){: external}.

To watch a video that walks you through getting a Java sample to run, see [Getting started with IBM {{site.data.keyword.messagehub}}](https://www.youtube.com/watch?v=XyNy7TcfJOc).{: external}
