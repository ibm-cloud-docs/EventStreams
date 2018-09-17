---

copyright:
  years: 2015, 2018
lastupdated: "2018-09-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}



# Reporting a problem to the {{site.data.keyword.messagehub}} team - Standard plan
{: #report_problem}

If you're experiencing a problem with {{site.data.keyword.messagehub}}, first check the [{{site.data.keyword.Bluemix_notm}} status page ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/status){:new_window}. 

If you'd like help from the {{site.data.keyword.messagehub}} team, please gather all the following information. The more information that you can provide upfront, the more efficiently the team can help with the problem:
{:shortdesc}

1. Which {{site.data.keyword.Bluemix_notm}} region is your instance of {{site.data.keyword.messagehub}} provisioned in?  For example, US South or United Kingdom. 
2. Which interface are you seeing issues with? Kafka, REST, AMQP, or bridges?
3. When did the problem first occur (specifically time, date, and timezone)? How long was your app running before this?
4. Is the problem still occurring? Can you replicate it?
5. What is the Instance ID of the {{site.data.keyword.messagehub}} service you are using? 
You can find this ID by looking at the "instance_id" field in the service's VCAP_SERVICES JSON. For example:
 ```
 "instance_id": "e662a61b-d1ff-4cce-aab9-5eae9adb9827"
 ```
6. Which Kafka or REST client is your application using? What are the version details?
7. What are your client configuration details?
8. Do you have application log snippets that display the problem?
9. What is the issue you are seeing? Which topics, client IDs, and group IDs are affected?
10. What impact is the problem having on your service?


You can provide the information you've gathered to IBM in a support ticket by [submitting a support request ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/get-support/howtogetsupport.html#open-case).







