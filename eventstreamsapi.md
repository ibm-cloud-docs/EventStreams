---

copyright:
  years: 2015, 2019
lastupdated: "2019-04-04"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}

# API experiment
{: #api_rest}

## Introduction
{: #es_api_intro}

The resource controller is the next-generation IBM Cloud platform provisioning layer that manages the lifecycle of IBM Cloud resources in a customer account. Resources is a broad term that could mean anything from an instance of a service like Cloudant, a Cloud Foundry application, a virtual machine, a container, a software image, a data set, or other entities associated to the customer account.

The resource controller provides common APIs to control the lifecycle of resources from provisioning (creating an instance) to binding (creating access credentials) to unbinding (removing access) to de-provisioning (deleting an instance).  Resources are provisioned globally in an account scope. The resource controller supports both synchronous and asynchronous provisioning of resources.

Resources are created by the resource controller within [resource groups](https://console.cloud.ibm.com/docs/overview/resource-groups.html#whatis). A resource group belongs to an account. All IBM Cloud resources must be provisioned within a resource group. If an account is suspended, the corresponding resource group are suspended as well, and all resources within the resource group are suspended.

## Introduction
{: #intro_es}

IBM {{site.data.keyword.messagehub}} for IBM Cloud is a high-throughput message bus built with Apache Kafka. It is optimized for event ingestion into IBM Cloud and event stream distribution between your services and applications. {{site.data.keyword.messagehub}} was previously known as Message Hub.

{{site.data.keyword.messagehub}} provides a REST API to help connect your existing systems to your {{site.data.keyword.messagehub}} Kafka cluster. Using the API, you can integrate {{site.data.keyword.messagehub}} with any system that supports RESTful APIs.

The REST producer API is a scalable REST interface for producing messages to {{site.data.keyword.messagehub}} over a secure HTTP endpoint. Send event data to {{site.data.keyword.messagehub}}, utilize Kafka technology to handle data feeds, and take advantage of {{site.data.keyword.messagehub}} features to manage your data.

Use the API to connect existing systems to {{site.data.keyword.messagehub}}. Create produce requests from your systems into {{site.data.keyword.messagehub}}, including specifying the message key, headers, and the topics that you want to write messages to.



### Resource aliases

You can think of an alias as a symlink in computing terms. It represents an entity that points back to a resource instance and enables you to define different access controls on it. As with symlinks you can also create multiple aliases to a single resource instance and manage each one separately.

For example, you can create an instance of a service and then reuse that instance in both London and Dallas by creating aliases in both regions. This enables you to bind keys (credentials) to applications that run in those regions and utilize the same logical instance.

## Example (Displayed on the right)
{: curl}
{: right}

API endpoint

```bash
https://resource-controller.cloud.ibm.com/v2/
```


## Error handling
{: #errors}

This API uses standard HTTP response codes to indicate whether a method completed successfully. A `200` response indicates success. A `400` type response indicates a failure, and a `500` type response indicates an internal system error.

| HTTP Error Code | Description | Recovery |
|-----------------|-------------|----------|
| `200` | Success | The request was successful. |
| `400` | Bad Request | The input parameters in the request body are either incomplete or in the wrong format. Be sure to include all required parameters in your request. |
| `401` | Unauthorized | You are not authorized to make this request. Log in to {{site.data.keyword.Bluemix_notm}} and try again. If this error persists, contact the account owner to check your permissions.	|
| `403` | Forbidden | The supplied authentication is not authorized to access '{namespace}'. |
| `404` | Not Found | The requested resource could not be found. |
| `409` | Conflict | The entity is already in the requested state. |
| `410` | Gone | The resource is valid but has been removed already in a previous call |
| `500` | Internal Server Error | *offering_name* is currently unavailable. Your request could not be processed. Wait a few minutes and try again. |

## Authentication
{: #authentication}

To work with the API, authenticate your app or service by including your IBM Cloud IAM access token in the API request authentication header:

```
-H 'Authorization: Bearer <IAM_TOKEN>'
```

You can retrieve an access token by first creating an API key, and then exchanging your API key for a IBM Cloud IAM token. For more information, see [Getting an IBM Cloud IAM token by using an API key](https://console.cloud.ibm.com/docs/iam/apikey_iamtoken.html#iamtoken_from_apikey).
{: tip}

## Example (Displayed on the right)
{: curl}
{: right}

To retrieve your access token:

```bash
curl -X POST
https://iam.cloud.ibm.com/identity/token
  -H "Content-Type: application/x-www-form-urlencoded"
  -H "Accept: application/json"
  -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<API_KEY>"
```

Replace `<API_KEY>` with your service credentials. Then use the full `IAM token` value, prefixed by the _Bearer_ token type, to authenticate your API requests.

To retrieve your instance ID:

```bash
ibmcloud resource service-instance <instance_name> --id
```

Replace `<instance_name>` with the unique alias that you assigned to your service instance.


## Pagination

Some API requests might return a large number of results. To avoid performance issues, these results are returned one page at a time, with a limited number of results on each page. GET requests for the following resources use pagination:

   * /v2/resource_instances
   * /v2/resource_bindings
   * /v2/resource_keys
   * /v2/resource_aliases

The default page and max size is 100 objects. To use a different page size, use the `limit` query parameter.

For any request that uses pagination, the response includes a `next_url` object that specifies pagination information. `next_url` is the URL for requesting the next page of results. The `next_url` property is null if there are no more results, and retains the same `limit` parameter that is used for the initial request.

## Rate limiting

Rate limits for API requests are enforced on a per-caller basis. If the number of requests for a particular method and endpoint reaches the request limit within the specified time window, no further requests are accepted until the timer expires. After the timer expires, a new time window begins with the next accepted request.

The response to each HTTP request includes headers you can use to determine whether you are close to the rate limit:

   * X-RateLimit-Reset: the time the current timer expires (in UNIX epoch time)
   * X-RateLimit-Remaining: the number of requests remaining in the current time window
   * X-RateLimit-Limit: the total number of requests allowed within the time window

An HTTP status code of 429 indicates that the rate limit has been exceeded.

The number of allowed requests, and the length of the time window, vary by method and endpoint. The reference information for each endpoint specifies the rate limit that applies.


## Related APIs

When working with the resource controller endpoints, it may be helpful to be aware of the IBM Cloud Open Source Broker APIs used to create your service broker.

* [IBM Cloud OSB](/apidocs/ibm-cloud-osb-api)
