---

copyright:
  years: 2015, 2018
lastupdated: "2018-04-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Getting started with the Alpha program
{: #alpha_program}

The Alpha program provides early access to the next version of the {{site.data.keyword.messagehub}} service. 

Complete the following steps to get an app running with the {{site.data.keyword.messagehub}} Alpha:


## Create the {{site.data.keyword.messagehub}} service
{: alpha_create}


  1. Click the **Message Hub** tile, which is a service in the 
[catalog ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.stage1.bluemix.net/catalog/services/message-hub).</li>

  2. Create a {{site.data.keyword.messagehub}} service using the <code>Premium</code> pricing plan. This service provides a single-tenant cluster and typically takes 1-3 hours to provision.
 


## Get credentials using the console option: create and connect a test app
{: alpha_app}

You'll need credentials to work with {{site.data.keyword.messagehub}}. 
If you don't already have an app you can use, create a test app and use the credentials the app uses to connect to {{site.data.keyword.messagehub}}. For example, use the **SDK for Node.js** service for a test app. 

  1. Navigate to the **SDK for Node.js** tile in the [catalog ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.stage1.bluemix.net/catalog/starters/sdk-for-nodejs).
   
  Before you enter an app name, ensure that you select a region of US South. Create the app.

  2. When the app is running, click the **Connections** tab on the left.

  3. Click **Create connection** button.

  4. Select your new {{site.data.keyword.messagehub}} service from the list of existing compatible services and click the **Connect** button.

  5. In the **Connect IAM-Enabled Service** window, accept the defaults and click **Connect**.
  Ensure your {{site.data.keyword.messagehub}} service is provisioned so that you can connect to it.

  6. Click the **Runtime** tab on the left and select the **Environment variables** tab in the center. In the **VCAP_SERVICES** section, locate the <code>kafka_admin_url</code>, <code>apikey</code>, and <code>kafka_brokers_sasl</code> information, which you'll need to be able to send a message.
  
## Get credentials using the command line option
Alternatively, you can get the required credentials using the command line. Complete the following steps:

  1. Install the {{site.data.keyword.Bluemix_notm}} command line tool from [{{site.data.keyword.Bluemix_notm}} CLI ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/cli/index.html#overview).
  
  2. Log in to the {{site.data.keyword.Bluemix_notm}} CLI.
  
  3. Use the {{site.data.keyword.Bluemix_notm}} CLI to create a service key with the Manager role using the following command:
  ```
  bx resource service-key-create <NAME> Manager --instance-name <MESSAGEHUB_SERVICE_INSTANCE_NAME>
  ```
  4. The output contains the apikey, the admin REST endpoint URL, and broker list. You can view this information again by running the following command:
  ```
  bx resource service-key <NAME>
  ```

## Create a {{site.data.keyword.messagehub}} topic and send a message

You can use a CURL command to create a topic and then the kafkacat tool to produce and consume a message. 

For each command, replace APIKEY and KAFKA_ADMIN_URL with values from your VCAP_SERVICES environment variable.

  1. From the command line, create a {{site.data.keyword.messagehub}} topic using the following CURL command:
  
    ```
    curl -i -X POST -H "Content-Type: application/json" -H "X-Auth-Token: APIKEY" --data '{ "name": "newtop"}' KAFKA_ADMIN_URL/admin/topics
    ```
    {: codeblock}

  2. Install the [kafkacat tool![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/edenhill/kafkacat#install), which is useful for a quick test of Kafka.
  
  3. To run the next commands, you need the following information:
  
    * Your brokers list, which was returned in your credentials `kafka_brokers_sasl`. Your brokers list must be a comma-separated list for kafkacat. 
	Only your first five brokers are listed in VCAP_SERVICES. If you have more than five brokers, use a Kafka client to retrieve the details of you other brokers. 
  
    * Your <code>apikey</code>. The first 8 characters form your sasl.username and the remainder of the <code>apikey</code> forms your sasl.password.
    * The location of your SSL certificates. For example, on Ubuntu the SSL_CERTS_DIRECTORY is <code>/etc/ssl/certs/</code>
  
  4. Produce some messages by running a command like the following:
  ```
  kafkacat -X "security.protocol=sasl_ssl" -X 'sasl.mechanisms=PLAIN' -X 'sasl.username=<FIRST_8_CHARS_FROM_APIKEY>' -X 'sasl.password=<REMAINING_CHARS_FROM_APIKEY>' -X "ssl.ca.location=<SSL_CERTS_DIRECTORY>" -b <BROKERS_LIST> -P -t <TOPIC_NAME>
    ```
		
	<br/>
  After running the command, you can enter some text like <code>HelloWorld</code> in the producer terminal.
  
  5. Consume the messages by running a command like the following:
  ```
  kafkacat -X "security.protocol=sasl_ssl" -X 'sasl.mechanisms=PLAIN' -X 'sasl.username=<FIRST_8_CHARS_FROM_APIKEY>' -X 'sasl.password=<REMAINING_CHARS_FROM_APIKEY>' -X "ssl.ca.location=<SSL_CERTS_DIRECTORY>" -b <BROKERS_LIST> -C -t <TOPIC_NAME> -f 'Topic %t [%p] at offset %o: key %k: %s\n'
  ```
	
	<br/>
  You should see <code>HelloWorld</code> in the consumer terminal.

