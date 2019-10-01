---

copyright:
  years: 2015, 2019
lastupdated: "2019-10-01"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:deprecated: .deprecated}

# Using the Administration REST API on the Classic plan
{: #admin_api_standard}

The Classic plan is deprecated. From November 1, 2019, you will no longer be able to provision new instances of the Classic Plan. <br/>However, existing instances will continue to be supported.
From June 30, 2020, the Classic Plan will be retired and no longer supported. Any instance of the Classic Plan still provisioned at this date will be deleted. 
{:deprecated}

{{site.data.keyword.messagehub}} provides an Administration RESTful API that you can use to create, delete, and list topics.
{: shortdesc}

To discover the Administration RESTful API's endpoint, your {{site.data.keyword.Bluemix_short}} application can use the `kafka_admin_url` property in your application's VCAP_SERVICES environment variable.

You can download the full specification for the API from [admin-rest-api.yaml ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/event-streams-docs/blob/master/admin-rest-api-classic-plan-only/admin-rest-api.yaml){:new_window}.
To view the swagger file use Swagger tools, for example [Swagger editor ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://editor.swagger.io/#/){:new_window}.

The [{{site.data.keyword.messagehub}} admin-rest-api ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/event-streams-docs/tree/master/admin-rest-api-classic-plan-only){:new_window} directory also contains a useful set of examples of how you can call the Administration RESTful API.


