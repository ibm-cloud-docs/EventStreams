---

copyright:
  years: 2015, 2019
lastupdated: "2019-05-09"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}

# Using the REST producer API
{: #rest_producer_using}

{{site.data.keyword.messagehub}} provides a REST API to help connect your existing systems to your {{site.data.keyword.messagehub}} Kafka cluster. Using the API, you can integrate {{site.data.keyword.messagehub}} with any system that supports RESTful APIs.

The REST producer API is a scalable REST interface for producing messages to {{site.data.keyword.messagehub}}  over a secure HTTP endpoint. Send event data to {{site.data.keyword.messagehub}}, utilize Kafka technology to handle data feeds, and take advantage of {{site.data.keyword.messagehub}} features to manage your data.

Use the API to connect existing systems to {{site.data.keyword.messagehub}}. Create produce requests from your systems into {{site.data.keyword.messagehub}}, including specifying the message key, headers, and the topics that you want to write messages to.


## Producing messages using REST
{: #rest_produce_messages}

Use the producer API to write messages to topics. To be able to produce to a topic, you must have the following available:

* The URL of the {{site.data.keyword.messagehub}} API endpoint, including the port number.
* The topic you want to produce to.
* The API key that gives permission to connect and produce to the selected topic.
* The {{site.data.keyword.messagehub}} certificate.

To retrieve the full URL for the {{site.data.keyword.messagehub}} API endpoint:

1. Ensure that you have installed the [{{site.data.keyword.messagehub}} CLI](/docs/services/EventStreams?topic=eventstreams-cli).
2. Log in to your cluster as an administrator by using the IBM Cloud CLI:

    ```
    ibmcloud login -a https://<Cluster Master Host>:<Cluster Master API Port>
    ```
    {: codeblock}

    The master host and port for your cluster are set during the installation of IBM Cloud.
3. Run the following command to initialize the {{site.data.keyword.messagehub}} CLI: 
    ```
    ibmcloud es init
    ```
    {: codeblock}
    If you have more than one {{site.data.keyword.messagehub}} instance installed, select the one where the topic you want to produce to is located.
    Details of your {{site.data.keyword.messagehub}} installation are displayed.
4. Copy the full URL from the {{site.data.keyword.messagehub}} API endpoint field, including the port number.

<br/>
To create a topic and generate an API key with produce permissions, and to download the certificate:

1. If you have not previously created the topic, create it now:

    ```
    ibmcloud es topic-create --name <topic_name> --partitions 1 --replication-factor 3
    ```
    {: codeblock}
2. Create a service ID and generate an API key:

    ```
    ibmcloud es iam-service-id-create --name <serviceId_name> --role editor --topic <topic_name>
    ```
    {: codeblock}

    For more information about roles, permissions, and service IDs, see [Managing access to your {{site.data.keyword.messagehub}} resources](/docs/services/EventStreams?topic=eventstreams-security).
3. Copy the API key returned by the previous command.
4. Download the certificate for {{site.data.keyword.messagehub}}:

    ```
    ibmcloud es certificates --format pem
    ```
    {: codeblock}

<br/>
You have now gathered all the details required to use the producer API. You can use the usual languages for making the API call. For example, to use cURL to produce messages to a topic with the producer API, run the curl command as follows:

```
curl -v -X POST -H "Authorization: Bearer <api_key>" -H "Content-Type: text/plain" -H "Accept: application/json" -d 'test message' --cacert es-cert.pem "<api_endpoint>/topics/<topic_name>/records"
```
{: codeblock}

<br/>

Where:

* ```<api_key>``` is the API key that you generated earlier.
* ```<api_endpoint>``` is the full URL copied from the Event Streams API endpoint field earlier (the format is ```https://<host>:<port>```).
* ```<topic_name>``` is the name of the topic you want to produce messages to.

## API reference
{: #rest_api_reference}

For full details of the API, see the 
[{{site.data.keyword.messagehub}} REST Producer API reference yaml file ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.ibm.com/mhub/rest-producer/blob/master/openapi.yaml){:new_window}.






