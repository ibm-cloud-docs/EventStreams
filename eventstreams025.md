---

copyright:
  years: 2015, 2019
lastupdated: "2019-05-15"

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


** The REST producer API is available as part of the new {{site.data.keyword.messagehub}} Standard plan only.**
<br/>

{{site.data.keyword.messagehub}} provides a REST API to help connect your existing systems to your {{site.data.keyword.messagehub}} Kafka cluster. Using the API, you can integrate {{site.data.keyword.messagehub}} with any system that supports RESTful APIs.

The REST producer API is a scalable REST interface for producing messages to {{site.data.keyword.messagehub}} over a secure HTTP endpoint. Send event data to {{site.data.keyword.messagehub}}, utilize Kafka technology to handle data feeds, and take advantage of {{site.data.keyword.messagehub}} features to manage your data.

Use the API to connect existing systems to {{site.data.keyword.messagehub}}. Create produce requests from your systems into {{site.data.keyword.messagehub}}, including specifying the message key, headers, and the topics that you want to write messages to.


## Producing messages using REST
{: #rest_produce_messages}

Use the producer API to write messages to topics. To be able to produce to a topic, you must have the following information available:

* The URL of the {{site.data.keyword.messagehub}} API endpoint, including the port number.
* The topic you want to produce to.
* The API key that gives permission to connect and produce to the selected topic.

You must retrieve the URL and credential details that are needed to connect to the API from a Service credentials object or service key for the service instance. For information about creating these objects, see 
[Connecting to {{site.data.keyword.messagehub}}](/docs/services/EventStreams?topic=eventstreams-connecting).

The URL for the API's endpoint is provided in the ```kafka_http_url``` property.

Use one of the following methods to authenticate:

* **To authenticate using Basic Auth:**<br/> 
    Use the ```user``` and ```api_key``` properties of the above objects as the username and password. Place these values into the ```Authorization``` header of the HTTP request in the form ```Basic <base64 encoding of username:password joined by a single colon (:)>```.

* **To authenticate using a bearer token:**<br/> 
    To obtain your token using the IBM Cloud CLI, first log in to IBM Cloud then run the following command: 

    ```
    ibmcloud iam oauth-tokens
    ```
    {: codeblock}

    Place this token in the Authorization header of the HTTP request in the form ```Bearer <token>```. Both API key or JWT tokens are supported. 

* ** To authenticate directly using the api_key:**<br/> 
    Place the key directly as the value of the ```X-Auth-Token``` HTTP header.

<br/>
The following code shows an example of sending a message using curl:

```
curl -v -X POST -H "Authorization: Basic <base64 username:password>" -H "Content-Type: text/plain" -H "Accept: application/json" -d 'test message' "<kafka_http_url>/topics/<topic_name>/records"
```
{: codeblock}


## API reference
{: #rest_api_reference}

For full details of the API, see the 
[{{site.data.keyword.messagehub}} REST Producer API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://ibm.github.io/event-streams/api/){:new_window}.








