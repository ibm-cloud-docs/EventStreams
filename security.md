---

copyright:
  years: 2023
lastupdated: "2023-04-26"

keywords: security, gdpr, hipaa, compliance, personal data, personal information, privacy policy, cloud notice, terms of use, event streams

subcollection: EventStreams

---

{{site.data.keyword.attribute-definition-list}}

# Security and compliance
{: #compliance}

{{site.data.keyword.messagehub_full}} provides a trustworthy and secure cloud database system. The service is built on best-in-industry standards, including ISO 27001:2013.

## {{site.data.keyword.cloud_notm}} for Financial Services
{: #cloud_fs}

{{site.data.keyword.hscrypto}} is {{site.data.keyword.cloud}} for [Financial Services](https://www.ibm.com/cloud/financial-services) certified. For information about requesting an {{site.data.keyword.cloud_notm}} for Financial Services report, see [{{site.data.keyword.cloud_notm}} industry compliance programs](https://www.ibm.com/cloud/compliance).

## General Data Protection Regulation (GDPR)
{: #gdpr}

If you have an account with {{site.data.keyword.cloud_notm}}, your personal data is held by {{site.data.keyword.cloud_notm}}. The [IBM Data Processing Addendum (IBM DPA)](https://www.ibm.com/support/customer/csol/terms/?cat=dpa) applies to the processing of clients' personal data by IBM on behalf of the client to provide IBM standard services.

{{site.data.keyword.messagehub}} processes limited client Personal Information (PI) in the course of running the service and optimizing the user experience.

{{site.data.keyword.messagehub}} provides a [Data Sheet Addendum (DSA)](https://www.ibm.com/software/reports/compatibility/clarity-reports/report/html/softwareReqsForProduct?deliverableId=AC17FFB0B52911E7A9EB066095601ABB) with its policies as a data processor regarding content and data protection.

## Health Insurance Portability and Accountability Act (HIPAA)
{: #hipaa}

{{site.data.keyword.messagehub}} with {{site.data.keyword.keymanagementservicelong}} for managing encryption keys meets the required IBM controls that are commensurate with the Health Insurance Portability and Accountability Act of 1996 (HIPAA) Security and Privacy Rule requirements. These requirements include the appropriate administrative, physical, and technical safeguards required of Business Associates in 45 CFR Part 160 and Subparts A and C of Part 164. HIPAA must be requested at the time of provisioning and requires a representative to sign a Business Associate Addendum (BAA) agreement with IBM.

## ISO 27001/27017/27018 and ISO 27701
{: #iso}

{{site.data.keyword.messagehub}} is ISO 27001, 27017, 27018, and ISO 27701 certified. The certificates and the certified cloud products listing can be found in the [IBM Trust Center](https://www.ibm.com/trust) in section [IBM Cloud Compliance Programs - Global](https://www.ibm.com/cloud/compliance/global).

## Information System Security Management and Assessment Program (ISMAP) 
{: #ismap}

{{site.data.keyword.messagehub}} Standard and Enteprise plans are certified by ISMAP (Information System Security Management and Assessment Program), the Japanese government program for assessing the security of public cloud services.

## Cloud Computing Compliance Controls Catalogue (C5)
{: #c5}

{{site.data.keyword.messagehub}} Standard and Enterprise plans are certified to C5 (Cloud Computing Compliance Controls Catalogue) and meet the requirements for cloud security and the adoption of public cloud solutions by German government agencies.

## SOC 2 Type 1 Certification
{: #soc2_type1}

{{site.data.keyword.messagehub}} is SOC 2 Type 1 certified. For information about requesting an {{site.data.keyword.cloud_notm}} SOC 2 report, see [IBM Cloud global compliance programs](https://www.ibm.com/cloud/compliance).

## SOC 2 Type 2 Certification
{: #soc2_type2}

{{site.data.keyword.IBM}} provides a Service Organization Controls (SOC) 2 Type 2 report for {{site.data.keyword.messagehub}}. The reports evaluate {{site.data.keyword.IBM_notm}}'s operational controls according to the criteria set by the American Institute of Certified Public Accountants (AICPA) Trust Services Principles. The Trust Services Principles define adequate control systems and establish industry standards for service providers such as {{site.data.keyword.cloud_notm}} to safeguard their customers' data and information.

You can request a SOC 2 Type 2 report from the customer portal or contact your sales representative. Alternatively, you can open a support ticket with [IBM Cloud support](https://cloud.ibm.com/unifiedsupport/supportcenter).

## PCI DSS
{: #pci_dss}

{{site.data.keyword.messagehub}} is compliant with the Payment Card Industry Data Security Standard (PCI DSS). {{site.data.keyword.cloud_notm}} completes annual PCI DSS assessments by using an approved Qualified Security Assessor (QSA), and the resulting Attestations of Compliance (AOCs) and Service Responsibility Matrix (SRM) guides are available upon customer request. Auditors reviewed {{site.data.keyword.messagehub}} for compliance under PCI DSS version 3.2.1 at Service Provider Level 1.

If you intend to store sensitive information in an IBM Cloudant database, you must use client-side encryption to render data unreadable to IBM Cloudant operators. For example, for PCI DSS compliance, you must encrypt the Primary Account Number (PAN) before sending a document that contains it to the database.
{: tip}

Customers are responsible for the storing, processing, and transmission of their cardholder data, and can create cardholder data environments (CDEs) that can store, transmit, or process cardholder data by using {{site.data.keyword.messagehub}}. Customers can request and use the {{site.data.keyword.cloud_notm}} AOCs and SRM guides when they seek their own PCI DSS certifications. It is the responsibility of the customer to document and operate CDEs and applications that are built by using {{site.data.keyword.cloud_notm}} Platform services in a PCI DSS-compliant manner.

{{site.data.keyword.messagehub}} documentation on service security and deletion of data covers methods to manage cardholder data within the environment in accordance with PCI requirements. It is the customer’s responsibility to familiarize themselves with these processes an
d to manage data retention and removal from the service according to the customer’s policies. To facilitate this process, no cardholder data can be used in an {{site.data.keyword.messagehub}} document ID. If PAN data is to be stored in {{site.data.keyword.messagehub}}, they must be rendered unreadable (in accordance with PCI requirement 3.4) before transmission to the {{site.data.keyword.messagehub}} service.

A full list of PCI DSS-ready {{site.data.keyword.cloud_notm}} Platform services, and options to request a PCI DSS AOC and SRM guide, can be found at the [IBM Cloud compliance page](https://www.ibm.com/cloud/compliance).

