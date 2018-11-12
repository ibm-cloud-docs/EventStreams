---

copyright:
  years: 2015, 2018
lastupdated: "2018-05-25"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Using the MQ Light clients
{: #mql_clients}

** The MQ Light API is available as part of the Standard plan only.**
<br/>

## Using the MQ Light Java client
{: #mql_java}

To use the API, add a reference to the latest available {{site.data.keyword.mql}} client API for Java as follows:

Add the following reference to your <code>Maven pom</code> file:

```
<dependency>
    <groupId>com.ibm.mqlight</groupId>
    <artifactId>mqlight-api</artifactId>
    <version>LATEST</version>
</dependency>
```
{:codeblock}

<!-- Comment from Andrew
Instructions for getting started, with links for more info
Simple send source and receive source in-line

-->

<!-- 12/11/18: info was in eventstreams102.md, moved because of doc app changes -->

## Using the MQ Light Node.js client 
{: #mql_node}


To use the API, add a reference to the latest available {{site.data.keyword.mql}} client API for Node.js as follows:

Add the following reference to the dependency section of your <code>package.json</code> file:

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



