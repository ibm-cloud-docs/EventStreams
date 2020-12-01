---

copyright:
  years: 2020
lastupdated: "2020-12-01"

keywords: IBM Cloud, observability, api methods, iam, activity tracker, actions

subcollection: Activity-Tracker-with-LogDNA

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}
{:important: .important}
{:note: .note}
{:term: .term}
{:deprecated: .deprecated}
{:external: target="_blank" .external}

# IAM and Activity Tracker action by API method
{: #event_at_iam}

When you use {{site.data.keyword.at_full}} through the command line or console, the service calls application programming interface (API) methods to complete your requests. You might need certain permissions to call these API methods, and you can track the requests that you make with an {{site.data.keyword.at_full_notm}} instance.
{: shortdesc}

Review the following list of {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) actions and {{site.data.keyword.at_full_notm}} events that correspond to each API method in {{site.data.keyword.at_full_notm}}.

For more information, see the following topic: [{{site.data.keyword.messagehub}} API Docs](https://cloud.ibm.com/apidocs/event-streams){: external}



## Administration REST APIs
{: #event_admin_rest}

Review the following administration API methods, their required actions in {{site.data.keyword.cloud_notm}} IAM, and the event streams that are sent to {{site.data.keyword.at_full_notm}}.

| Action                                    | Methods                 | IAM Action    |  AT Action |
|-------------------------------------------|------------------------|---------------|------------|
| Create a topic | `POST $Kakfa-http-url/admin/topics` | `messagehub.cluster.read messagehub.topic.manage` | `event-streams.topic.create` |
| List topics	| `GET $Kakfa-http-url/admin/topics` | `messagehub.cluster.read` | None |
| Get detailed information on a topic | `GET $Kakfa-http-url/admin/topics/{topic_name}` | `messagehub.cluster.read` | None |
| Delete a topic | `DELETE $Kakfa-http-url/admin/topics/{topic_name}` | `messagehub.cluster.read messagehub.topic.manage` | `event-streams.topic.delete` |
| Update a topic | `PATCH $Kakfa-http-url/admin/topics/{topic_name}` | `messagehub.cluster.read messagehub.topic.manage` | `event-streams.topic.update` |
| Get the current topic selection for mirroring	| `GET $Kakfa-http-url/admin/mirroring/topic-selection` | `messagehub.cluster.manage` | None |
| Replace the topic selection for mirroring	| `POST $Kakfa-http-url/admin/mirroring/topic-selection` | `messagehub.cluster.manage` | None |
| Get the topics that are being actively mirrored | `GET $Kakfa-http-url/admin/mirroring/active-topics` | `messagehub.cluster.manage` | None |
| Create a schema | `POST $Kakfa-http-url/artifacts/` | `messagehub.cluster.read messagehub.schema.write` | `event-streams.schema.create` |
| List the schemas in the schema registry | `GET $Kakfa-http-url/artifacts`	| `messagehub.cluster.read`	| None |
| Delete a schema from the schema registry | `DELETE $Kakfa-http-url/artifacts/{schema-id}` | `messagehub.cluster.read  messagehub.schema.manage` | `event-streams.schema.delete` |
| Create a schema version | `POST $Kakfa-http-url/artifacts/{schema-id}/versions` |` messagehub.cluster.read messagehub.schema.write` | `event-streams.schema.create` |
| Get the latest schema version	| `GET $Kakfa-http-url/artifacts/{schema-id} ` | `messagehub.cluster.read messagehub.schema.read` | None |
| Get a specific schema version	| `GET $Kakfa-http-url/artifacts/{schema-id}/versions/{version}` | `messagehub.cluster.read messagehub.schema.read`	| None |
| List all schema versions | `GET $Kakfa-http-url/artifacts/{schema-id}/versions` | `messagehub.cluster.read  messagehub.schema.read` | None |
| Delete a schema version	| `DELETE $Kakfa-http-url/artifacts/{schema-id}/versions/{version}` | `messagehub.cluster.read. messagehub.schema.manage` | `event-streams.schema.delete` |
| Update a global rule | `PUT $Kakfa-http-url/rules/{rule-type}` | `messagehub.cluster.manage` | `event-streams.schema-rule.update` |
| Get the current value of rule	| `GET $Kakfa-http-url/rules/{rule-type}`	| `messagehub.cluster.read`	| None |
| Create a per-schema rule	| `POST $Kakfa-http-url/artifacts/{schema-id}/rules` | `messagehub.cluster.read  messagehub.schema.manage`	| `event-streams.schema-rule.create` |
| Get a per-schema rule	| `GET $Kakfa-http-url/artifacts/{schema-id}/rules/{rule-type}` | `messagehub.cluster.read  messagehub.schema.read` | None |
| Update a per-schema rule | `PUT $Kakfa-http-url/artifacts/{schema-id}/rules/{rule-type}` | `messagehub.cluster.read  messagehub.schema.manage`	| `event-streams.schema-rule.update` |
| Delete a per-schema rule | `DELETE $Kakfa-http-url/artifacts/{schema-id}/rules/{rule-type}` | `messagehub.cluster.read  messagehub.schema.manage` | `event-streams.schema-rule.delete` |
{: caption="Table 1. Administration" caption-side="top"}

## Producer REST APIs
{: #event_producer_rest}

Review the following producer API methods, their required actions in {{site.data.keyword.cloud_notm}} IAM, and the events that are sent to {{site.data.keyword.at_full_notm}}.

| Action                                    | Method                 | IAM ACTION    |  AT ACTION |
|-------------------------------------------|------------------------|---------------|------------|
| Produce a message | `POST /topics/{topic_name}/records` | `messagehub.cluster.read messagehub.topic.write` | 	None |
{: caption="Table 2. Producer" caption-side="top"}

