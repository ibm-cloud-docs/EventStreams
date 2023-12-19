---

copyright:
  years: 2023
lastupdated: "2023-12-11"

keywords: troubleshooting, question, problem

subcollection: EventStreams

---

{{site.data.keyword.attribute-definition-list}}

# Troubleshooting {{site.data.keyword.messagehub}}
{: #troubleshooting}

Use the troubleshooting tips to learn how to troubleshoot issues with {{site.data.keyword.messagehub_full}}.

If you experience a problem with {{site.data.keyword.messagehub}}, first check the [{{site.data.keyword.Bluemix_notm}} status page](https://cloud.ibm.com/status){: external}. If you like help from the {{site.data.keyword.messagehub}} team, ensure that you gather all the information that is required as detailed in [Reporting a problem to the {{site.data.keyword.messagehub}} team - Standard and Enterprise plans](/docs/EventStreams?topic=EventStreams-report_problem_enterprise#report_problem_enterprise).
{: shortdesc}

## Timeouts when connecting or producing to a topic
{: #timeouts}

If you have an Apache Kafka application that is unable to connect to a topic or unable to produce to a topic due to a timeout excpetion, check whether the producer has network problems by using the following command: `nc -zv <broker-hostname> 9093` (for example, `nc -zv broker-3-abc.kafka.svc01.us-east.eventstreams.cloud.ibm.com 9093`).

*  [{{site.data.keyword.messagehub}} Java Kafka sample](https://github.com/ibm-messaging/event-streams-samples/tree/master/kafka-java-console-sample){: external}
*  [Apache Kafka documentation](http://kafka.apache.org/documentation.html){: external}
*  [Apache Kafka 2.2.0 client](https://archive.apache.org/dist/kafka/2.2.0/kafka-2.2.0-src.tgz){: external}
*  [Apache Kafka 3.4.1 client](https://www.apache.org/dyn/closer.cgi?path=/kafka/3.4.1/kafka-3.4.1-src.tgz){: external}
*  [{{site.data.keyword.Bluemix_notm}} pricing information](/docs/billing-usage?topic=billing-usage-cost){: external}

During regular updates, it is normal for individual brokers and IP endpoints to go down for a short period of time while updates are applied and the system is restarted. These timeouts are likely a result of a broker that was temporarily offline. In some cases, your apps might have some impact as the cluster reassigns resources. Write your apps to be resilient to these changes and to be able to reconnect and retry operations.

Another possible problem might be that the client is adding records in a queue faster than they can be sent from the client. In this case, consider to increase the `request.timeout.ms` or to decrease `batch.size` of the producer, or both. If the issue needs further investigation, a request to enable TRACE level debug for the Kafka clients will be sent. Producer disconnects might occur due to known bugs with the Kafka client, so refer to the [list of recommended clients](docs/EventStreams?topic=EventStreams-kafka_using).

## HTTP error codes for Kafka and how to fix them
{: #http_error_codes}

| Error code | Error message | How to fix |
| --- | --- | --- |
| 400 | Invalid request JSON. | Correct your request. |
| 403 | Not authorized to perform the operation. | The ID that was used to create the resource key does not have an IAM policy granting the ID to create the resource key, or the API key that is used is missing a certain role. For more information, see [Managing authentication to your Event Streams instances](/docs/EventStreams?topic=EventStreams-security). |
| 404 | Unable to find the topic with the topic name entered by the user. | Check if the schema request is valid, the installation is correct, or if the topic exists in the instance ID. |
| 422 | Semantically invalid request. | If you receive this error when you try to create a new topic, it might be due to the maximum number of allowed partitions for your plan. For more information, see [How Event Streams uses limits and quotas](/docs/EventStreams?topic=EventStreams-security) for verifying the limits. |
| 503 | An error occurred while handling the request. The service is unavailable. | Check if this error is caused by a response timeout from Kafka. If creating a new topic fails, check the limits. |

## Unable to resolve host address
{: #unable_resolve_host}

If the application or CURL command is unable to connect to the {{site.data.keyword.messagehub}} service due to closing connection, it might be caused by DNS issues. Check if there are any network issues with connecting to the broker. Use the `dig` command output to check DNS, for example, `dig kafka-1-mh-xyz.private.ussouth.messagehub.appdomain.cloud`. If the lookup of the hostname resolves from a workstation, it might be a transient network issue.
If the UI displays the incorrect hostname, raise a [support ticket](docs-draft/EventStreams?topic=EventStreams-gettinghelp).

## Unable to view topics in the UI
{: #unable_view_topics}

Check the IAM policy for the account, as there might be an issue with the roles assigned to your user. Verify if you can connect to the topic by using the CLI or the REST API. For more information, see [Using the Administration REST API](/docs/EventStreams?topic=EventStreams-admin_api) and [Using Kafka console tools with Event Streams](/docs/EventStreams?topic=EventStreams-kafka_console_tools). If viewing topics does not work when using the CLI, it might be a network issue. Check the network problem with the following command: `nc -zv <broker-hostname> 9093` (for example, `nc -zv broker-3-abc.kafka.svc01.us-east.eventstreams.cloud.ibm.com 9093`).
  
## Unable to create topics
{: #unable_create_topics}

- If you are not able to create topics, it might be because you exceed the maximum number of partitions that are allowed. Check whether the [partition limit is reached](/docs/EventStreams?topic=EventStreams-kafka_quotas#limits_standard). 
- If you receive an insufficient disk space error when you try to create a topic, check how the [disk space is reserved according to topic configuration](/docs/EventStreams?topic=EventStreams-ES_understanding_reserved_disk_usage). If disk space must be added, see [Scaling Enterprise plan capacity](/docs/EventStreams?topic=EventStreams-ES_scaling_capacity).
- If you use a multitenant environment, check the [quota limits](/docs/EventStreams?topic=EventStreams-kafka_quotas).
- If you are on an Enterprise instance and have questions on scaling, see [scaling combinations](/docs/EventStreams?topic=EventStreams-ES_scaling_capacity#ES_scaling_combinations).
- For timeout errors when creating topics, check if any network issues exist or if VPN to be used is for private endpoints.
