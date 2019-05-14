---

copyright:
  years: 2015, 2019
lastupdated: "2019-05-14"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Using the Administration REST API
{: #admin_api}

{{site.data.keyword.messagehub}} provides an Administration RESTful API that you can use to create, delete, list, and update topics.
{: shortdesc}

You must retrieve the URL and credential details that are needed to connect to the API from a Service credentials object or service key for the service instance. For information about creating these objects, see 
[Connecting to {{site.data.keyword.messagehub}}](/docs/services/EventStreams?topic=eventstreams-connecting).

The URL for the API's endpoint is provided in the ```kafka_admin_url```property.

The credentials depend on the authentication method and two types of credential are supported:
* **Basic Auth**:<br/> 
    Use the ```user``` and ```api_key``` properties of the above objects as the username and password fields for Basic Auth, where the ```Authorization``` HTTP header of the request is set to the ```Basic <base64 encoding of username and password joined by a single colon (:)>```.

* **Bearer Token**:<br/>
    You can obtain this credential from IAM after logging in to {{site.data.keyword.Bluemix_notm}}, where the ```Authorization``` HTTP header of the request is set to `Bearer <token>`. If you're using the {{site.data.keyword.Bluemix_notm}} CLI, use the following command to retrieve the token after logging into ibmcloud:

    ```
    ibmcloud iam oauth-tokens
    ```
    {: codeblock}

    Both API key or JWT tokens are supported. 

For service instances created on the Classic plan, this information is available from your application's VCAP_SERVICES environment variable instead.

For a description of the API with examples, see 
[{{site.data.keyword.messagehub}} admin-rest ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/event-streams-docs/tree/master/admin-rest-api){:new_window}.

You can download the full specification for the API from the [{{site.data.keyword.messagehub}} Admin REST API yaml file ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/event-streams-docs/blob/master/admin-rest-api/admin-rest-api.yaml){:new_window}.
To view the swagger file use Swagger tools, for example [Swagger editor ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://editor.swagger.io/#/){:new_window}.




