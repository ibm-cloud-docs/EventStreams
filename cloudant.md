---

copyright:
  years: 2018
lastupdated: "2018-11-07"

keywords: Database-as-a-Service,DBaaS,MapReduce,pre-built client libraries

subcollection: cloudant

content-type: api-docs

title: IBM Cloudant API Reference

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:generic: .ph data-hd-programlang='generic'}
{:java: .ph data-hd-programlang='java'}
{:ruby: .ph data-hd-programlang='ruby'}
{:c#: .ph data-hd-programlang='c#'}
{:objectc: .ph data-hd-programlang='Objective C'}
{:python: .ph data-hd-programlang='python'}
{:node: .ph data-hd-programlang='node'}
{:php: .ph data-hd-programlang='PHP'}
{:swift: .ph data-hd-programlang='swift'}
{:curl: .ph data-hd-programlang='curl'}
{:node: .ph data-hd-programlang='node'}
{:middle: .ph data-hd-position='middle'}
{:right: .ph data-hd-position='right'}


# Introduction

{{site.data.keyword.cloudantfull}} is a document-oriented
database as a service (DBaaS). It stores data as documents in JSON
format. It is built with scalability, high availability, and
durability in mind. It comes with a wide variety of indexing options
that include MapReduce, {{site.data.keyword.cloudant_short_notm}}
Query, full-text indexing, and geospatial indexing. The replication
capabilities make it easy to keep data in sync between database
clusters, desktop PCs, and mobile devices.

We maintain pre-built [client libraries][cl]{:new_window} for customers to use.
Detailed documentation is also available such as a
[Getting started tutorial][gs]{:new_window}, [API documentation, tutorials, and guides][about]{:new_window}.

# Authentication

Access to {{site.data.keyword.cloudant_short_notm}} is controlled using
{{site.data.keyword.cloud}} Identity and Access Management (IAM), which provides
a unified approach to managing user identities, and access control across your
{{site.data.keyword.cloud}} services and applications.

To work with the API, authenticate your application or service by including your
{{site.data.keyword.cloud}} [IAM access token][iamtoken] in API requests.

Further information:

- Our [client libraries][cl]{:new_window}
  provide full integration with IAM's access controls and will automatically
  retrieve an IAM access token when provided an IAM API key.
- View {{site.data.keyword.cloudant_short_notm}} [authentication
  documentation][1]{:new_window}.

[about]: /docs/services/Cloudant?topic=cloudant-about#about
[gs]: /docs/services/Cloudant?topic=cloudant-getting-started-with-cloudant#getting-started-with-cloudant
[1]: /docs/services/Cloudant?topic=cloudant-ibm-cloud-identity-and-access-management-iam-#ibm-cloud-identity-and-access-management-iam-
[cl]: /docs/services/Cloudant?topic=cloudant-client-libraries#client-libraries
[iamtoken]: /docs/iam?topic=iam-iamtoken_from_apikey#iamtoken_from_apikey

# Error handling

{{site.data.keyword.cloudant_short_notm}} works through HTTP. The HTTP status
codes indicate the success or failure of a method by using a combination of the
HTTP status code number and corresponding data in the body of the response. A
`200` response always indicates success. A `400` response indicates a failure,
and a `500` response usually indicates an internal system error.

# Complete IBM Cloudant API Documentation

The documentation here is **partial** and covers a subset of endpoints. View
the [full API documentation][fulldocs]{:new-window}.

[fulldocs]: /docs/services/Cloudant?topic=cloudant-api-reference-overview#api-reference-overview
