---
title: 'Operational Standards: Data Monitoring (4)'
author: Datadog Support
modified: 2025-12-01T06:48:04.509Z
tags: []
metadata:
  type: Documentation
time:
  live_span: 1h
template_variables: []
---


# Data Monitoring

#### 

#### 

## Log Management Strategy

### Log Index Strategy

#### Background

Log Indexes in Datadog provide a method for managing and optimizing your log data by segmenting it into distinct groups based on business or technical needs. This segmentation allows organizations to tailor retention periods, apply quotas, track usage, and manage billing effectively. They are required to use your logs in dashboards and monitors.

By default, all logs are captured into a single catch-all index titled “main” and retention is set to 15 days regardless of contract details. For effective log data management, it’s essential to create additional indexes with distinct retention policies, sampling rates, and access controls based on the type of logs.

Log indexes are defined by filters, where:

* **Inclusion Filters** determine if a log should be included in a specific index.

* **Exclusion Filters** define if a log should be excluded or dropped after passing the inclusion filter.

Each log is evaluated against index filters in sequence, and logs can only be retained in one index. Logs that don't match any inclusion filter or match an exclusion filter are dropped.

_Note: This strategy assumes 100% ingestion and no pre-ingestion log processing through Datadog Observability Pipelines or third-party frameworks like OTEL, Logstash, or Cribl being utilized._

#### Supported Documentation

