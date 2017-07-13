---

copyright:
  years: 2015, 2017
lastupdated: "2016-11-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Using the MQ Light Node.js client 
{: #mql_node}


To use the API, add a reference to the latest available {{site.data.keyword.mql}} client API for Node.js as follows:

Add the following reference to the dependency section of your ```package.json``` file:

<pre class="pre"><code>"mqlight" : "1.0.x"</code></pre>
{: codeblock}

And add the following require statement to your source
file:

<pre class="pre"><code>var mqlight = require(‘mqlight’);</code></pre>
{: codeblock}

<!-- Comment from Andrew
Instructions for getting started, with links for more info
Simple send source and receive source in-line

-->


