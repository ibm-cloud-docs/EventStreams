---
 
copyright:
  years: 2021
lastupdated: "2021-05-18"

subcollection: your-subcollection

keywords: _doing this task_ in the console, _doing this task_ in the UI, _doing this task_ cli, _doing this task_ command line, _doing this task_ API, _doing this task_ with Terraform

---

{{site.data.keyword.attribute-definition-list}}

<!-- File guidance:
This template demonstrates how to incorporate steps for completing a task using your offering's UI, CLI, and API into your docs.
As always, following good topic-based writing practices means that every task should have a single topic. You can organize this information in two ways: as a standalone topic, where the entire page (H1) is about a single task and each interface is an H2 section, or as a second-level topic (H2) within a page, where each interface is an H3 section. Choose the structure that best fits your needs, and replace the example content in this template with your own. -->

<!-- The title of your topic should describe a user goal and start with a gerund (-ing form derived from a verb). For example, "Viewing enterprise usage".-->
# _Task name_
{: #my-task}

<!-- Content guidance: 
The short description should be a single, concise paragraph that contains one or two sentences and no more than 50 words. For SEO, include your product name keyref (with trademark for first mention) and any keywords that relate to the task that you're describing.-->
You can track resource and support costs from accounts in your {{site.data.keyword.cloud}} enterprise by viewing their usage. The accounts and account groups that you can view usage for depends on your assigned access.
{: shortdesc} 

<!-- For the UI section, use the main task name, and add "in the UI" at the end. For example, "Viewing enterprise usage in the UI"-->
## _Task name_ in the UI
{: #my-task-ui}
{: ui}

<!-- Content guidance: 
Follow standard best practices for procedural information - see IBM Style: https://ibmdocs-test.mybluemix.net/docs/en/ibm-style?topic=format-procedures
Some tips for working in Markdown:
- Use ordered lists (1.) for steps and unordered lists (* or -) for options. Ordered lists are automatically numbered, so you can always use 1. as shown below.
- Code clickable UI links or buttons with **bold**.
-->

1. Log in to the enterprise account.
1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage > Billing and usage**, and select **Usage**.

   The Usage page displays the costs for all resource usage in the entire enterprise during the current month. Usage is organized according to your enterprise hierarchy, so costs are broken down by the accounts and account groups that are directly under the enterprise. 
   
1. To view usage within an account group, click the account group name in the table or in the **Enterprise level** menu. Similar to the enterprise level, usage is broken down by the account and account group.

   If an account group doesn't contain any accounts, it isn't displayed on the Usage page.

1. _More steps as needed for your task_

<!-- For the CLI section, use the main task name, and add "from the CLI" at the end. For example, "Viewing enterprise usage from the CLI"-->
## _Task name_ from the CLI
{: #my-task-cli}
{: cli}

<!-- Content guidance: 
To demonstrate the steps to complete a task using the CLI, explain the command and then provide one or more realistic command examples. 

First, include an introductory sentence or two that explains the command to use. Provide any additional explanation that's needed to explain how the values in the command translate to the action that's completed. Because the text in command code blocks is not translated, the introduction provides a chance to explain what's happening in a plain-text format that's readable in all languages.

For the command examples, use realistic values for the arguments and options that users input when they run the command. Provide multiple examples if needed to explain different scenarios.
-->

<!--    *******************************    -->
<!--    Option 1: Single command format    -->
<!--    *******************************    -->

To view usage across an entire enterprise, run the [**`ibmcloud billing enterprise-usage`**](/docs/cli?topic=cloud-cli-ibmcloud_billing#ibmcloud_billing_enterprise_usage) command. By default, usage for the current month is displayed. You can view usage for a specific month by specifying the year and month on the `--month` option. For example, the following command displays usage information for April 2020.

```sh
ibmcloud billing enterprise-usage --month 2020-04
```
{: pre}

<!-- If your command outputs a report or other information, include an example and explain what the user is seeing. Make sure to separate the command output from the command itself so that the command is in a separately copyable codeblock. -->
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


<!--    ***********************************    -->
<!--    Option 2: Multi-step command format    -->
<!--    ***********************************    -->

<!-- If multiple steps are needed to complete the task, use the following format. As with other tasks, use ordered list items for each step in a sequence, and unordered list items for options. Make sure that you keep the steps focused on the task and why they're performing each action rather than just listing the commands in sequence. This helps the user better understand the purpose of each command instead of learning by rote. -->

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

   <!-- If your command outputs a report or other information, include an example and explain what the user is seeing. Make sure to separate the command output from the command itself so that the command is in a separately copyable codeblock. -->
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

<!-- For the API section, use the main task name, and add "with the API" at the end. For example, "Viewing enterprise usage with the API"-->
## _Task name_ with the API
{: #my-task-api}
{: api}

<!-- Content guidance: 
As with the CLI, introduce the API and provide a link to the related API docs. Then introduce the specific API call example, and explain the example in plain text. Use multiple examples if you have multiple scenarios that you want to illustrate.

It's always best to use realistic sample values instead of variables in examples. However, if you need to use variables, call out which items in the examples are variables and remind the user to replace them with their own values.
-->

You can get usage reports from an enterprise and its accounts by calling the [Enterprise Usage Reports API (Beta)](/apidocs/enterprise-apis/resource-usage-reports). You can base the query in your API call on an enterprise, an account group, or an account and specify whether to view the entity or its children. The Enterprise Usage Reports API is a beta release.

The following examples show queries that you can use to get different usage reports. When you call the API, replace the ID variables and IAM token with the values from your enterprise.

- View usage for the entire enterprise for the current month.

<!-- To highlight your API examples, add the language next to the first backtick. Popular languages for API calls are cURL (```bash), Node.js (```javascript), Python (```python), Go (```go). In addition, add the language attribute following the codeblock. For more examples, see https://test.cloud.ibm.com/docs/developing/writing?topic=writing-css-test-for-markdown-changes.  After the code block, add the {: codeblock} attribute, followed by the language attribute. -->

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

<!-- Be sure to use terraform syntax highlighting on any Terraform configuration examples, such as shown in step 2.-->

1. In your Terraform configuration file, find the Terraform code that you used to create the namespace. 
2. Update the name of the namespace.

   ```terraform
   resource "cr_namespace" "namespace" {
     name = "<new_name>"
   }
   ```
   {: codeblock}
   
   Changing the name of a {{site.data.keywords.registryshort}} namespace cannot be done without deleting the old namespace and re-creating the namespace with a new name. Make sure that you backed up and removed any images that you stored in your namespace before you proceed. 
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


