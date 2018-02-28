---

copyright:
  years: 2015, 2018
lastupdated: "2018-02-28"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

<!-- Notes from chat with Charlie 

Different plan for provisioning

Quality of service from each plan

Life of a user through cycle - APIs, feature sets

-->

# Getting started with the Alpha program
{: #alpha_program}

The Alpha program provides early access to the next version of the {{site.data.keyword.messagehub}} service. 

Use the following information to get an app running with the {{site.data.keyword.messagehub}} Alpha:


## Create the Message Hub service
{: alpha_create}

<ol type="a">
  <li>Click the **Message Hub vNext - Production** tile, which is an experimental service in the 
[catalog ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.stage1.bluemix.net/catalog/labs/?search=vnext).</li>

  <li>Create a Message Hub service. This service provides a single-tenant cluster under by the ```Premium``` pricing plan and typically takes 1-3 hours to provision.</li>
</ol>  


## Create and connect a test app

If you don't already have an app you can use, create a test app. For example, using the **SDK for Node.js** service. 

<ol type="a">
<li>Navigate to the **SDK for Node.js** tile in the [catalog ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.stage1.bluemix.net/catalog/starters/sdk-for-nodejs).</li>
   
<li>Before you enter an app name, ensure that you select a region of US South. Create the app.</li>

<li>When the app is running, click the **Connections** tab on the left.</li>

<li>Click **Create connection** button.</li>

<li>Select your new {{site.data.keyword.messagehub}} service from the list of existing compatible services and click the **Connect** button.</li>

<li>In the **Connect IAM-Enabled Service** window, accept the defaults and click **Connect**
Ensure your {{site.data.keyword.messagehub}} service is provisioned so you can connect to it.</li>

<li>Click the **Runtime** tab on the left and select the **Environment variables** tab in the center. In the **VCAP_SERVICES** section, locate the ```kafka_admin_url``` and ```apikey``` information, which you will need for the next task.</li>
</ol>


## Create a Message Hub topic and send messages

You can use CURL commands to create a topic and then produce and consume a message. For each command, replace APIKEY and KAFKA_ADMIN_URL with values from your VCAP_SERVICES environment variable.

<ol type="a">
<li>From the command line, create a {{site.data.keyword.messagehub}} topic using the following CURL command:

<pre class="pre"><code>
curl -i -X POST -H "Content-Type: application/json" -H "X-Auth-Token: <var class="keyword varname">APIKEY</var>" --data '{ "name": "newtop:"}' <var class="keyword varname">KAFKA_ADMIN_URL</var>/admin/topics
</code></pre>
{: codeblock}
</li>

<li>To produce a message, use the following CURL command:

<pre class="pre"><code>
curl -X POST -H "X-Auth-Token:<var class="keyword varname">APIKEY</var>" -H "Content-Type: application/vnd.kafka.binary.v1+json" <var class="keyword varname">KAFKA_ADMIN_URL</var>/topics/<var class="keyword varname">topic name</var> -d 

'
{
  "records": [
    {
      "value": "<var class="keyword varname">A base 64 encoded value string</var>"
    }
  ]
}
'
</code></pre>
{: codeblock}
</li>

<li>To consume the message, use the following CURL command: 

<pre class="pre"><code>
curl -X GET -H "X-Auth-Token:<var class="keyword varname">APIKEY</var>" -H "Accept: application/vnd.kafka.binary.v1+json" <var class="keyword varname">KAFKA_ADMIN_URL</var>/topics/<var class="keyword varname">topic name</var>/partitions/<var class="keyword varname">partition ID</var>/messages?offset=<var class="keyword varname">offset to start from</var>
</code></pre>
{: codeblock}
</li>

</ol>






