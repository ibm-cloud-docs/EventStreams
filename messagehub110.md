---

copyright:
  years: 2015, 2017
lastupdated: "2017-09-26"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Using KSQL with Message Hub
{: #ksql_using}


You can use [KSQL ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/confluentinc/ksql){:new_window} with {{site.data.keyword.messagehub}} for stream processing. Complete the following steps:
<ol>
<li>Create a {{site.data.keyword.messagehub}} KSQL configuration file. For example:
</li>
<li>Use the {{site.data.keyword.messagehub}} dashboard in the {{site.data.keyword.Bluemix_notm}} console to create a topic called </code>ksql__commands<code> with a single partition and the default retention period.
</li>
<li>From a Docker terminal, start KSQL using the following command:
<pre>
<code>
    /bin/ksql-cli local --<var class="keyword varname">messagehub-ksql-properties-file</var> ./config/ksqlserver.properties
</code>
</pre>
{:codeblock}
</li>
<li>item 3 item 3
<ol>
<li>item 3a item 3a</li>
<li>item 3b item 3b</li>
<li>item 3c item 3c</li>
</ol>
</li>
</ol>

When you have completed these steps, you can run all queries listed in the [Quick Start guide ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/confluentinc/ksql/tree/0.1.x/docs/quickstart#create-a-stream-and-table){:new_window}








