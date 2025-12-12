---
title: 'Operational Standards: Tagging Strategy'
author: Datadog Support
modified: 2025-12-01T02:02:41.506Z
tags: []
metadata:
  type: Documentation
time:
  live_span: 1h
template_variables: []
---


# Tagging Standards Strategy

### Background

Tagging is Datadog’s implementation of [metadata](https://en.wikipedia.org/wiki/Metadata), similar to AWS’s tags and GCP’s labels. [Tags](https://docs.datadoghq.com/getting_started/tagging/) ensure that your telemetry can be queried, aggregated, and correlated efficiently and effectively. Having a rich, consistent, and accurate tagging strategy across your whole organization is essential to get the most out of Datadog.

If your company does not have a company wide tagging strategy yet, Datadog strongly recommends creating one.

### Supported Documentation

* [Getting Started with Tags](https://docs.datadoghq.com/getting_started/tagging/)

* [Unified Service Tagging](https://docs.datadoghq.com/getting_started/tagging/unified_service_tagging)

* [Best Practices for Tagging Your Infrastructure and Applications | Datadog](https://www.datadoghq.com/blog/tagging-best-practices/)

### Formatting

Tags are converted to lowercase. Therefore, CamelCase tags are not recommended. Authentication (crawler) based integrations convert camelcase tags to underscores, for example TestTag –> test_tag. Underscores are preferred over hyphens for consistency.

### Recommended Approach

#### _Initiating an Effective Tagging Strategy_

#### 1. Understanding Scopes and Dimensions

_Scopes_ refer to the context in which a tag applies, such as environments or services, while _Dimensions_ provide specific attributes that describe an object within that scope.

* **Global Scope**: Tags like env (environment) apply universally across all resources.

* **Service-Specific Scope**: Tags like service provide context specific to application services.

* **Location Scope**: Tags that specify where resources are located, such as region or datacenter.

#### 2. Key Tagging Categories

Based on Datadog's Unified Service Tagging (UST) approach, here are the recommended tagging categories:

| | | |
|-|-|-|
| **TAGGING CATEGORY**| **RECOMMENDED KEY VALUE(S)**| |
| **Infrastructure**| Environment| env: (e.g., dev, prod, qa|
| Location| region: (e.g., us-west-1)datacenter: (e.g., us1.prod)availability-zone: (e.g., us-west-1a)| |
| Specifications| os: (e.g., linux, windows)instance-type: (auto-inferred)| |
| Ownership| cost_center: (e.g., sales-001)business_unit: (e.g., support)| |
| Team| team: (e.g., dev-team, ops-team)| |
| **Service (APM)**| Unified Service Tags| service: (e.g., payment-gateway)env: (e.g., prod)version: (e.g., v1.0)|
| Ownership| support_team: (e.g., support-team)business_unit: (e.g., finance)| |
| Function| function: (e.g., webserver, middleware)| |
| Custom Span Tags| For added granularity in tracing, implement custom span tags as needed| |

#### 3. Implementation of Tags

* **Automatic Inheritance**: Leverage tags from cloud providers and integrations automatically collected by Datadog (see[ Unified Service Tagging](https://docs.datadoghq.com/getting_started/tagging/unified_service_tagging)).

* **Manual Configuration**: For integrations without inherited tags, implement tags via configuration files (e.g., datadog.yaml).

#### 4. Log Tags

Ensure logs include necessary tags:

* service: (e.g., web-store)

* source: (e.g., nginx)

#### 5. Tagging Best Practices

* **Consistency**: Maintain consistent naming conventions for keys and values across all telemetry. Refer to[ tagging best practices](https://www.datadoghq.com/blog/tagging-best-practices/).

* **Documentation**: Document all tags and their purposes, ensuring clarity for all teams.

* **Automation**: Use infrastructure as code (IaC) to enforce tagging policies.

* **Dynamic Alerts**: Configure alerts that utilize tags for efficient routing and context in notifications.

By implementing this tagging strategy, you can effectively organize and manage your observability data in Datadog, providing valuable context for monitoring and troubleshooting across your applications and infrastructure.

#### _Reserved Tags_

Datadog reserved tags are predefined tags that the platform automatically applies to resources based on specific attributes, providing a standardized way to categorize and manage monitoring data. These tags include attributes like service, env, region, and host, which help users filter and aggregate metrics, logs, and traces across their infrastructure. By using reserved tags, organizations can gain quick insights into their system's performance and health, as these tags facilitate easy querying and visualization in dashboards. Additionally, reserved tags enhance alerting capabilities by ensuring that notifications are appropriately routed based on common attributes, streamlining incident response and improving overall observability.

| | | | |
|-|-|-|-|
| [RESERVED TAGS](https://docs.datadoghq.com/getting_started/tagging/#overview)| | | |
| **TAG KEY**| **SAMPLE TAG VALUES**| **DESCRIPTION**| **BUSINESS VALUE**|
| \*\*env \*\*| dev, stage, prod| The environment in which the service or application is running.| Ensures critical telemetry can be easily identified. Essential for enabling appropriate monitoring, and access control.|
| \*\*service \*\*| auth-server,  middleware, api-gateway| Defines the specific service or function being monitored. Should be descriptive, concise and easily understandable.| Important for tracking performance and availability of distinct services, ensuring targeted alerts and diagnostics.|
| \*\*version \*\*| 2.1.3, v1.0, 06142ee, etc…| Specifies the version of the application or service being deployed. Can include semantic versioning or specific commit hashes.| Essential for tracking changes, identifying issues related to specific versions, and ensuring compatibility and compliance with release management practices.|
| **source**\*\*  \*\*| python, cisco, nginx| Ensures logs get routed to their appropriate pipelines to be parsed and processed.| Allows logs to be logically grouped based on their underlying technology and logger. Makes log processing more efficient.|
| **host**\*\*  \*\*| [fqdn.domain.com](http://fqdn.domain.com)| Where applicable, identifies where telemetry is shipping from. Usually automatically inferred, can be set.| Allows telemetry to be filtered by what infrastructure it is shipped from|
| **device**| c:, d:, eth0| Where applicable, identifies disk drives or network devices for relevant telemetry| Crucial dimension for storage and network telemetry.|

#### _Integration Tags_

Certain integrations, like those for AWS, Azure, or GCP, come with built-in tags that are automatically applied to relevant resources. For example, the AWS integration provides tags such as region, availability-zone, and account-id. This feature eliminates the need to manually assign specific tags to resources that are discovered automatically through these integrations.

# _Recommended Tags_

The recommended tags for Datadog provide a structured approach to organizing and managing monitoring data across services and applications. Key tags include **team**, which identifies the responsible group (e.g., integrations, SRE, DevOps) and facilitates accountability and communication; **framework**, which names the software being used (e.g., Apache, Tomcat) and aids in technology stack insights; and **role**, describing the function of a service (e.g., web, app, cache) to enhance understanding of system dependencies. Other important tags include **tier**, indicating the criticality of the service for prioritizing monitoring efforts, and **backup**, which classifies data protection strategies (e.g., bronze, silver, gold) to ensure business continuity. Tags like **platform**, **product**, and **network** help clarify infrastructure dependencies, business domains, and network segments, while **compliance** and **datatype** tags ensure adherence to regulatory requirements and data protection standards. Finally, the **datacenter** tag specifies the physical location of services, supporting disaster recovery planning and compliance with data residency regulations. Overall, these tags enhance observability, streamline incident management, and align monitoring efforts with business objectives.

| | | | |
|-|-|-|-|
| **RECOMMENDED TAGS**| | | |
| **TAG KEY (PRIORITY)**| **SAMPLE TAG VALUES**| **DESCRIPTION**| **BUSINESS VALUE**|
| **team (critical)**| integrations, sre, devops| Identifies the team responsible for the service or application. Examples include integrations, site reliability engineering (SRE), and DevOps teams.| Helps in assigning responsibility, facilitating communication, and streamlining incident response and resolution processes.|
| **runtime (high)**| apache, tomcat, weblogic, etc…| Names the application or software being used. Common examples are web servers and application servers like Apache, Tomcat, and WebLogic.| Provides insight into the technology stack, aiding in configuration management, compatibility checks, and resource allocation.|
| **Journey (high)**| login, checkout, browsing, registration, file_upload, password_reset, order_tracking| Tracks key user journeys across various processes, such as logging in, browsing products, completing checkout, uploading files, resetting passwords, and tracking orders.| Ensures high reliability and performance of critical user flows, improving user experience, reducing churn, and driving revenue by minimizing disruptions.|
| **role (high)**| app, web, cache, worker, leader| Indicates the role of a host or service within a larger system. This tag is useful for distinguishing key components in a distributed system, where each component has a specific responsibility.| Helps teams quickly isolate issues, optimize performance, and maintain system reliability in complex distributed systems.|
| **tier (medium)**| 1, 2, 3,4| Indicates the criticality or priority level of the service. Tier 1 typically represents the most critical services, while higher numbers indicate lower criticality.| Essential for prioritizing monitoring efforts, resource allocation, and incident management based on the criticality of the service.|
| **backup (medium)**| bronze, silver, gold| Classifies the backup and recovery strategy for the service. Bronze, Silver, and Gold often represent increasing levels of backup frequency and retention.| Important for ensuring data protection and business continuity, helping to manage risk and meet recovery time objectives (RTO) and recovery point objectives (RPO).|
| **platform (medium)**| middleware, ecosystem, common platform, etc…| Specifies the underlying platform or ecosystem on which the service operates. Examples include middleware solutions, broader technology ecosystems, or shared platforms.| Critical for understanding the infrastructure dependencies, facilitating integration, and ensuring compatibility and standardization across services.|
| **application (high)**| store-platform, payments, ads, etc.| Identifies how services and resources are grouped together into a larger business workload.Represents the name of the application defined internally by the customer. This could include derivative applications that are part of a larger platform.| Allows grouping, organizing, and filtering of resources relating to a large business application, such as microservices, hosts, and containers. This tag enables effective monitoring, performance analysis, and alignment of applications compared with business goals.|
| **product (medium)**| crm, cms, etc.| Identifies the business product or application domain. Examples include customer relationship management (CRM) systems and content management systems (CMS).| Helps in aligning monitoring and optimization efforts with business objectives and ensuring the performance of key business applications.|
| **network (medium)**| dmz, internal, external, etc…| Describes the network segment where the service is running. DMZ (demilitarized zone), internal, and external networks are common examples.| Important for understanding network security considerations, traffic patterns, and potential vulnerabilities, enabling appropriate security measures and monitoring.|
| **compliance (medium)**| pci-dss, non-pci, sox, fedramp, gdpr, hipaa, etc…| Specifies the compliance standards or regulations applicable to the service. Examples include PCI-DSS (Payment Card Industry Data Security Standard), SOX (Sarbanes-Oxley Act), FedRAMP (Federal Risk and Authorization Management Program), GDPR (General Data Protection Regulation), and HIPAA (Health Insurance Portability and Accountability Act).| Essential for ensuring adherence to regulatory requirements, managing legal and financial risks, and maintaining customer trust and business reputation.|
| **datatype (medium)**| financial, phii, pii,| Identifies the type of data handled by the service. Examples include financial data, PHI (protected health information), and PII (personally identifiable information).| Critical for data classification, implementing appropriate security controls, and ensuring compliance with data protection regulations and best practices.|
| **datacenter (medium)**| fdc, mdc, wdc, etc…| Specifies the physical data center location where the service or application is hosted. Examples include FDC (Primary Data Center), MDC (Main Data Center), and WDC (West Data Center).| Important for understanding the geographical and physical hosting environment, enabling effective disaster recovery planning, latency management, and compliance with data residency regulations.|
