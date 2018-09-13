---

copyright:
  years: 2015, 2018
lastupdated: "2018-06-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# {{site.data.keyword.messagehub}} Dedicated environment
{: #dedicated}

{{site.data.keyword.messagehub}} Dedicated provides a more
isolated environment where your infrastructure is not shared and is hosted in a separate account managed by {{site.data.keyword.IBM_notm}}. This environment is securely connected to {{site.data.keyword.Bluemix_notm}} Public and your own network.

In a dedicated instance of {{site.data.keyword.messagehub}}, you
pay for the service rather than how much you use it. You can have up to 75 partitions across the
whole environment including all organizations and spaces. Each partition is capped at 10 GB to
ensure the cluster doesn't run out of space.

{{site.data.keyword.messagehub}} in Dedicated can only be deployed with {{site.data.keyword.Bluemix_notm}} Dedicated, but a syndicated version of our public service can be made available if you're using other dedicated environments.

The Kibana and Grafana dashboards for monitoring the service are not supported in {{site.data.keyword.Bluemix_notm}} Dedicated.


## Kafka quotas in {{site.data.keyword.messagehub}} Dedicated
{: kafka_dedicated_quotas notoc}

{{site.data.keyword.messagehub}} implements Kafka quotas, that is throttling for producers and consumers in Dedicated and Public environments. You are not recommended to remove quotas, although you can request to have them removed for your Dedicated environment.

For more information, see [Kafka quotas in {{site.data.keyword.messagehub}}](/docs/services/MessageHub/messagehub117.html).







