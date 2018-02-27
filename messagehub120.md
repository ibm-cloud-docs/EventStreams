---

copyright:
  years: 2015, 2018
lastupdated: "2018-02-27"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

<!-- Notes from chat with Charlie 

Different plan for provisioning

Quality of service from each plan

Life of a user through cycle - APIs, feature sets

-->

# Alpha users
{: #alpha_users }

The Alpha program provides early access to the next version of the {{site.data.keyword.messagehub}} service. 

Use the following information to get an app running with the {{site.data.keyword.messagehub}} Alpha:


## 1. Create the Message Hub service
{: alpha_create}

  a. Click the **Message Hub vNext - Production** tile, which is an experimental service in the 
[catalog ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.stage1.bluemix.net/catalog/labs/?search=vnext).

  b. Create a Message Hub service. This service provides a single-tenant cluster under by the ```Premium``` pricing plan and typically takes 1-3 hours to provision.


## 2. Create and connect a test app

If you don't already have an app you can use, create a test app. For example, using the **SDK for Node.js** service. 

a. Navigate to the **SDK for Node.js** tile in the [catalog ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.stage1.bluemix.net/catalog/starters/sdk-for-nodejs).
   
b. Before you enter an app name, ensure that you select a region of US South. Create the app. 

c. When the app is running, click the **Connections** tab on the left.

d. Click **Create connection** button.

e. Select your new Message Hub service from the list of existing compatible services and click the **Connect** button.

f. In the **Connect IAM-Enabled Service** window, accept the defaults and click **Connect**
Ensure your Message Hub service is provisioned so you can connect to it.

g. Click the **Runtime** tab on the left and select the **Environment variables** tab in the center. In the **VCAP_SERVICES** section, locate the ```kafka_admin_url``` and ```apikey``` information, which you will need for the next task.


## 3. Create a Message Hub topic and send messages

You can use CURL commands to create a topic and then produce and consume a message. For each command, replace APIKEY and KAFKA_ADMIN_URL with values from your VCAP_SERVICES environment variable.

a. From the command line, create a Message Hub topic using the following CURL command:
```
curl -i -X POST -H "Content-Type: application/json" -H "X-Auth-Token: ${APIKEY}" --data '{ "name": "newtop:"}' ${KAFKA_ADMIN_URL}/admin/topics
```

b. To produce a message, use the following CURL command:

<pre class="pre"><code>
curl -X POST -H "X-Auth-Token:<var class="keyword varname">APIKEY</var>" -H "Content-Type: application/vnd.kafka.binary.v1+json" <var class="keyword varname">KAFKA_ADMIN_URL</var>/topics/<var class="keyword varname">topic name</var> -d 

'
{
  "records": [
    {
      "value": "<var class="keyword varname">A base 64 encoded value string</var>"
    }
  ]
}
'
</code></pre>
{: codeblock}... 

c. To consume the message, use the following CURL command: 

<pre class="pre"><code>
curl -X GET -H "X-Auth-Token:<var class="keyword varname">APIKEY</var>" -H "Accept: application/vnd.kafka.binary.v1+json" <var class="keyword varname">KAFKA_ADMIN_URL</var>/topics/<var class="keyword varname">topic name</var>/partitions/<var class="keyword varname">partition ID</var>/messages?offset=<var class="keyword varname">offset to start from</var>
</code></pre>
{: codeblock}


## About your Alpha cluster

The maximum cluster size and storage allocation created is ...

The cluster is provisioned with a single Kafka version, a fixed number of nodes, storage, and maximum retention period, which you cannot change.

The Alpha program is available in the US-South region only.



## Single tenant Premium plan for the Alpha
{: premium_plan}

The Premium plan is designed for users who have performance and other functional requirements that go beyond the public service. The Premium plan provides a single-tenant version of the service on a shared network and shared compute.

* For the Alpha, there is no Lite or Standard plan.
	
* You can define the number of partitions and storage (within the maximum storage allocated to the cluster).

* There are no quotas or throttling.

* You can use Kafka clients from 0.10 and later and it supports Kafka Streams and KSQL.

* You can use the Kafka REST admin interface to create, list, and delete topics.


## Security
{: security}

The authentication method used to access Message Hub resources is an IAM service access key and SASL. A TLS certificate is shared across a region and SNI support is required.

You can connect new and existing applications to a single-tenant resource.

## Resource controller management

TBD


## Administering Message Hub

### Administering Message Hub using the dashboard in the IBM Cloud console

* You can create, list, and delete topics.

* You cannot change your configuration or view the current configuration.

* No metrics, logs, or usage information are available.


### Administering Message Hub using the Kafka REST interface

* You can create, list, and delete topics.

* V1 is backwards compatible with the existing Kafka REST admin.

* V2 will allow cluster administration and options in future, but currently allows topics only.

This interface uses TLS 1.2 and there is no authorization at topic level.


## Samples

Samples are specific to the Alpha program. You can find samples for the Alpha: ...

## Compatibility

You can connect new and existing applications to a single-tenant resource. 


## Kafka information

Message Hub in Alpha is based on Kafka 1.0.

* No quotas are enforced

* No multitenancy 

The following Kafka client versions are supported:

* 1.0
* 0.11
* 0.10 

0.9 clients are not supported.


## Migration and coexistence

### Apps that use VCAP services
{: notoc}

If you have an existing app that uses VCAP services, you  must make the following code change to ensure it keeps working ...


## Alpha limitations

The current limitations of this Alpha program are as follows:

- No options: clusters are provisioned with a single Kafka version, with a fixed number of nodes, storage, and a maximum retention period.

- No authorization just authentication, that is, you cannot apply fine-grained authorization on topics.

- No CLI

- No user-controlled scaling

- No configuration personalization

- No Kafka REST 1.0

- No Schema Registry 

- No MQ Light API

- No bridges

- No integration with the {{site.data.keyword.cloudaccesstrailfull_notm}} service (previously known as AccessTrail) 

- No VPC

- No BYOK

- No Kafka Connect






