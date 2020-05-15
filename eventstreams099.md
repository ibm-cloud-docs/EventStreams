---

copyright:
  years: 2015, 2019
lastupdated: "2019-11-01"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: EventStreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:deprecated: .deprecated}

# Using the MQ Light clients on the Classic plan
{: #mql_clients}

The {{site.data.keyword.mql}} API is available as part of the Classic plan only. The Classic plan is deprecated. From November 1, 2019, you can no longer provision new instances of the Classic Plan. <br/>However, existing instances will continue to be supported.
From June 30, 2020, the Classic Plan will be retired and no longer supported. Any instance of the Classic Plan still provisioned at this date will be deleted. 
{:deprecated}

## Using the MQ Light Java client
{: #mql_java}

To use the API, add a reference to the latest available {{site.data.keyword.mql}} client API for Java as follows:
{: shortdesc}

Add the following reference to your <code>Maven pom</code> file:

```
<dependency>
    <groupId>com.ibm.mqlight</groupId>
    <artifactId>mqlight-api</artifactId>
    <version>LATEST</version>
</dependency>
```
{:codeblock}


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

<!-- 14/11/18: info was in eventstreams103.md, moved because of doc app changes -->

## Using the MQ Light Ruby client
{: #mql_ruby}


To use the API, add a reference to the latest available {{site.data.keyword.mql}} client API for Ruby as follows:

Add the following reference to the <code>Gemfile</code>:

```
gem 'mqlight', '~> 1.0'
```
{: codeblock}

And add the following require statement to your source file:

```
require ‘mqlight’
```
{: codeblock}

<!-- 14/11/18: info was in eventstreams101.md, moved because of doc app changes -->

## Using the MQ Light Python client
{: #mql_python}

To use the API, add a reference to the latest available {{site.data.keyword.mql}} client API for Python as follows:

Add the following reference to your <code>requirements.txt</code>
file:

```
git+git://github.com/mqlight/python-mqlight.git@readthedocs
```
{:codeblock}

<br>
And add the following import statement to your source file:

```
import mqlight
```
{:codeblock}
<!-- Comment from Andrew
Instructions for getting started, with links for more info
Simple send source and receive source in-line

-->



