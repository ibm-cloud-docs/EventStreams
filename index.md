---

copyright:
  years: 2015, 2019
lastupdated: "2019-08-08"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}
{:important: .important}

# Getting started tutorial
{: #getting_started}

To get started with {{site.data.keyword.messagehub}}
and start sending and receiving messages, you can use the Java™ sample. The sample shows how a producer sends
messages to a consumer using a topic. The same sample program is used to consume messages and
produce messages.
{: shortdesc}

To understand more about how {{site.data.keyword.messagehub}} works, see [About {{site.data.keyword.messagehub}}](/docs/services/EventStreams?topic=eventstreams-about). {{site.data.keyword.messagehub}} was previously called Message Hub.

To access other {{site.data.keyword.messagehub}} samples, including samples for Node.js and Python, see [{{site.data.keyword.messagehub}} samples ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/event-streams-samples){:new_window}.

<!-- 11/01/18 - Karen - removing diagram as requested by James
![Java sample overview diagram](getting_started_sample.gif "Overview diagram of Java sample showing the flow of messages.")
-->
<!-- 08/08/2019 - Chloe - Re-structuring to get UI components of the flow introduced earlier in the flow. Also moving pre-requsisites to a potentially collapsible section. -->

##Prerequisites##

1. **If you don't already have one, create an {{site.data.keyword.messagehub}} service instance.**
	
   a. Log in to the {{site.data.keyword.Bluemix_notm}} console. 
  
   b. Click **Catalog**.
  
   c. In the **Integration** section, click the {{site.data.keyword.messagehub}} tile and then select the **Lite plan**. The {{site.data.keyword.messagehub}} service instance page opens.
  
   d. Enter a name for your service. You can use the default value.
  
   e. Click **Create**. The {{site.data.keyword.messagehub}} **Getting started** page opens. 

		
2. **If you don't already have them, install the following prerequisites:**
	
	* [git ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://git-scm.com/){:new_window}
	* [Gradle ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://gradle.org/){:new_window}
     * Java 8 or higher

##Tutorial steps##
{: #getting_started_steps}

1. {: #Create_topic_step notoc} ###Create a topic###

   The topic is the core of {{site.data.keyword.messagehub}} flows. Data passes through a topic from producing applications to consuming applications. 

   We'll be using the UI to create the topic, and then reference it when starting the application.

      a. Go to **Topics**.
  
      b. Click **New topic**.
  
      c. Name your topic.
  
     The sample application is configured to connect to topic `kafka-java-console-sample-topic`. If the topic does not exist, it will be created when the application is started. {: important}

     d. Observe the defaults set in the rest of the topic creation, click **Next** and then **Create topic**.
  
     e. The topic appears in the table. Congratulations, you have created a topic!
  
2. {: #create_credentials_step notoc} ###Create credentials###

    To allow the sample application to access your topic, we need to create some credentials for it. 

     a. Go to **Service credentials**.
  
     b. Click **New credential**.
  
     c. Give the credential a name so you can identify its purpose later. You can use the default value.
  
     d. Give the credential the **Manager** role so that it can access the topics, and create them if necessary. 
  
     e. Click **Create**. The new credential is listed in the table in **Service credentials**.
  
     f. Click **View credentials** to see the `API key` and `kafka_brokers_sasl`.
3.  {: #clone_repository_step notoc} ###Clone the Github repository for the sample application###
    The sample application is stored in Github. Clone the `event-streams-samples` repository by running the clone command from the command line. 

    <pre class="pre">
    git clone https://github.com/ibm-messaging/event-streams-samples.git
    </pre>

    When the repository is cloned, change the command line directory into the `kafka-java-console-sample` directory.

    <pre class="pre">
    cd event-streams-samples/kafka-java-console-sample
    </pre>

    Build the contents of the `kafka-java-console-sample` directory.

    <pre class="pre">
    gradle clean && gradle build
    </pre>
4. {: #start_consumer_step notoc} ###Run the consuming application###
   Start the sample consuming application from the command line, replacing the _`italicised`_ values. 

    <pre class="pre">java -jar ./build/libs/kafka-java-console-sample-2.0.jar
	"<var class="keyword varname">kafka_brokers_sasl</var>" "<var class="keyword varname">api_key</var>" -consumer</pre>
  
   The `java -jar ./build/libs/kafka-java-console-sample-2.0.jar` part of the command identified the locations of the java .JAR file to run within the cloned repository. This does not need to be changed. 

   Use the `kafka_brokers_sasl` from the **Service credentials** created in [Step 2](/docs/services/EventStreams?topic=eventstreams-getting_started#create_credentials_step). We recommend using all the `kafka_brokers_sasl` listed in the **Service credentials** that you created.

   The `kafka_brokers_sasl` must be formatted as `"host:port,host2:port2"`. Format the contents of `kafka_brokers_sasl` in a text editor before entering it in the command line. {: important}

   Then, use the `api_key` from the **Service credentials** created in [Step 2](/docs/services/EventStreams?topic=eventstreams-getting_started#create_credentials_step). Add `-consumer` to specify that the consumer should start. 

   An `INFO No messages consumed` is produced when the consuming application is running, but there is no data being consumed. 

5. {: #start_producer_step notoc} ###Run the producing application###
   Open a new command line window and start the sample producing application from the command line, replacing the _`italicised`_ values. 

    <pre class="pre">java -jar ./build/libs/kafka-java-console-sample-2.0.jar
	"<var class="keyword varname">kafka_brokers_sasl</var>" "<var class="keyword varname">api_key</var>" -producer</pre>
  
   The `java -jar ./build/libs/kafka-java-console-sample-2.0.jar` part of the command identified the locations of the java .JAR file to run within the cloned repository. This does not need to be changed. 

   Use the `kafka_brokers_sasl` from the **Service credentials** created in [Step 2](/docs/services/EventStreams?topic=eventstreams-getting_started#create_credentials_step). We recommend using all the `kafka_brokers_sasl` listed in the **Service credentials** that you created.

   The `kafka_brokers_sasl` must be formatted as `"host:port,host2:port2"`. Format the contents of `kafka_brokers_sasl` in a text editor before entering it in the command line. {: important}

   Then, use the `api_key` from the **Service credentials** created in [Step 2](/docs/services/EventStreams?topic=eventstreams-getting_started#create_credentials_step). Add `-producer` to specify that the producer should start. 

5. {: #success_step notoc} ###Success!###
When the producer starts, messages are produced to the topic. Messages are then consumed from the topic by the consuming application.
You can verify the successful flow of messages when `INFO Message consumed` is seen from the consumer. 

   The sample runs indefinitely until you stop it. To stop the process, run an exit command `Ctrl+C`.

##Next steps##

Now that you've run the java sample application, you can try other [{{site.data.keyword.messagehub}} samples ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/event-streams-samples){:new_window}, explore [other ways to connect ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/services/EventStreams?topic=eventstreams-kafka_connect){:new_window} to the {{site.data.keyword.messagehub}} service, or take a look at [IBM Event Streams on IBM Cloud Private and Red Hat OpenShift![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/garage/dte/tutorial/ibm-event-streams-tutorial-part-1).
 
<!-- 07/06/18 - Karen: removing until a newer version available
To watch a video that walks
you through getting a Java sample to run against {{site.data.keyword.messagehub}}, see [{{site.data.keyword.messagehub}} - Getting started with IBM's Kafka in the cloud ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.youtube.com/watch?v=tt-bLtFzC_4){:new_window}.
-->





