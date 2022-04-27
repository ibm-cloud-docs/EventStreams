---

copyright:
  years: 2015, 2022
lastupdated: "2022-02-27"

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

To understand more about how {{site.data.keyword.messagehub}} works, see [About {{site.data.keyword.messagehub}}](/docs/EventStreams?topic=EventStreams-about). {{site.data.keyword.messagehub}} was previously called Message Hub.

To access other {{site.data.keyword.messagehub}} samples, including samples for Node.js and Python, see [{{site.data.keyword.messagehub}} samples]](https://github.com/ibm-messaging/event-streams-samples){: external}.

## Prerequisites
{: #getting_started_prereqs}

1. **If you don't already have one, create an {{site.data.keyword.messagehub}} service instance.**

   a. Log in to the {{site.data.keyword.Bluemix_notm}} console.
  
   b. Click the [**{{site.data.keyword.messagehub}} service**](https://cloud.ibm.com/catalog/event-streams){: external} in the **Catalog**.
  
   c. Select the **Lite plan** on the service instance page.
  
   d. Enter a name for your service. You can use the default value.
  
   e. Click **Create**. The {{site.data.keyword.messagehub}} **Getting started** page opens. 

2. **If you don't already have them, install the following prerequisites:**
	
	* [Git](https://git-scm.com/){: external}
	* [Gradle](https://gradle.org/){: external}
	* Java™  8 or higher 

## Tutorial steps
{: #getting_started_steps}

1. **Create a topic**. {: #Create_topic_step notoc}

   The topic is the core of {{site.data.keyword.messagehub}} flows. Data passes through a topic from producing applications to consuming applications. 

   We use the {{site.data.keyword.Bluemix_notm}} console (UI) to create the topic and reference it when we start the application.

      a. Go to the **Topics** tab.
  
      b. Click **New topic**.
  
      c. Name your topic.
  
     The sample application is configured to connect to topic `kafka-java-console-sample-topic`. If the topic does not exist, it is created when the application is started. 
     {: important}

      d. Keep the defaults set in the rest of the topic creation, click **Next**, and then **Create topic**.

      e. The topic appears in the table. You just created a topic!
  
2. **Create credentials**. {: #create_credentials_step notoc}

    To allow the sample application to access your topic, we need to create some credentials for it. 

     a. Go to **Service credentials** in the navigation pane.
  
     b. Click **New credential**.
  
     c. Give the credential a name so you can identify its purpose later. You can accept the default value.
  
     d. Give the credential the **Manager** role so that it can access the topics, and create them if necessary. 
  
     e. Click **Add**. The new credential is listed in the table in **Service credentials**.
  
     f. Click **View credentials** to see the `api_key` and `kafka_brokers_sasl` values.

3. **Clone the GitHub repository for the sample application**. {: #clone_repository_step notoc}

   The sample application is stored in GitHub. Clone the `event-streams-samples` repository by running the clone command from the command line. 

   ```
   git clone https://github.com/ibm-messaging/event-streams-samples.git
   ```
   {: codeblock}

 
   When the repository is cloned, from the command line change into the `kafka-java-console-sample` directory.

   ```
   cd event-streams-samples/kafka-java-console-sample
   ```
   {: codeblock}
   

   Build the contents of the `kafka-java-console-sample` directory.

   ```
   gradle clean && gradle build
   ```
   {: codeblock}

4. **Run the consuming application** {: #start_consumer_step notoc}
   
   Start the sample consuming application from the command line, replacing the `kafka_brokers_sasl` and `api_key` values. 

   The `java -jar ./build/libs/kafka-java-console-sample-2.0.jar` part of the command identifies the locations of the .JAR file to run within the cloned repository. You do not need to change this value. 
   
   Use the `kafka_brokers_sasl` from the **Service credentials** created in [Step 2](/docs/EventStreams?topic=EventStreams-getting_started#create_credentials_step). 
   Use all the `kafka_brokers_sasl` listed in the **Service credentials** that you created.

   The `kafka_brokers_sasl` must be formatted as `"host:port,host2:port2"`. 
   Format the contents of `kafka_brokers_sasl` in a text editor before you enter it in the command line.
   {: important}

   Then, use the `api_key` from the **Service credentials** created in [Step 2](/docs/EventStreams?topic=EventStreams-getting_started#create_credentials_step). `-consumer` indicates to start the consumer. 

   ```
   java -jar ./build/libs/kafka-java-console-sample-2.0.jar \
   <kafka_brokers_sasl> <api_key> -consumer
   ```
   {: codeblock}

   An `INFO No messages consumed` is displayed when the consuming application is running, but no data is consumed. 

5. **Run the producing application**. {: #start_producer_step notoc}

   Open a new command line window and change into the `kafka-java-console-sample` directory.

   ```
   cd event-streams-samples/kafka-java-console-sample
   ```
   {: codeblock}
   
   Then, start the application that produces the sample from the command line, and replace the `kafka_brokers_sasl` and `api_key` values. 

   The `java -jar ./build/libs/kafka-java-console-sample-2.0.jar` part of the command identifies the locations of the .JAR file to run within the cloned repository. You do not need to change this value. 

   Use the `kafka_brokers_sasl` from the **Service credentials** created in [Step 2](/docs/EventStreams?topic=EventStreams-getting_started#create_credentials_step). We recommend to use all the `kafka_brokers_sasl` listed in the **Service credentials** that you created.

   The `kafka_brokers_sasl` must be formatted as `"host:port,host2:port2"`. 
   Format the contents of `kafka_brokers_sasl` in a text editor before you enter it in the command line.
   {: important}

   Use the `api_key` from the **Service credentials** created in [Step 2](/docs/EventStreams?topic=EventStreams-getting_started#create_credentials_step). `-producer` initiates to start the producer. 

   ```
   java -jar ./build/libs/kafka-java-console-sample-2.0.jar \
   <kafka_brokers_sasl> <api_key> -producer
   ```
   {: codeblock}

6. **Success!** {: #success_step notoc}

   When the producer starts, messages are produced to the topic. Messages are then consumed from the topic by the consuming application.
   You can verify the successful flow of messages when you see`INFO Message consumed` from the consumer. 

   The sample runs indefinitely until you stop it. To stop the process, run an exit command `Ctrl+C`.

## Next steps
{: #next_steps}

Now that ran the Java sample application, you can try other [{{site.data.keyword.messagehub}} samples](https://github.com/ibm-messaging/event-streams-samples){: external}. Explore [other ways to connect](/docs/EventStreams?topic=EventStreams-kafka_connect){: external} to the {{site.data.keyword.messagehub}} service, look at the [IBM Event Streams on IBM Cloud Private and Red Hat OpenShift](https://www.ibm.com/cloud/garage/dte/tutorial/ibm-event-streams-tutorial-part-1) {: external} tutorial, or find out more about 
[{{site.data.keyword.messagehub}} on IBM Cloud Private](https://ibm.github.io/event-streams/){: external}.

To watch a video that walks you through getting this Java sample to run, see [Getting started with IBM {{site.data.keyword.messagehub}}](https://www.youtube.com/watch?v=XyNy7TcfJOc).{: external}
