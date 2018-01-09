---

copyright:
  years: 2015, 2018
lastupdated: "2018-01-09"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Cloud Object Storage bridge 
{: #cloud_object_storage_bridge }

The {{site.data.keyword.IBM}} Cloud Object Storage bridge provides a way of reading data from a {{site.data.keyword.messagehub}} Kafka topic
and placing the data into [{{site.data.keyword.IBM_notm}} Cloud Object Storage ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/services/cloud-object-storage/about-cos.html){:new_window}.

The Cloud Object Storage bridge allows you
to archive data from the Kafka topics in {{site.data.keyword.messagehub}} to an instance of the [Cloud Object Storage service ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/services/cloud-object-storage/index.html){:new_window}. The bridge consumes
batches of messages from Kafka and uploads the message data as objects to a bucket in the
Cloud Object Storage service. By configuring
the Cloud Object Storage bridge, you can
control how the data is uploaded as objects to Cloud Object Storage. For example, the properties that
you can configure are as follows:

* The bucket name that the objects are written into.
* How frequently objects are uploaded to the Cloud Object Storage service.
* How much data is written to each object before it is uploaded to the Cloud Object Storage service.

The output format of the bridge is an object storage service object that contains one or more
records concatenated with newline characters as separators.

## How data is transferred using the Cloud Object Storage bridge
{: #data_transfer notoc}

The Cloud Object Storage bridge works by
reading a number of Kafka records from a topic and writing the data from these records into an
object. This object is uploaded to an instance of the Cloud Object Storage service. Each Cloud Object Storage bridge reads message data from a
single Kafka topic, although it is possible for one topic to have multiple bridges reading data from
it. A new instance of the Cloud Object Storage
bridge always starts reading from the earliest offset present in the Kafka topic. The Cloud Object Storage bridge uses Kafka's consumer offset
management to transfer data reliably from Kafka without loss, but with a small chance of
duplication.

You can control how many records are read from Kafka before data is written into the Cloud Object Storage service instance using the
following properties. Specify these properties when you create or update a bridge:
<dl><dt>Upload Duration Threshold (seconds)</dt> 
<dd>Defines a period of time in seconds after which the data accumulated from Kafka is uploaded to
the Cloud Object Storage service.</dd>
<dt>Upload Size Threshold (kB)</dt>
<dd>Controls the amount of data in kilobytes that is accumulated from Kafka before the data is
uploaded to the Cloud Object Storage
service.</dd>
</dl>

The trigger for the Cloud Object Storage
bridge to upload data read from Kafka into the Cloud Object Storage service is when either of these
values is first reached. The Cloud Object Storage bridge does not guarantee to transfer data into the Cloud Object Storage service at exactly the point one of
these thresholds is reached. Therefore, the data transferred can arrive later or be larger than the
values specified by these properties.

The Cloud Object Storage bridge concatenates
messages using newline characters as separators as it writes the data into Cloud Object Storage. These separators make the bridge
unsuitable for messages that contain embedded newline characters and for binary message data.


## Getting credentials to use with the Cloud Object Storage bridge
{: notoc}

You must supply credentials to allow the Cloud Object Storage bridge to connect into your Cloud Object Storage instance. Request that the owner or administrator of your Cloud Object Storage instance creates
the credentials using the Cloud Object Storage UI as follows: 

1. Select **Service credentials** then add a **New credential**. 
2. For the **New credential**, select an **Access Role** of **Writer** and a **Service ID** of **Auto Generate**.
   
   You can copy the resulting JSON from this new credential into the {{site.data.keyword.messagehub}} dashboard in the {{site.data.keyword.Bluemix_notm}} console when you create a bridge. 
   
   Alternatively, you can take the ```apikey``` and ```resource_instance_id``` fields and input them into the {{site.data.keyword.messagehub}} dashboard or set them in the create bridge JSON if you are creating the bridge directly using a REST call.

The credential that you create grants writer access to the entire Cloud Object Storage instance,
therefore you might want to restrict this access to the specific bucket that the bridge will interact with.
1. Go to the [Identity & Access Management page ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/iam/?env_id=ibm%3Ayp%3Aus-south#/serviceids){:new_window}.
2. You should see the auto generated service ID on this page. When you have identified the specific ID, select
the **Manage service ID** action. 
3. Select the **Edit policy** action to further restrict it to a specific **Resource type**, which is bucket and a **Resource ID**, which
is the name of the bucket. Click **Save**.


## Creating a Cloud Object Storage bridge
{: notoc}

To create a new Cloud Object Storage bridge using the Kafka REST API, use JSON like the following example. Ensure that your bucket names are globally unique, not just unique within your Cloud Object Storage instance.

<pre class="pre"><code>
{
  "name": "cosbridge",
  "topic": "kafka-java-console-sample-topic",
  "type": "objectStorageS3Out",
  "configuration" : {
    "credentials" : {
      "endpoint" : "https://s3-api.us-geo.objectstorage.softlayer.net",
      "resourceInstanceId" : "crn::",
      "apiKey" : "your_api_key"
    },
    "bucket" : "cosbridge0",
    "uploadDurationThresholdSeconds" : 600,
    "uploadSizeThresholdKB" : 1024,
    "partitioning" : [ {
        "type" : "kafkaOffset"
      }
    ]
  }
}
</code></pre>
{: codeblock}


## How the Cloud Object Storage bridge partitions data into objects
{: notoc}

One of the features of the Cloud Object Storage bridge is its ability to partition
Kafka messages and store them as objects named with a common prefix. A group of objects named with a
common prefix is called a partition. Cloud Object Storage bridge partitioning is a different
concept from Kafka partitioning.

Each time the Cloud Object Storage bridge
has a batch of data to upload to the Cloud Object Storage service, it creates one or more
objects containing the data. The decision about how to partition messages and name the resulting
objects depends on how the bridge is configured. Object names can contain Kafka metadata and
possibly data from the messages themselves. Currently, the bridge supports the following two ways to
partition Kafka messages into Cloud Object Storage objects:

* By Kafka message offset.
* By an ISO 8601 date present in each Kafka message. This requires the Kafka messages to comprise a valid JSON format object.

## Partitioning by Kafka message offset
{: notoc}

To partition data by Kafka message offset, complete the following steps:

1. Configure a bridge without the `"inputFormat"` property.
2. Specify an object with a `"type"` property of the value `"kafkaOffset"` in the `"partitioning"` array. 

    For example:
    <pre class="pre"><code>
        ```
        {
          "topic": "topic1",
          "type": "objectStorageOut",
          "name": "bridge1",
          "configuration" : {
            "credentials" : { ... },
            "bucket" : "bucket1",
            "uploadDurationThresholdSeconds" : "1000",
            "uploadSizeThresholdKB" : "1000",
            "partitioning" : [ {
                "type" : "kafkaOffset"
              }
            ]
          }
        }
        ```
     	</code></pre>
    {:codeblock}

    The object names generated by a bridge configured in this way contain the prefix
    `"offset=<kafka_offset>"` where `"<kafka_offset>"` corresponds
    to the first Kafka message stored in that partition (the group of objects with this prefix). For
    example, if a bridge generates objects with names like the following example,
    `<object_a>` and `<object_b>` contain messages with offsets in
    the range 0 - 999, `<object_c>` contains messages with offsets in the range 1000 -
    1999, and so on.

    <pre class="pre"><code>
        ```
        &lt;bucket_name&gt;/offset=0/&lt;object_a&gt;
        &lt;bucket_name&gt;/offset=0/&lt;object_b&gt;
        &lt;bucket_name&gt;/offset=1000/&lt;object_c&gt;
        &lt;bucket_name&gt;/offset=2000/&lt;object_d&gt;
        ```       
    </code></pre>
    {:codeblock}
  
    
## Partitioning by ISO 8601 date
{: #partition_iso notoc}

To partition data by the ISO 8601 date, complete the following steps:

1. Configure a bridge with the `"inputFormat"` property set to `"json"`. You cannot use an `"inputFormat"` property other than
`"json"`.
2. Specify an object with a `"type"` property of the value `"dateIso8601"` and a `"propertyName"` property in the `"partitioning"` array. 

	For example:
    <pre class="pre"><code>
    ```
    {
      "topic": "topic2",
      "type": "objectStorageOut",
      "name": "bridge2",
      "configuration" : {
        "credentials" : { ... },
        "bucket" : "bucket2",
        "inputFormat" : "json",
        "uploadDurationThresholdSeconds" : "1000",
        "uploadSizeThresholdKB" : "1000",
        "partitioning": [
          {
            "type": "dateIso8601",
            "propertyName": "timestamp"
          }
        ]
      }
    }
    ```
    </code></pre>
    {:codeblock}

	Partitioning by the ISO 8601 date requires that Kafka messages have a valid JSON format. The value of
	`"propertyName"` in the JSON used to configure the bridge must correspond to the ISO
	8601 date field in each Kafka message. In this example, the `"timestamp"` field must
	contain a valid ISO 8601 date value. Messages are then partitioned according to their dates.
	
	A bridge configured like this example generates objects with names specified as follows:
	`<object_a>` contains JSON messages with `"timestamp"` fields with
	a date of 2016-12-07, and both `<object_b>` and `<object_c>` contain JSON messages with `"timestamp"` fields with a date of
	2016-12-08.

    <pre class="pre"><code>
        ```
        &lt;bucket_name&gt;/dt=2016-12-07/&lt;object_a&gt;
        &lt;bucket_name&gt;/dt=2016-12-08/&lt;object_b&gt;
        &lt;bucket_name&gt;/dt=2016-12-08/&lt;object_c&gt;
        ```       
    </code></pre>
    {:codeblock}

	Any message data that is valid JSON but without a valid date field or value is written into an object
	with the prefix `"dt=1970-01-01"`.

## Cloud Object Storage bridge metrics
{: notoc}

The Cloud Object Storage bridge reports
metrics, which can be displayed on your dashboard using Grafana. Metrics of interest include the following:
<dl>
<dt><code>*.<var class="keyword varname">topicName</var>.<var class="keyword varname">bridgeName</var>.bytes-consumed-rate</code></dt>
<dd>Measures the rate that the bridge consumes data (in bytes per second).</dd>
<dt><code>*.<var class="keyword varname">topicName</var>.<var class="keyword varname">bridgeName</var>.records-lag-max</code></dt>
<dd>Measures the maximum lag in the number of records consumed by the bridge for any partition in
this topic. An increasing value over time indicates that the bridge is not keeping up with producers
for the topic.</dd>
</dl>
