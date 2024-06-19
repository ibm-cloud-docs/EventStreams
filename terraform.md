---
 
copyright:
  years: 2021
lastupdated: "2021-05-18"

subcollection: your-subcollection

keywords: _doing this task_ in the console, _doing this task_ in the UI, _doing this task_ cli, _doing this task_ command line, _doing this task_ API, _doing this task_ with Terraform

---

{{site.data.keyword.attribute-definition-list}}




# _Task name_
{: #my-task}


You can track resource and support costs from accounts in your {{site.data.keyword.cloud}} enterprise by viewing their usage. The accounts and account groups that you can view usage for depends on your assigned access.
{: shortdesc} 


## _Task name_ in the UI
{: #my-task-ui}
{: ui}



1. Log in to the enterprise account.
1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage > Billing and usage**, and select **Usage**.

   The Usage page displays the costs for all resource usage in the entire enterprise during the current month. Usage is organized according to your enterprise hierarchy, so costs are broken down by the accounts and account groups that are directly under the enterprise. 
   
1. To view usage within an account group, click the account group name in the table or in the **Enterprise level** menu. Similar to the enterprise level, usage is broken down by the account and account group.

   If an account group doesn't contain any accounts, it isn't displayed on the Usage page.

1. _More steps as needed for your task_


## _Task name_ from the CLI
{: #my-task-cli}
{: cli}







To view usage across an entire enterprise, run the [**`ibmcloud billing enterprise-usage`**](/docs/cli?topic=cloud-cli-ibmcloud_billing#ibmcloud_billing_enterprise_usage) command. By default, usage for the current month is displayed. You can view usage for a specific month by specifying the year and month on the `--month` option. For example, the following command displays usage information for April 2020.

```sh
ibmcloud billing enterprise-usage --month 2020-04
```
{: pre}


By default, the command outputs the usage report for the current month in the following format. Most costs are listed as billable costs. Non-billable costs are listed only in rare cases, such as for the month when you add a trial account to the enterprise.

```text
Name             Type            Billable Cost   Non-billable Cost   Currency   Month
Example Corp     account         123.45          0                   USD        2019-07
Development      account_group   234.56          0                   USD        2019-07
Marketing        account_group   345.67          0                   USD        2019-07
Sales            account_group   456.78          0                   USD        2019-07
```
{: screen}

For more information about the command options, see [**`ibmcloud billing enterprise-usage`**](/docs/cli?topic=cloud-cli-ibmcloud_billing#ibmcloud_billing_enterprise_usage).








1. Log in and select the enterprise account.

   ```sh
   ibmcloud login
   ```
   {: pre}

1. If you want to view usage for a specific account group or account, find the name or ID by running the [**`ibmcloud enterprise`**](/docs/cli?topic=cloud-cli-ibmcloud_enterprise) command.

   For example, the following command displays all account groups in an enterprise.

   ```sh
   ibmcloud enterprise account-groups --recursive
   ```
   {: pre}

1. View usage by running the [**`ibmcloud billing enterprise-usage`**](/docs/cli?topic=cloud-cli-ibmcloud_billing#ibmcloud_billing_enterprise_usage) command as shown in the following examples.

   * View usage for the entire enterprise for the current month.

      ```sh
      ibmcloud billing enterprise-usage
      ```
      {: pre}

   * View usage for the `Development` account group for July 2019.

      ```sh
      ibmcloud billing enterprise-usage --account-group Development --month 2019-07
      ```
      {: pre}

   * View the usage for the account groups and accounts that are directly under the enterprise.

      ```sh
      ibmcloud billing enterprise-usage --children
      ```
      {: pre}

   
   By default, the commands output the usage report for the current month in the following format. Most costs are listed as billable costs. Non-billable costs are listed only in rare cases, such as for the month when you add a trial account to the enterprise.

   ```text
   Name             Type            Billable Cost   Non-billable Cost   Currency   Month
   Example Corp     account         123.45          0                   USD        2019-07
   Development      account_group   234.56          0                   USD        2019-07
   Marketing        account_group   345.67          0                   USD        2019-07
   Sales            account_group   456.78          0                   USD        2019-07
   ```
   {: screen}

   You can output the report in JSON format by specifying the `--output JSON` option.
   {: tip}


## _Task name_ with the API
{: #my-task-api}
{: api}



You can get usage reports from an enterprise and its accounts by calling the [Enterprise Usage Reports API (Beta)](/apidocs/enterprise-apis/resource-usage-reports). You can base the query in your API call on an enterprise, an account group, or an account and specify whether to view the entity or its children. The Enterprise Usage Reports API is a beta release.

The following examples show queries that you can use to get different usage reports. When you call the API, replace the ID variables and IAM token with the values from your enterprise.

- View usage for the entire enterprise for the current month.



   ```bash
   curl -X GET \
   "https://enterprise.test.cloud.ibm.com/v1/resource-usage-reports?enterprise_id=<ENTERPRISE_ID>" \
   -H "Authorization: Bearer <IAM_Token>" \
   -H 'Content-Type: application/json'
   ```
   {: codeblock}
   {: curl}

- View usage for an account group for July 2019.

   ```bash
   curl -X GET \
   "https://enterprise.test.cloud.ibm.com/v1/resource-usage-reports?account_group_id=<ACCOUNT_GROUP_ID>&month=2019-07" \
   -H "Authorization: Bearer <IAM_Token>" \
   -H 'Content-Type: application/json'
   ```
   {: codeblock}
   {: curl}

- View usage for account groups and accounts directly under the enterprise.

   ```bash
   curl -X GET \
   "https://enterprise.test.cloud.ibm.com/v1/resource-usage-reports?enterprise_id=<ENTERPRISE_ID>&children=true" \
   -H "Authorization: Bearer <IAM_Token>" \
   -H 'Content-Type: application/json'
   ```
   {: codeblock}
   {: curl}

## _Task name_ with Terraform
{: #my-task-terraform}
{: terraform}



1. In your Terraform configuration file, find the Terraform code that you used to create the namespace. 
2. Update the name of the namespace.

   ```terraform
   resource "cr_namespace" "namespace" {
     name = "<new_name>"
   }
   ```
   {: codeblock}
   
   Changing the name of a {{site.data.keyword.registryshort}} namespace cannot be done without deleting the old namespace and re-creating the namespace with a new name. Make sure that you backed up and removed any images that you stored in your namespace before you proceed. 
   {: important}
   
3. Create a Terraform execution plan.

   ```terraform
   terraform plan
   ```
   {: pre}
   
4. Remove the namespace and re-create it with a new name. Note that this process might take a few minutes to complete.
   
   ```terraform
   terraform apply
   ```
   {: pre}
   
5. List the namespaces in your account and verify that the namespace is created with a new name. 
   
   ```sh
   ibmcloud cr namespace-list
   ```
   {: pre}


