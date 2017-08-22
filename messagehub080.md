---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# How to connect existing MQ Light applications
{: #mql_exist_apps}

You can connect existing applications that currently run against either {{site.data.keyword.IBM_notm}} MQ or the {{site.data.keyword.mql}}
{{site.data.keyword.Bluemix_notm}} service to the service. The apps continue to work in the same way.
{:shortdesc}

To connect existing apps, complete the following checks:

* Ensure that the app is using the latest available {{site.data.keyword.mql}} API client version for your language.
* Check that the connection details extracted from VCAP_SERVICES reference the <code>messagehub</code> service type and retrieve the connections user name from the <code>credentials.user</code> property rather than the <code>credentials.username</code> property, and retrieve the connection lookup URL from the <code>credentials.mqlight_lookup_url</code> property rather than the <code>credentials.connectionLookupURI</code> property. For more information, see [VCAP_SERVICES environment variable](/docs/services/MessageHub/messagehub071.html).

	Note that this step is done for you if you use the Java&trade; client and specify 'null' as the endpointService parameter in the create() call, so that the client retrieves the information itself.
	
* Your app must support TLS v1.2 connections. VCAP_SERVICES no longer contains a <code>credentials.nonTLSConnectionLookupURI</code> property for creating a non-TLS connection.

You should also note the following information:

* Message limits are consistent with {{site.data.keyword.messagehub}} but might be different from other servers supporting the {{site.data.keyword.mql}} API. For more information, see [Maximum limits](/docs/services/MessageHub/messagehub083.html).
* JMS is not supported.
* You can have only one {{site.data.keyword.messagehub}} instance for each {{site.data.keyword.Bluemix_notm}} space.
