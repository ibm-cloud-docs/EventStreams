---

copyright:
  years: 2023
lastupdated: "2023-01-24"

keywords: IBM Event Streams, Kafka, plan, Enterprise, quotas, kafka quotas, quota implementation, mapping quotas, authorization, activity tracker, client metrics

subcollection: EventStreams

---

{{site.data.keyword.attribute-definition-list}}

# Enabling Apache Kafka quotas
{: #enabling_kafka_quotas}

## Introduction to Apache Kafka quotas
{: intro_kafka_quotas}

It is possible for a consumer to consume extremely fast and thus to monopolize broker resources and cause network saturation. It is also possible for a producer 
to push extremely large amounts of data causing memory pressure and large IO on broker instances. 

Kafka brokers support quotas that enforce rate limits to prevent clients saturating the network or monopolizing broker resources. For more information, see the 
[Apache Kafka documentation](https://kafka.apache.org/documentation/#design_quotas).

Kafka quotas can be configured to limit network bandwidth usage, Kafka measures this throughput in bytes per second. If throughput over a ~30 second window is found to 
exceed a configured quota, Kafka calculates a sufficient delay to bring throughput within the quota limit.

Kafka brokers then send the delay information to clients as part of protocol responses. A cooperative client should wait for this delay before making new requests; 
a uncooperative client may not respect the throttling request, but in such a case, the broker will not read that client's requests until the throttling delay 
has elapsed (which may cause timeouts on the uncooperative client).

Note the following information on quotas:

- Separate quotas may be defined for producers and consumers. 
- By default, client quotas are unlimited.
- Quotas are applied per broker, rather than per cluster.
- A quota is applied to all clients that share a single user identity.
- A quota can be applied to the 'default' user, i.e. will apply to any user for which no user-specific quota has been set.

## Client metrics
{: client_metrics}

The Java client also exposes throttling information with the following per-broker metrics:

- produce-throttle-time-max
- produce-throttle-time-avg
- fetch-throttle-time-max
- fetch-throttle-time-avg

## IBM Event Streams quota implementation
{: es_quota_implementation}

IBM Event Streams Enterprise plan allows the use of the Kafka API to set and describe quotas on on Kafka 3.1.x clusters.

With reference to the [Kafka documentation on quotas](https://kafka.apache.org/documentation/#quotas), only throughput quota types 
(''producer_byte_rate" and "consumer_byte_rate" quota types) applied to the "user" entity (or the "default user") are supported. 

The "client-id" entity and the "request" and "controller-mutation" quota types are not supported as user-settable quotas. In IBM Event Streams an authenticated user identity 
is represented by an IBM Cloud IAM ID. Because Kafka quotas are applied per IAM ID, a single quota can be shared by a group of API keys, if these all belong to the same 
IAM Service ID.

To obtain the IAM ID of an IAM ServiceID, the IBM Cloud CLI can be used :

ibmcloud iam service-id ServiceId-12345678-aaaa-bbbb-cccc-1234567890ab --output json

See the following example output:

```
{

    "active":true,

    "jti":"...",

    "iam_id":"iam-ServiceId-12345678-aaaa-bbbb-cccc-1234567890ab",

    "realmId":"iam",

     ....

}
```

## Mapping quotas onto an IBM Event Streams Enterprise cluster
{: mapping_quotas_enterprise}

The Kafka API quotas are per-broker, however Enterprise plan capacity is described as a per-cluster throughput in 
https://cloud.ibm.com/docs/EventStreams?topic=EventStreams-kafka_quotas#enterprise_throughput

Therefore if you wish to limit a user to say 10MB/s in total, you would apply a quota of 10/n MB/s to each broker (where n is the number of brokers in the cluster).

To find the number of brokers in a cluster, the KafkaAdminClient.describeCluster call may be used.

For more information, see the [Java documentation]
(https://kafka.apache.org/32/javadoc/org/apache/kafka/clients/admin/KafkaAdminClient.html#describeCluster(org.apache.kafka.clients.admin.DescribeClusterOptions).

The number of brokers can also be found using the kafka-configs.sh shell script bundled in the Apache Kafka distribution :

```
$ bin/kafka-configs.sh --command-config command-config.properties --bootstrap-server "kafka-0.blah.cloud:9093" --describe --entity-type brokers
```

## IBM Event Streams authorization
{: es_authorization}

To be authorized to set client quotas, a user must have a Manager role on the "cluster" resource in IAM.

NB - A set of credentials created with the IBM Event Streams UI with  Manager role on the instance will also have Manager role on cluster, so will also be able to create, 
delete and alter topics in addition to setting quotas.

NB - Any authenticated user has an implied Reader role on cluster and is able to describe quotas.

To create a set of credentials able to manage topics, groups and participate in transactions but NOT authrorized to set quotas, then an IAM access policy that has 
Manager role on resource types "topic", "group" and "txnid" and Reader role on "cluster" needs to be associated with the Service ID. 

### Example: Managing quotas with the kafka-config.sh script (Apache client)
{: example_managing_quotas_kafka_script}

1 - download a Kafka distribution (at least 3.1.0, tested with 3.2.0).

2 - create a properties file (named command-config.properties in the following command lines examples), containing the following entries (replacing "myapikey" with the 
actual API key):

```

sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="token" password="myapikey";

security.protocol=SASL_SSL

sasl.mechanism=PLAIN

ssl.protocol=TLSv1.2

ssl.enabled.protocols=TLSv1.2

ssl.endpoint.identification.algorithm=HTTPS

```

For more information, see[](https://cloud.ibm.com/docs/EventStreams?topic=EventStreams-kafka_using#kafka_api_client).

3 - usage examples:

# alter quotas for user

$ bin/kafka-configs.sh --command-config command-config.properties --bootstrap-server "kafka-0.blah.cloud:9093" --alter --add-config 'producer_byte_rate=1024,
consumer_byte_rate=2048' --entity-type users --entity-name iam-ServiceId-12345678-aaaa-bbbb-cccc-1234567890ab

Completed updating config for user iam-ServiceId-12345678-aaaa-bbbb-cccc-1234567890ab.

# describe quotas for user

$ bin/kafka-configs.sh --command-config command-config.properties --bootstrap-server "kafka-0.blah.cloud:9093" --describe --entity-type users --entity-name 
iam-ServiceId-12345678-aaaa-bbbb-cccc-1234567890ab

Quota configs for user-principal 'iam-ServiceId-12345678-aaaa-bbbb-cccc-1234567890ab' are consumer_byte_rate=2048.0, producer_byte_rate=1024.0

# remove quotas for user

$ bin/kafka-configs.sh --command-config command-config.properties --bootstrap-server "kafka-0.blah.cloud:9093" --alter --delete-config 'producer_byte_rate,consumer_byte_rate' 
--entity-type users --entity-name iam-ServiceId-12345678-aaaa-bbbb-cccc-1234567890ab

Completed updating config for user iam-ServiceId-12345678-aaaa-bbbb-cccc-1234567890ab.

# describe all quotas that have been set to any user, including the default user

$ bin/kafka-configs.sh --command-config command-config.properties --bootstrap-server "kafka-0.blah.cloud:9093" --describe --entity-type users

# alter quotas for the default user

$ bin/kafka-configs.sh --command-config command-config.properties --bootstrap-server "kafka-0.blah.cloud:9093" --alter --add-config 'producer_byte_rate=1024,
consumer_byte_rate=2048' --entity-type users --entity-default

Completed updating default config for users in the cluster.

# remove quotas for the default user

$ bin/kafka-configs.sh --command-config command-config.properties --bootstrap-server "kafka-0.blah.cloud:9093" --alter --delete-config 'producer_byte_rate,
consumer_byte_rate' --entity-type users --entity-default

Completed updating default config for users in the cluster.

Example: Alter throughput quota usage through the Java API 

This is a short sample snippet showing how to invoke the KafkaAdminClient.alterclientQuotas method

```
https://kafka.apache.org/32/javadoc/org/apache/kafka/clients/admin/KafkaAdminClient.html#alterClientQuotas(java.util.Collection,org.apache.kafka.clients.admin.AlterClientQuotas
Options)

import java.util.*;

import org.apache.kafka.clients.CommonClientConfigs;

import org.apache.kafka.clients.admin.*;

import org.apache.kafka.common.config.*;

import org.apache.kafka.common.quota.*;

class Snippet {

    public static void main(String[] args) throws Exception {

        // Kafka client configuration properties

        Properties properties = new Properties();

        properties.put(CommonClientConfigs.BOOTSTRAP_SERVERS_CONFIG, "kafka-0....cloud:9093"); // set mybootstrap

        properties.put(CommonClientConfigs.SECURITY_PROTOCOL_CONFIG, "sasl_ssl");

        properties.put(SslConfigs.SSL_ENABLED_PROTOCOLS_CONFIG, "TLSv1.2");

        properties.put(SslConfigs.SSL_PROTOCOL_CONFIG, "TLSv1.2");

        properties.put(SaslConfigs.SASL_MECHANISM, "PLAIN");

        properties.put(SaslConfigs.SASL_JAAS_CONFIG,

                "org.apache.kafka.common.security.plain.PlainLoginModule " +

                        "required username=\"token\" password=\"" +

                        "myapikey" + "\";"); // set myapikey

        AdminClient admin = AdminClient.create(properties);

        String iamID = "iam-ServiceId-12345678-aaaa-bbbb-cccc-1234567890ab"; //set iam id of target user to set quotas to

        // if null is used instead of the iamID string, the following quota alteration will be applied to the default user

        // add quotas 

        ClientQuotaEntity entity = new ClientQuotaEntity(

                Collections.singletonMap(ClientQuotaEntity.USER, iamID));

        ClientQuotaAlteration alteration = new ClientQuotaAlteration(entity,

                Arrays.asList(new ClientQuotaAlteration.Op("consumer_byte_rate", 1000.0),

                        new ClientQuotaAlteration.Op("producer_byte_rate", 1000.0)));

        admin.alterClientQuotas(Arrays.asList(alteration)).all().get();

        // describe quotas

        DescribeClientQuotasResult describeClientQuotasFuture = admin.describeClientQuotas(ClientQuotaFilter.all());

        System.out.println(describeClientQuotasFuture.entities().get());

        //remove quotas (set them to null)

        entity = new ClientQuotaEntity(Collections.singletonMap(ClientQuotaEntity.USER, iamID));

        alteration = new ClientQuotaAlteration(entity,

                Arrays.asList(new ClientQuotaAlteration.Op("consumer_byte_rate", null),

                        new ClientQuotaAlteration.Op("producer_byte_rate", null)));

        admin.alterClientQuotas(Arrays.asList(alteration)).all().get();

    }

}
```

## IBM Cloud Activity Tracker events
{: activity_tracker_events}

Whenever throughput quotas are updated, an Event Streams config event is generated, which can be monitored in IBM Cloud Activity Tracker.

See the following example of an emitted Activity Tracker Event on adding `producer_byte_rate` and `consumer_byte_rate` quotas to IAM id 
"iam-ServiceId-12345678-aaaa-bbbb-cccc-1234567890ab"}]:

```
{"initiator.id":"iam-ServiceId-12345678-aaaa-bbbb-cccc-1234567890ab","initiator.name":"Service credentials-1","initiator.typeURI":"",
"initiator.credential.type":"apikey","target.id":"crn:v1:staging:public:messagehub-vnext-integration:eu-gb:a/123456789abcdefghijklmnopqrs:a123b456-ab12-1234-5678-1234abcd5678::",
"outcome":"success","reason.reasonCode":0,"correlationId":"4","initiator.host.agent":"adminclient-1","responseData":{"errorCode":0,"errorMessage":null,"entities":
[{"type":"user","name":"iam-ServiceId-12345678-aaaa-bbbb-cccc-1234567890ab"}],"ops":[{"key":"producer_byte_rate","value":1000.0,"remove":false},{"key":"consumer_byte_rate",
"value":1000.0,"remove":false}]},"severity":"normal","eventTime":"2022-06-30T14:05:52.993+0000","initiator.host.address":"123.123.123.1","action":"event-streams.config.update"}
```

For more information about Activity Tracker events for Event Streams, see the [Activity tracker documentation]
(https://cloud.ibm.com/docs/EventStreams?topic=EventStreams-at_events).
