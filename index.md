---

copyright:
  years: 2015, 2019
lastupdated: "2019-05-08"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}

# Getting started tutorial
{: #getting_started}


To get started with {{site.data.keyword.messagehub}}
and start sending and receiving messages, you can use the Java™ sample. The sample shows how a producer sends
messages to a consumer using a topic. The same sample program is used to consume messages and
produce messages.
{: shortdesc}

To understand more about how {{site.data.keyword.messagehub}} works, see [About {{site.data.keyword.messagehub}}](/docs/services/EventStreams?topic=eventstreams-about#about). {{site.data.keyword.messagehub}} was previously called Message Hub.

To access other {{site.data.keyword.messagehub}} samples, including samples for Node.js and Python, see [{{site.data.keyword.messagehub}} samples ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/event-streams-samples){:new_window}.

<!-- 11/01/18 - Karen - removing diagram as requested by James
![Java sample overview diagram](getting_started_sample.gif "Overview diagram of Java sample showing the flow of messages.")
-->

Complete the following steps:
{: #getting_started_steps}
 
1. Create an {{site.data.keyword.messagehub}} service instance:

  a. Log in to the {{site.data.keyword.Bluemix_notm}} console. 
  
  b. Click **Catalog**.
  
  c. In the **Integration** section, click the {{site.data.keyword.messagehub}} tile and then select the **Standard plan**. The {{site.data.keyword.messagehub}} service instance page opens.
  
  d. Enter a name for your service. You can use the default value.
  
  e. Click **Create**.

2. {: #create_credentials_step notoc} Create some {{site.data.keyword.messagehub}} credentials by completing these steps: [get credentials and connect using the IBM Cloud console](/docs/services/EventStreams?topic=eventstreams-connecting#connect_standard_cf_console).
   <br/>
   <br/>You'll need the values of *kafka_brokers_sasl* and *api_key* for [step 7](/docs/services/EventStreams?topic=eventstreams-getting_started#start_consumer_step) of this task.   

3. If you don't already have them, install the following prerequisites:

    * [git ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://git-scm.com/){:new_window}
	* [Gradle ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://gradle.org/){:new_window}
    * Java 8 or higher
 
4. Clone the event-streams-samples git repository by running the following command from the command line:

    <pre class="pre">
    git clone https://github.com/ibm-messaging/event-streams-samples.git
    </pre>

5. Change directory to the java console sample by running the following command:

    <pre class="pre">
    cd event-streams-samples/kafka-java-console-sample
    </pre>

6. Run the following build commands:

    <pre class="pre">
    gradle clean && gradle build
    </pre>

7. {: #start_consumer_step notoc} Start the consumer on your console by running the following command:

    <pre class="pre">java -jar ./build/libs/kafka-java-console-sample-2.0.jar
	<var class="keyword varname">kafka_brokers_sasl</var> <var class="keyword varname">api_key</var> -consumer</pre>
    
    The sample uses a topic named `kafka-java-console-sample-topic`. If the topic does
    not already exist, the sample creates it using the {{site.data.keyword.messagehub}} Administration API. To send and receive
    messages, the sample uses the Apache Kafka Java API.

    Use the values for *kafka_brokers_sasl*
    and *api_key* from the credentials you created in [step 2](/docs/services/EventStreams?topic=eventstreams-getting_started#create_credentials_step).
	
	<br/>
    
	**Important:** *kafka_brokers_sasl* must be a single string and you must enclose it in quotes. For example:

    <pre class="pre">
    "host1:port1,host2:port2"
    </pre>

    We recommend using all the Kafka hosts listed in the **Credentials** that you selected.

8. Start the producer on your console by running the following command:
   
    <pre class="pre">java -jar ./build/libs/kafka-java-console-sample-2.0.jar
	<var class="keyword varname">kafka_brokers_sasl</var> <var class="keyword varname">api_key</var> -producer</pre>
  
9. You should now see the messages sent by the producer appearing in the consumer. The following
is some sample output:

    ```
    [2018-07-02 14:54:50,788] INFO Running in local mode. (com.messagehub.samples.MessageHubConsoleSample)
    [2018-07-02 14:54:50,789] INFO Kafka Endpoints: kafka-0.mh-zarjkgtnzzspbkfrkqgdhmq.us-south.containers.appdomain.cloud:9093,kafka-1.mh-zarjkgtnzzspbkfrkqgdhmq.us-south.containers.appdomain.cloud:9093,kafka-2.mh-zarjkgtnzzspbkfrkqgdhmq.us-south.containers.appdomain.cloud:9093 (com.messagehub.samples.MessageHubConsoleSample)
    [2018-07-02 14:54:50,789] INFO Admin REST Endpoint: https://mh-zarjkgtnzzspbkfrkqgdhmq.us-south.containers.appdomain.cloud (com.messagehub.samples.MessageHubConsoleSample)
    [2018-07-02 14:54:50,789] INFO Creating the topic kafka-java-console-sample-topic (com.messagehub.samples.MessageHubConsoleSample)
    [2018-07-02 14:54:52,680] INFO Admin REST response : (com.messagehub.samples.MessageHubConsoleSample)
    [2018-07-02 14:54:53,351] INFO Admin REST Listing Topics: [{"name":"kafka-java-console-sample-topic","partitions":1,"retentionMs":86400000,"cleanupPolicy":"delete"},{"name":"__consumer_offsets","partitions":50,"retentionMs":86400000,"cleanupPolicy":"compact"}] (com.messagehub.samples.MessageHubConsoleSample)
    [2018-07-02 14:54:55,126] INFO [Partition(topic = kafka-java-console-sample-topic, partition = 0, leader = 0, replicas = [0,2,1], isr = [0,2,1], offlineReplicas = [])] (com.messagehub.samples.ConsumerRunnable)
    [2018-07-02 14:54:55,126] INFO class com.messagehub.samples.ConsumerRunnable is starting. (com.messagehub.samples.ConsumerRunnable)
    [2018-07-02 14:54:56,328] INFO [Partition(topic = kafka-java-console-sample-topic, partition = 0, leader = 0, replicas = [0,2,1], isr = [0,2,1], offlineReplicas = [])] (com.messagehub.samples.ProducerRunnable)
    [2018-07-02 14:54:56,328] INFO MessageHubConsoleSample will run until interrupted. (com.messagehub.samples.MessageHubConsoleSample)
    [2018-07-02 14:54:56,328] INFO class com.messagehub.samples.ProducerRunnable is starting. (com.messagehub.samples.ProducerRunnable)
    [2018-07-02 14:54:57,514] INFO Message produced, offset: 0 (com.messagehub.samples.ProducerRunnable)
    [2018-07-02 14:54:59,652] INFO Message produced, offset: 1 (com.messagehub.samples.ProducerRunnable)
    [2018-07-02 14:55:00,671] INFO No messages consumed (com.messagehub.samples.ConsumerRunnable)
    [2018-07-02 14:55:01,788] INFO Message produced, offset: 2 (com.messagehub.samples.ProducerRunnable)
    [2018-07-02 14:55:01,797] INFO Message consumed: ConsumerRecord(topic = kafka-java-console-sample-topic, partition = 0, offset = 2, CreateTime = 1530539701655, serialized key size = 3, serialized value size = 25, headers = RecordHeaders(headers = [], isReadOnly = false), key = key, value = This is a test message #2) (com.messagehub.samples.ConsumerRunnable)
    [2018-07-02 14:55:03,921] INFO Message consumed: ConsumerRecord(topic = kafka-java-console-sample-topic, partition = 0, offset = 3, CreateTime = 1530539703789, serialized key size = 3, serialized value size = 25, headers = RecordHeaders(headers = [], isReadOnly = false), key = key, value = This is a test message #3) (com.messagehub.samples.ConsumerRunnable)
    [2018-07-02 14:55:03,921] INFO Message produced, offset: 3 (com.messagehub.samples.ProducerRunnable)
    [2018-07-02 14:55:06,053] INFO Message consumed: ConsumerRecord(topic = kafka-java-console-sample-topic, partition = 0, offset = 4, CreateTime = 1530539705922, serialized key size = 3, serialized value size = 25, headers = RecordHeaders(headers = [], isReadOnly = false), key = key, value = This is a test message #4) (com.messagehub.samples.ConsumerRunnable)
    [2018-07-02 14:55:06,054] INFO Message produced, offset: 4 (com.messagehub.samples.ProducerRunnable)
    [2018-07-02 14:55:08,186] INFO Message consumed: ConsumerRecord(topic = kafka-java-console-sample-topic, partition = 0, offset = 5, CreateTime = 1530539708055, serialized key size = 3, serialized value size = 25, headers = RecordHeaders(headers = [], isReadOnly = false), key = key, value = This is a test message #5) (com.messagehub.samples.ConsumerRunnable)
    ```
	{: codeblock}
	
10. The sample runs indefinitely until you stop it. To stop the process, run a command like the
following: <code>Ctrl+C</code>

<!-- 07/06/18 - Karen: removing until a newer version available
To watch a video that walks
you through getting a Java sample to run against {{site.data.keyword.messagehub}}, see [{{site.data.keyword.messagehub}} - Getting started with IBM's Kafka in the cloud ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.youtube.com/watch?v=tt-bLtFzC_4){:new_window}.
-->