* [Best Practices for Log Management Guide](https://docs.datadoghq.com/logs/guide/best-practices-for-log-management/)

* [A Guide to Log Management Indexing Strategies with Datadog](https://blog.psa-dd.io/a-guide-to-log-management-indexing-strategies-with-datadog-a727539c9e50)

#### Recommended Approach

##### Strategy Overview

The generic strategy we recommend is described in the diagram above. It consists of the following steps:

1. Log data from your workloads are ingested into your Datadog organization. The ingested logs will be searchable for 15 minutes via Live Tail.

2. From there, log data can either be retained in an index, sent to an archive, or have metrics generated from it. This happens independently and concurrently. It is possible to do some, none, or all of these steps.

3. For archived data, you provide cloud storage for the data to live, and upon rehydrating, ingestion and indexing costs apply as well as network egress costs from your cloud provider.

4. For metrics, custom metrics rates apply.

##### Building Your Own Strategy

**1. Define Indexes Based on Retention Buckets and Use Cases**

* **Segmentation by Log Type:** To optimize log management, it's essential to segment logs both by log type and environment. This allows for more granular control over log retention, filtering, and cost management based on the nature of the logs and the environment in which they were generated.

  * _Reference:_ [Log Index Segmentation Strategies](https://docs.google.com/document/d/1HhJSpluTu6ivgHs0TlptjuuLKhQTUJOX74vL9sja_us/edit#heading=h.porbjh43py3a)

* **Retention Policies:** Set retention periods for each log type based on compliance, troubleshooting needs, or cost-saving strategies.

  * Short-term retention for high-volume, short-lived logs (e.g., debug logs).

  * Long-term retention for critical business logs (e.g., security or audit logs).

* **Use Case Segmentation:** Define different indexes for varying organizational use cases such as:

  * _Compliance and Security Logs:_ Ensure audit trails and security events are retained for regulatory purposes.

  * _Operational Logs:_ Set up indexes for app performance and infrastructure logs that require real-time monitoring but shorter retention.

* **Exclusion Strategy:** Use exclusion filters for irrelevant logs (e.g., excessive debugging or non-critical logs) that do not need to be indexed.

**2. Define Storage for Long-Term Retention**

* Leverage _Datadog's built-in retention settings_ for longer-term data retention within the platform.

* For long-term historical analysis or compliance needs, there are two options:

  * [Archive Storage](https://docs.datadoghq.com/logs/log_configuration/archives/?tab=awss3) in external services like Amazon S3 or Azure Blob Storage. Good for long retention time where querying in a matter of hours is acceptable.

  * [Flex Logs](https://docs.datadoghq.com/logs/log_configuration/flex_logs/#potential-sources-for-sending-directly-to-flex-logs) is a hybrid of indexing and archiving, managed by Datadog. Good for long retention time where querying in a matter of minutes is required.

* Define how long logs should remain in Datadog versus being archived (e.g., retain logs for 15 days in Datadog, archive them for 1 year).

**3. Define an Archiving Strategy**

* **Archiving to External Storage:** Set up automated processes to archive logs to cost-efficient storage for extended retention needs.

  * Configure archival storage in AWS S3, Google Cloud Storage, or another preferred storage solution.

* **Retrieving Archived Logs:** Ensure archived logs can be restored or queried easily if needed for audits or investigations.

* **Optimizing Costs:** Regularly review the volume and types of logs stored in your archive and implement strategies for pruning outdated logs.

### Log Index Segmentation Strategies

#### Segmentation by Log Type

| **LOG TYPE**| **DESCRIPTION**| **USE CASE**| **RETENTION**|
|-|-|-|-|
| **Application Logs**| Logs generated by your applications.| Useful for troubleshooting, debugging, and performance monitoring.| Shorter retention for debug logs; longer retention for production logs.|
| **Security Logs**| Logs related to authentication, authorization, and other security events.| Critical for audit trails, intrusion detection, and compliance.| Longer retention periods, often mandated by regulatory requirements.|
| **Infrastructure Logs**| Logs from infrastructure components like servers, databases, and networking devices.| Monitoring system health, capacity planning, and troubleshooting.| Varies depending on the nature of the infrastructure (e.g., production vs. development environments).|
| **Audit Logs**| Logs that capture user activity and changes to systems.| Ensuring accountability and compliance, tracking changes, and security investigations.| Long-term retention for regulatory compliance.|
| **Compliance Logs**| Specific logs required for legal and regulatory purposes.| Ensures compliance with industry standards such as GDPR, HIPAA, etc.| Extended retention to meet legal requirements.|

#### Segmentation by Environment

| **ENVIRONMENT**| **DESCRIPTION**| **USE CASE**| **RETENTION**|
|-|-|-|-|
| **Development Environment**| Logs from systems used for development and testing.| Helps developers troubleshoot and test features.| Shorter retention, as these logs are less critical and primarily for quick feedback loops.|
| **Staging/Pre-production**| Logs from systems that mimic production environments for testing purposes.| Used to simulate production workloads and test for bugs or performance issues before deployment.| Intermediate retention, long enough to validate deployments but not as long as production logs.|
| **Production Environment**| Logs generated in the live, customer-facing environment.| Critical for monitoring live applications and ensuring operational stability.| Longer retention, especially for security, compliance, and business-critical operations.|

#### How to Segment by Both Log Type and Environment

1. **Combination Filtering**:

  * Use log indexes to create filters that combine log type and environment. For example, create an index for _Production Application Logs_ and another for _Development Security Logs_.

  * Example Filter: `service:application AND env:production` for production application logs, and `service:security AND env:dev` for development security logs.

2. **Retention and Sampling Strategies**:

  * Apply different retention and sampling policies for logs depending on both their type and the environment.

  * Example: **Production Application Logs** might have a retention period of 30 days with no sampling, while **Development Application Logs** might have a retention period of 7 days with sampled retention.

3. **Access Control**:

  * Use Datadog’s Role-Based Access Control (RBAC) to ensure only appropriate teams have access to certain indexes. For example, developers may only need access to logs from the development environment, while the security team needs access to all security logs across environments.

By segmenting logs both by **log type** and **environment**, you gain enhanced control over data retention, cost management, and log accessibility, while ensuring critical logs are appropriately stored and monitored across your organization.

#### Sample Segmented Log Index Strategy

| **INDEX NAME**| **FILTER CRITERIA**| **RETENTION PERIOD**| **EXCLUSION/SAMPLING**| **NOTES**|
|-|-|-|-|-|
| **Production Critical Logs**| `status:error OR status:warning`| 7 days| Sample 15-30% for specific sources| Use for high-priority error and warning tracking|
| **Production Info Logs**| `status:info`| 3 days| Sample 30-75%| Include optional 30+ day Flex Logs for analysis|
| **Non-Production Error Logs**| `env:non-prod AND (status:error OR status:warning)`| 3 days| Exclude all info/debug logs| Focus on critical errors; archive all excluded logs|
| **Non-Production Info Logs**| `env:non-prod AND status:info`| 3 days| Exclude all debug logs| Route to archives; sample if needed|
| **Debug Logs**| `status:debug`| Excluded| Use Live Tail for real-time access| Generally excluded to reduce noise|
| **Catch-All Index**| `\*`| 3 days| Minimal sampling to capture unknown logs| Monitor for unclassified logs and adjust strategy|

#### Implementation Considerations

* **Sampling & Exclusion:** Apply sampling to info-level and low-density logs. Certain logs like application health checks or debug logs are excluded or routed to archives.

* **Retention & Flex Logs:** Flex Logs are used for long-term storage of high-volume, low-value logs such as network flow logs or non-critical status logs. These logs bypass standard indexing, saving costs while retaining logs for audit and compliance purposes.

* **RBAC:** Proper Role-Based Access Control (RBAC) is implemented to ensure that only relevant teams have access to the logs based on their role (e.g., Security Team for security logs, DevOps for infrastructure).

* **Catch-All Index:** A fallback index is in place to capture any logs that do not match specific index criteria, ensuring no logs are lost unintentionally.

### ✅ Decision Point

* Reference your \[**Engagement Project Plan**\] to input your decisions and create your strategy.

### ⭕ Action Items

| **STATUS**| **DESCRIPTION**|
|-|-|
| Not Started| Identify and document all log types and sources|
| Not Started| Identify and document retention, sampling and access requirements for all log types and sources|
| Not Started| Define the retention policy based on the grouping from the first two steps|
| Not Started| Create log indexes with defined retention policies|
