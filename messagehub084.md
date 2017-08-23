---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# How to migrate the Kafka client from 0.9.x to 0.10.x
{: #kafka_migrate}


If you're using the Java clients, you can now use
the publicly available 0.10.x Kafka clients. You are strongly encouraged to move from 0.9.x to the
latest 0.10.x version (currently 0.10.2.1). Complete the following steps:

<ol>
<li>Delete the {{site.data.keyword.messagehub}} login jar module.</li>
<li>Change your file to the following:

<pre class="pre">
    KafkaClient {
      org.apache.kafka.common.security.plain.PlainLoginModule required
      serviceName="kafka"
        username="&lt;your username&gt;"
        password="&lt;your password&gt;";
    };
</pre>
{: codeblock}
</li>

<li>Add this line to your consumer and producer properties: <code>sasl.mechanism=PLAIN</code></li>
</ol>

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">The name of the user in {{site.data.keyword.Bluemix_notm}}.</dd>
<dt class="pt dlterm">&lt;permission&gt;</dt>
<dd class="pd">Set the permissions for the user: Admin (available alternative is Superuser), Login (available alternative is Basic), Catalog (read or write access), Reports (read or write access), or Users (read or write access).</dd>
<dt class="pt dlterm">&lt;access&gt;</dt>
<dd class="pd">For Catalog, Reports, or Users permissions, you must also set the level of access as <code>read</code> or <code>write</code>.</dd>
</dl>