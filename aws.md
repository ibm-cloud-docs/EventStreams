---

copyright:
  years: 2015, 2021
lastupdated: "2021-12-14"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka, AWS

subcollection: EventStreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}


# Setting up AWS machines
{: #satellite_aws}

## Prerequisites
{: #prereqs_aws}

1. Go to your Satellite location and under  **Setting up your location**, download the script to set up Satellite machines for your location.
1. Edit the script by placing the following after the first mention of `API_URL`

   ```text
   # Enable AWS RHEL package updates
   yum update -y
   yum-config-manager --enable '*'
   yum repolist all
   yum install container-selinux -y
   echo "repos enabled"
   ```
   {: codeblock}

## Launch templates
{: #launch_templates}

Launch templates are used to specify the machine types and configuration you're intending to use for each respective machine type in your Satellite location.

1. Log into the AWS account you want to use for provision and select the appropriate region for your provision.
1. From the [AWS EC2 dashboard](https://console.aws.amazon.com/ec2/v2/home){: external}, go to **Instances** > **Launch Templates**.
1. Click **Create Launch template** for our Satellite control plane and name it `satellite-location-name-ctrl`.
1. Select image, `ami-030e754805234517e` which is a community image.
1. Select instance type `m5d.xlarge`
1. Select the `default` security group.
1. Change the storage (AMI Root) from 10 GB to `100GB`
1. Add a new storage volume. The device name is `/dev/sdb` and set the size to `100GB`
1. In advance settings, paste the edited satellite location script to the user data section
1. Create the launch template
1. Repeat this for a new template, but call it `satellite-locaiton-name-edge-mgmt`
1. Repeat this for a new template, but call it `satellite-location-name-data` AND set the instance type to `m5d.2xlarge`


## Auto Scaling groups
{: #auto_scaling_groups}

An Auto Scaling group is a scalable group of hosts that are created based on a launch template. By scaling the group to the capacity that you want, you provision the hosts in EC2. The startup script you downloaded from IBM Cloud Satellite will make the machines provision with your Satellite location.

1. Go to the Auto Scaling Groups section of the AWS EC2 dashboard by clicking **Auto Scaling Groups**.
1. Click **Create Auto Scaling group**.
1. Name it `satellite-location-name-ctrl` to pair it with the launch template you created for control planes.
1. Select the launch template `satellite-location-name-ctrl` if you have made edits to the launch template you might need to specify the latest version. Click **Next**.
1. Under Network, select Availability Zones and subnets, select `region-a`, `region-b` and `region-c`, then click next 
1. Click Next
1. Set the `Desired capacity`, `Minimum Capacity` and `Maximum capacity` to `3`, then click next
1. Click Next
1. Click Next
1. Review the settings and click `Create Auto Scaling group`
1. Wait for the machines to appear in your satellite location, this is to ensure we are assigning our control workers to the control auto scaling group
1. Configure the `Control Plane` in your satellite location using the `Setting up your new location` section at the top of the `Getting Started` page of your satellite location in {{site.data.keyword.Bluemix_notm}}.
1. Wait for the `Control Plane` workers to be assigned and start provisioning.
1. Repeat the steps above for creating an auto scaling group for `satellite-location-name-data`.
1. Repeat the steps above for creating an auto scaling group for `satellite-location-name-edge-mgmt` but set the `Desired Capacity`, `Minimum Capacity`, and `Maximum Capacity` and to 6.
1. Wait for all the machines to appear.

You are now ready to provision {{site.data.keyword.messagehub}} for Satellite on AWS

