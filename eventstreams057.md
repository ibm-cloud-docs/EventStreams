---

copyright:
  years: 2015, 2021
lastupdated: "2021-02-15"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: EventStreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}


# Known restrictions
{: #restrictions}

If you find a problem while using {{site.data.keyword.messagehub}}, review these known restrictions and workarounds. 
{: shortdesc}

## Java Kafka calls don’t failover if a Kafka bootstrap server fails
{: #calls_failover}

### Problem
{: #calls_failover_problem notoc}

The Java Virtual Machine (JVM) caches DNS lookups. When the JVM resolves an IP address for a host name, it caches the IP address for a specified period of time, known as the time to live (TTL). Some Java configurations set the JVM TTL so that it never refreshes a host name’s IP address until the JVM is restarted. An example configuration is one that has a security manager.

### Workaround
{: #calls_failover_workaround notoc}

Because {{site.data.keyword.messagehub}} uses Kafka bootstrap server URLs with multiple IP addresses for high availability, not all the broker IP addresses are known to the Kafka client, which prevents failover to a working broker. In these cases, failover requires a re-query of the IP addresses for the broker URLs to get a working IP address. You are recommended to configure your JVM with a TTL value of 30 to 60 seconds. This value ensures that if a bootstrap server’s IP address has issues, the Kafka client will be able to look up and use a new IP address by querying the DNS.

From the <code>java.security</code> file: 

```
# The Java-level namelookup cache policy for successful lookups:
#
# any negative value: caching forever
# any positive value: the number of seconds to cache an address for
# zero: do not cache
#
# default value is forever (FOREVER). For security reasons, this
# caching is made forever when a security manager is set. When a security
# manager is not set, the default behavior in this implementation
# is to cache for 30 seconds.
#
# NOTE: setting this to anything other than the default value can have
#       serious security implications. Do not set it unless
#       you are sure you are not exposed to DNS spoofing attack.
#
#networkaddress.cache.ttl=-1
```

### How to modify the JVM's TTL
{: #jvm_ttl notoc}

* To modify the JVM's TTL for all applications, set the <code>networkaddress.cache.ttl</code> value in the <code><var class="keyword varname">$JAVA_HOME</var>/jre/lib/security/java.security</code> file.
* To modify the JVM TTL for a given application, set the <code>networkaddress.cache.ttl</code> in your application code as follows:
```
java.security.Security.setProperty("networkaddress.cache.ttl" , "30");
```

## Java Kafka calls might time out
{: #calls_timeout_kafka}

### Problem
{: #calls_timeout_problem notoc}

Sometimes a Kafka Java client call fails to find Kafka. The cause of failure is that the Kafka client has determined the same failing IP address for each of the bootstrap servers. The Kafka client tries each broker’s IP address (which is the same failing IP address) and incorrectly determines that Kafka is down. Note that the Kafka client uses the first IP address returned in the list if multiple IP addresses are returned in the DNS query.

### Workaround
{: #calls_timeout_workaround notoc}

Retry your calls after waiting long enough for the JVM DNS cache for the broker URLs to expire. On subsequent Kafka calls, a working broker IP address should be returned from the DNS query and used. 

A Kafka Improvement Proposal (KIP) #302 (available from Kafka 2.1.1) ensures that Kafka clients try all available broker IP addresses and not a subset, so a failure in a single IP address won't cause a failure. 

You need to opt into this functionality by using one of the following methods:
* specify a new allowed value in the Consumer/Producer properties of the configuration parameter <code>client.dns.lookup</code>:

    ```
    client.dns.lookup: "use_all_dns_ips" 
    ```
    {: codeblock}

* use the constants CommonClientConfigs.CLIENT_DNS_LOOKUP_CONFIG: ClientDnsLookup.USE_ALL_DNS_IPS 


## Topics and partitions
{: #topics_partitions}

*  Topic names are restricted to a maximum of 200 characters.
*  The default number of partitions for a topic is one.

<!--following message retention info duplicted in FAQs eventstreams108-->

## Creating and deleting topics in Kafka
{: #create_delete}

In Kafka, topic creation and deletion are asynchronous operations
that might take some time to complete. You are recommended to
avoid usage patterns that rely on the rapid creation and deletion
of topics, or on the rapid deletion and re-creation of topics.

<!--
## Kafka REST API
{: #trouble_rest}

<br/>
**Is this specific to old Standard only? If so I'll move to specific Standard topic.**
{: note}

*  Only the binary-embedded format is supported for requests and
   responses. The Avro and JSON embedded formats are not supported.
*  Concurrent requests are not supported for a consumer instance.
   Read, commit, or delete requests corresponding to a consumer
   instance should be sent only after a response is received for
   any outstanding requests of that instance.

-->
<!--
<br/>
**Is this specific to old Standard only? If so I'll move to specific Standard topic.**
{: note}

## Kafka REST API rate limitation
{: #kafka_rate}

Applications using the Kafka REST API can be subject to rate
limiting for each ApiKey. When this limiting occurs, the API
responds with the following HTTP error:

<code>429 Too Many Requests</code>
{:screen}

If you see this error, wait and submit the request again.

<br/>
**Is this specific to old Standard only? If so I'll move to specific Standard topic.**
{: note}
-->
<!--12/04/18 - Karen: same info duplicated at messagehub108 -->
<!--
## Kafka REST API daily restart
{: #rest_restart}

The Kafka REST API restarts once a day for a short period of
time. During this period, the Kafka REST API might become
unavailable. If this happens, you are recommended to retry your
request. After the REST API has restarted, you will have to
create your Kafka consumer instances again. If this is the case, the
REST API returns the following JSON:

```'{"error_code":40403,"message":"Consumer instance not found."}'
```
{:screen}
-->
<!--
## Kafka high-level consumer API
{: #kafka_consumer}

You cannot use the Apache Kafka 0.8.2 simple or high-level
consumer API with {{site.data.keyword.messagehub}}. Instead, you can use the earliest supported Kafka consumer API, which is 0.10.
-->
