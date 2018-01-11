---

copyright:
  years: 2015, 2017
lastupdated: "2017-09-26"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Getting started with Message Hub 
{: #messagehub}

{{site.data.keyword.messagehub_full}} is a scalable,
distributed, high throughput messaging service that enables applications and services to communicate easily and reliably.
{:shortdesc}

Using {{site.data.keyword.messagehub}}, you can
complete the following tasks:

* Offload work to back-end worker processes
* Connect stream data to analytics to realize powerful insights
* Feed event data to multiple applications to react in real time
* Transfer data into another service such as long-term storage

To get started with {{site.data.keyword.messagehub}}
and start sending and receiving messages, you can use the Java™ sample. The sample shows how a producer sends
messages to a consumer using a topic. The same sample program is used to consume messages and
produce messages.

<!-- 11/01/18 - Karen - removing diagram as requested by James
![Java sample overview diagram](getting_started_sample.gif "Overview diagram of Java sample showing the flow of messages.")
-->


Complete the following steps:
{: #getting_started_steps}
 
1. Create a {{site.data.keyword.messagehub}} service instance:

  a. Log in to {{site.data.keyword.Bluemix_notm}} using the web user interface. 
  
  b. Click **CATALOG**.
  
  c. In the **Application Services** section, click **{{site.data.keyword.messagehub}}**. The {{site.data.keyword.messagehub}} service instance page opens.
  
  d. Leave the service unbound in the **Connect to** menu and enter names for your service and your credentials. You can use the default values.
  
  e. Click **Create**.

2. If you don't already have them, install the following prerequisites:

    * [git ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://git-scm.com/){:new_window}
	* [Gradle ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://gradle.org/){:new_window}
    * Java 7 or higher
 
3. Clone the message-hub-samples git repository by running the following command from the command line:

    <pre class="pre">
    git clone https://github.com/ibm-messaging/message-hub-samples.git
    </pre>
	{: codeblock}

4. Change directory to the java console sample by running the following command:

    <pre class="pre">
    cd message-hub-samples/kafka-java-console-sample
    </pre>
	{: codeblock}

5. Run the following build commands:

    <pre class="pre">
    gradle clean && gradle build
    </pre>
	{: codeblock}

6. Start the consumer on your console by running the following command:

    <pre class="pre">java -jar build/libs/kafka-java-console-sample-2.0.jar 
	<var class="keyword varname">kafka_brokers_sasl</var> <var class="keyword varname">kafka_admin_url</var> <var class="keyword varname">api_key</var> -consumer</pre>
    {: codeblock}
    
    The sample uses a topic named `kafka-java-console-sample-topic`. If the topic does
    not already exist, the sample creates it using the {{site.data.keyword.messagehub}} Administration API. To send and receive
    messages, the sample uses the Apache Kafka Java API.

    To find the values for *kafka_brokers_sasl*, *kafka_admin_url*,
    and *api_key*, go to your {{site.data.keyword.messagehub}} instance in {{site.data.keyword.Bluemix_notm}}, go to the **Service Credentials** tab, and select the **Credentials** that you want to use.
    
	**Important:** *kafka_brokers_sasl* must be a single string and you must enclose it in quotes. For example:

    <pre class="pre">
    "host1:port1,host2:port2"
    </pre>
	{: codeblock}

    We recommend using all the Kafka hosts listed in the **Credentials** that you selected.

7. Start the producer on your console by running the following command:
   
    <pre class="pre">java -jar build/libs/kafka-java-console-sample-2.0.jar 
	<var class="keyword varname">kafka_brokers_sasl</var> <var class="keyword varname">kafka_admin_url</var> <var class="keyword varname">api_key</var> -producer</pre>
 {: codeblock}
  
8. You should now see the messages sent by the producer appearing in the consumer. The following
is some sample output:

    ```
    [2016-11-30 17:30:53,492] INFO Running in local mode. (com.messagehub.samples.MessageHubConsoleSample)
    [2016-11-30 17:30:53,492] INFO Updating JAAS configuration (com.messagehub.samples.MessageHubConsoleSample)
    [2016-11-30 17:30:53,506] INFO Kafka Endpoints: kafka01-prod01.messagehub.services.us-south.bluemix.net:9093,kafka02-prod01.messagehub.services.us-south.bluemix.net:9093,kafka03-prod01.messagehub.services.us-south.bluemix.net:9093,kafka04-prod01.messagehub.services.us-south.bluemix.net:9093,kafka05-prod01.messagehub.services.us-south.bluemix.net:9093 (com.messagehub.samples.MessageHubConsoleSample)
    [2016-11-30 17:30:53,506] INFO Admin REST Endpoint: https://kafka-admin-prod01.messagehub.services.us-south.bluemix.net:443 (com.messagehub.samples.MessageHubConsoleSample)
    [2016-11-30 17:30:53,506] INFO Creating the topic kafka-java-console-sample-topic (com.messagehub.samples.MessageHubConsoleSample)
    (com.messagehub.samples.MessageHubConsoleSample)e :{}
    [2016-11-30 17:30:54,947] INFO Admin REST Listing Topics: [{"name":"kafka-java-console-sample-topic","partitions":1,"retentionMs":"86400000","markedForDeletion":false}] (com.messagehub.samples.MessageHubConsoleSample)
    [2016-11-30 17:30:55,952] INFO [Partition(topic = kafka-java-console-sample-topic, partition = 0, leader = 0, replicas = [0,1,4,], isr = [0,4,1,]] (com.messagehub.samples.ConsumerRunnable)
    [2016-11-30 17:30:55,953] INFO class com.messagehub.samples.ConsumerRunnable is starting. (com.messagehub.samples.ConsumerRunnable)
    [2016-11-30 17:30:57,023] INFO [Partition(topic = kafka-java-console-sample-topic, partition = 0, leader = 0, replicas = [0,1,4,], isr = [0,4,1,]] (com.messagehub.samples.ProducerRunnable)
    [2016-11-30 17:30:57,024] INFO MessageHubConsoleSample will run until interrupted. (com.messagehub.samples.MessageHubConsoleSample)
    [2016-11-30 17:30:57,024] INFO class com.messagehub.samples.ProducerRunnable is starting. (com.messagehub.samples.ProducerRunnable)
    [2016-11-30 17:30:58,018] INFO Message produced, offset: 0 (com.messagehub.samples.ProducerRunnable)
    [2016-11-30 17:30:58,956] INFO No messages consumed (com.messagehub.samples.ConsumerRunnable)
    [2016-11-30 17:31:00,301] INFO Message consumed: ConsumerRecord(topic = kafka-java-console-sample-topic, partition = 0, offset = 1, CreateTime = 1480527060022, checksum = 1906962734, serialized key size = 3, serialized value size = 25, key = key, value = This is a test message #1) (com.messagehub.samples.ConsumerRunnable)
    [2016-11-30 17:31:00,397] INFO Message produced, offset: 1 (com.messagehub.samples.ProducerRunnable)
    [2016-11-30 17:31:02,550] INFO Message consumed: ConsumerRecord(topic = kafka-java-console-sample-topic, partition = 0, offset = 2, CreateTime = 1480527062401, checksum = 3801731428, serialized key size = 3, serialized value size = 25, key = key, value = This is a test message #2) (com.messagehub.samples.ConsumerRunnable)
    ```
	{: codeblock}
	
9. The sample runs indefinitely until you stop it. To stop the process, run a command like the
following: <code>Ctrl+C</code>


To find out more about running a {{site.data.keyword.messagehub}} sample using Python, see [Python console sample application ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/messaging/2017/02/09/new-message-hub-sample-python-console-application/){:new_window}. You can also find samples
that demonstrate other APIs and features at [{{site.data.keyword.messagehub}} samples ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/message-hub-samples){:new_window}.

To watch a video that walks
you through getting a Java sample to run against {{site.data.keyword.messagehub}}, see [{{site.data.keyword.messagehub}} - Getting started with IBM's Kafka in the cloud ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.youtube.com/watch?v=tt-bLtFzC_4){:new_window}.

