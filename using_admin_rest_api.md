---

copyright:
  years: 2015, 2019
lastupdated: "2019-05-15"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: EventStreams

---

{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Using the Administration REST API
{: #admin_api}

{{site.data.keyword.messagehub}} provides an Administration RESTful API that you can use to create, delete, list, and update topics.
{: shortdesc}

You must retrieve the URL and credential details that are needed to connect to the API from a Service credentials object or service key for the service instance. For information about creating these objects, see 
[Connecting to {{site.data.keyword.messagehub}}](/docs/EventStreams?topic=EventStreams-connecting).

The URL for the API's endpoint is provided in the `kafka_admin_url` property.

The credentials depend on the authentication method and three types of credential are supported:

* **To authenticate using Basic Auth**:

    Use the `user` and `api_key` properties of the above objects as the username and password. Place these values into the `Authorization` header of the HTTP request in the form `Basic <base64 encoding of username and password joined by a single colon (:)>`.

* **To authenticate using a bearer token:** 

    To obtain your token using the IBM Cloud CLI, first log in to IBM Cloud then run the following command: 

    ```text
    ibmcloud iam oauth-tokens
    ```
    {: codeblock}

    Place this token in the Authorization header of the HTTP request in the form `Bearer<token>`. Both API key or JWT tokens are supported. 

* **To authenticate directly using the api_key:**

    Place the key directly as the value of the `X-Auth-Token` HTTP header.

For a description of the API with examples, see 
[{{site.data.keyword.messagehub}} admin-rest](https://github.com/ibm-messaging/event-streams-docs/tree/master/admin-rest-api){: external}.

You can download the full specification for the API from the [{{site.data.keyword.messagehub}} Admin REST API YAML file](https://github.com/ibm-messaging/event-streams-docs/blob/master/admin-rest-api/admin-rest-api.yaml){: external}.
To view the swagger file, use Swagger tools, for example [Swagger editor](http://editor.swagger.io/#/){: external}.





