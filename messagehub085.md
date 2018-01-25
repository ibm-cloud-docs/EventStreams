---

copyright:
  years: 2015, 2018
lastupdated: "2017-12-04"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Differences between Message Hub in {{site.data.keyword.Bluemix_notm}} Public and Dedicated environments
{: #public_dedicated}

{{site.data.keyword.Bluemix}} is an open-standards,
cloud-based platform for building, running, and managing applications. {{site.data.keyword.Bluemix_notm}} provides public and dedicated deployment
models. {{site.data.keyword.messagehub}} is available in both
environments.

## {{site.data.keyword.Bluemix_notm}} Public environment
{: notoc}

{{site.data.keyword.Bluemix_notm}} Public provides an
economical public cloud service where you pay for what you use and share infrastructure with
others.

In {{site.data.keyword.Bluemix_notm}} Public, the cost of
{{site.data.keyword.messagehub}} is determined by two factors: the
number of partitions that you use and the number of messages that you send and receive. There is no
charge for message data while it is retained on the topics, but the data that each partition retains
is capped at 1 GB.

For more information, see [{{site.data.keyword.Bluemix_notm}} Public ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud-computing/bluemix/public){:new_window}.


## {{site.data.keyword.Bluemix_notm}} Dedicated environment
{: notoc}

{{site.data.keyword.Bluemix_notm}} Dedicated provides a more
isolated environment where your infrastructure is not shared and is hosted in a separate SoftLayer
account managed by {{site.data.keyword.IBM_notm}}. This environment is securely connected to {{site.data.keyword.Bluemix_notm}} Public and your own network.

In a dedicated instance of {{site.data.keyword.messagehub}}, you
pay for the service rather than how much you use it. You can have up to 75 partitions across the
whole environment including all organizations and spaces. Each partition is capped at 10 GB to
ensure the cluster doesn't run out of space.

{{site.data.keyword.messagehub}} in Dedicated can only be deployed with {{site.data.keyword.Bluemix_notm}} Dedicated, but a syndicated version of our public service can be made available if you're using other dedicated environments.

The Kibana and Grafana dashboards for monitoring the service are not supported in {{site.data.keyword.Bluemix_notm}} Dedicated.

For more information, see [{{site.data.keyword.Bluemix_notm}} Dedicated ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/cloud-computing/bluemix/dedicated/){:new_window}.


### Kafka quotas in {{site.data.keyword.messagehub}} Dedicated
{: kafka_dedicated_quotas notoc}

{{site.data.keyword.messagehub}} implements Kafka quotas, that is throttling for producers and consumers in Dedicated and Public environments. You are not recommended to remove quotas, although you can request to have them removed for your Dedicated environment.

For more information, see [Kafka quotas in {{site.data.keyword.messagehub}}](/docs/services/MessageHub/messagehub117.html).


