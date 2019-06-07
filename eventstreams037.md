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

# Using the Administration REST API
{: #admin_api}

{{site.data.keyword.messagehub}} provides an Administration RESTful API that you can use to create, delete, list, and update topics.
{: shortdesc}

You must retrieve the URL and credential details that are needed to connect to the API from a Service credentials object or service key for the service instance. For information about creating these objects, see 
[Connecting to {{site.data.keyword.messagehub}}](/docs/services/EventStreams?topic=eventstreams-connecting).

The URL for the API's endpoint is provided in the <code>kafka_admin_url</code>property.

The credentials depend on the authentication method and three types of credential are supported:

* **To authenticate using Basic Auth**:<br/> 
    Use the <code>user</code> and <code>api_key</code> properties of the above objects as the username and password. Place these values into the <code>Authorization</code> header of the HTTP request in the form <code>Basic<base64 encoding of username:password joined by a single colon (:)></code>.

* **To authenticate using a bearer token:**<br/> 
    To obtain your token using the IBM Cloud CLI, first log in to IBM Cloud then run the following command: 

    ```
    ibmcloud iam oauth-tokens
    ```
    {: codeblock}

    Place this token in the Authorization header of the HTTP request in the form <code>Bearer<token></code>. Both API key or JWT tokens are supported. 

* ** To authenticate directly using the api_key:**<br/>
    Place the key directly as the value of the <code>X-Auth-Token</code> HTTP header.

For service instances created on the Classic plan, this information is available from your application's VCAP_SERVICES environment variable instead.

For a description of the API with examples, see 
[{{site.data.keyword.messagehub}} admin-rest ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/event-streams-docs/tree/master/admin-rest-api){:new_window}.

You can download the full specification for the API from the [{{site.data.keyword.messagehub}} Admin REST API YAML file ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/event-streams-docs/blob/master/admin-rest-api/admin-rest-api.yaml){:new_window}.
To view the swagger file use Swagger tools, for example [Swagger editor ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://editor.swagger.io/#/){:new_window}.




