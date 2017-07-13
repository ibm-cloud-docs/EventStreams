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

# How to use the {{site.data.keyword.mql}} API in {{site.data.keyword.messagehub}}
{: #mql_how}


To use the API, add a reference to the latest available {{site.data.keyword.mql}} client API for your chosen language as follows:

<dl><dt>For Java</dt>
<dd>Add the following reference to your ```Maven pom``` file:
<pre>
<code>&lt;dependency&gt;
    &lt;groupId&gt;com.ibm.mqlight&lt;/groupId&gt;
    &lt;artifactId&gt;mqlight-api&lt;/artifactId&gt;
    &lt;version&gt;LATEST&lt;/version&gt;
&lt;/dependency&gt;
</code></pre>
{:pre}

</dd>
<dt>For Node.js</dt>
<dd>Add the following reference to the dependency section of your ```package.json```
file:<pre><code>"mqlight" : "1.0.x"</code></pre>

And add the following require statement to your source
file:<pre><code>var mqlight = require(‘mqlight’);</code></pre>
</dd>
<dt>For Ruby</dt>
<dd>Add the following reference to the
```Gemfile```:<pre><code>gem 'mqlight', '~> 1.0'</code></pre>
{:pre}

And add the following require statement to your source
file:<pre><code>require ‘mqlight’</code></pre>
</dd>
<dt>For Python</dt>
<dd>Add the following reference to your ```requirements.txt```
file:<pre><code>git+git://github.com/mqlight/python-mqlight.git@readthedocs</code></pre>
{:pre}


And the add following import statement to your source
file:<pre><code>import mqlight</code></pre>
{:pre}

</dd>
</dl>
