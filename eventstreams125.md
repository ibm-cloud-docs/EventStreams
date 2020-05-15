---

copyright:
  years: 2015, 2019
lastupdated: "2019-04-04"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: EventStreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}

# Reporting a problem to the {{site.data.keyword.messagehub}} team - Standard and Enterprise plans
{: #report_problem_enterprise}


If you're experiencing a problem with {{site.data.keyword.messagehub}}, first check the [{{site.data.keyword.Bluemix_notm}} status page ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/status?selected=status){:new_window}.
{: shortdesc}

If you'd like help from the {{site.data.keyword.messagehub}} team, please gather all the following information. The more information that you can provide upfront, the more efficiently the team can help with the problem:
{:shortdesc}

1. What is the CRN ID of the {{site.data.keyword.messagehub}} service you are
   using?  You can provide this ID by pasting the full
   {{site.data.keyword.Bluemix_notm}} console URL after clicking on the
   service, or by pasting the output from the following CLI command:<br/>
   <pre class="pre">
   ibmcloud resource service-instance NAME
   </pre>
	{: codeblock}
2. When did the problem first occur (specifically time, date, and timezone)?
   How long was your app running before this?
3. Is the problem still occurring? Can you replicate it?
4. Which Kafka client is your application using? What are the version details?
5. What are your client configuration details? We need to know your producer and consumer settings, so please list any non-default options you have passed to your producer or consumer creation.
6. Do you have application log snippets that display the problem?
7. What is the issue you are seeing? Which topics, client IDs, group IDs, and
   transaction IDs are affected?
8. What impact is the problem having on your service?

You can provide the information you've gathered to IBM in a support ticket by [submitting a support request ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/get-support?topic=get-support-getting-customer-support#using-avatar){:new_window}.







