---
title: 'Operational Standards: Data Visualization (5)'
author: Datadog Support
modified: 2025-12-01T06:48:47.201Z
tags: []
metadata:
  type: Documentation
time:
  live_span: 1h
template_variables: []
---


# Data Visualization

# 

# 

## Data Visualization Workflow

# Dashboard Management Strategy

### Background

Dashboards are crafted to bring together all essential data for monitoring applications into a clear and concise view for your team. They usually include widgets (such as metrics, logs, monitors, and SLOs), template variables (filter variables for widgets), context links (which provide access to other dashboard views, monitors, or documentation with a click), and saved views (combinations of dashboard control settings).

### Recommended Approach

When creating dashboards, steer clear of simply duplicating the standard views (product pages or out of the box dashboards) offered by Datadog, like the basic host dashboard or an unfiltered host map. Instead, focus on a specific area of interest. For instance, an Infrastructure dashboard should highlight key host metrics and monitors pertinent to your team, while an Application dashboard can showcase vital performance indicators, including the application's SLOs.

To accommodate multiple teams, design more generic dashboards by creating versatile widgets and data groups, which can be further refined using controls and saved views. In cases where a generic dashboard is not feasible, consider creating template dashboards that can be cloned and customized by application owners.

An effective dashboard should allow the owner to assess system performance in about five seconds and quickly drill down to identify specific components causing issues, all with just a few clicks using the dashboard controls and context links.

#### Dashboard Strategy Architecture

The diagram above outlines our recommended dashboard structure, illustrating how each dashboard is linked to Monitors, SLOs, Datadog Service Summary Pages, and other related dashboards.

To implement this structure, follow these high-level steps:

1. **Create Monitors and SLOs**: Monitors and SLOs offer a quick snapshot of system health. Include relevant monitor and SLO views at the top of your dashboards to provide immediate insight into the system’s status.

2. **Develop App Overview Dashboard Templates**: These dashboards provide a comprehensive view of an application’s performance across all environments. They can focus on a single application or span multiple applications, depending on your organization’s requirements.

3. **(Optional) Build Core Dashboards**: Core Dashboards present a consolidated view of system performance across various applications and environments, offering a holistic perspective on overall system health.

**Refer to the next section for more details on steps 2 and 3.**

### Create App Overview Dashboard Template

To efficiently monitor applications and their associated integrations across different environments, we will establish a central App Overview Dashboard Template. This template serves as a baseline for all applications, containing a comprehensive set of widget groups representing the various Datadog integrations used across your organization. App owners can then clone this central template, customize it to fit their specific application needs, and maintain a consistent monitoring strategy.

### Design the Central App Overview Dashboard Template

The central template should include all necessary widgets to monitor application performance and integration health across all environments. The structure of the template will be as follows:

1. **SLO and Monitor Summary Section**:

  * Centralized display of key SLOs and monitor statuses applicable to all applications.

  * Widgets showing general application health, such as uptime, latency, and error rates.

2. **Widget Groups for Integrations:** Each widget group corresponds to a Datadog integration and should include custom context links to related core dashboards and resources:

| **INTEGRATION GROUP**| **DESCRIPTION**| **CONTEXT LINKS**|
|-|-|-|
| **WebLogic**| Widgets for active sessions, JDBC connection pool utilization, thread states, etc.| Add custom links to core dashboards for JVM performance, database monitoring, or thread utilization, enabling detailed exploration of WebLogic-specific metrics.|
| **Redis**| Widgets for memory usage, keyspace hits/misses, connected clients, etc.| Link to a Redis core dashboard with detailed insights into key metrics like cache performance, latency, and replication status.|
| **Tomcat**| Widgets for active threads, request processing time, connection pool status, etc.| Provide links to Tomcat service dashboards, covering metrics such as HTTP request performance and thread pool management.|
| **Other**| Include additional widget groups for all other relevant integrations (e.g., Kafka, MySQL, Kubernetes).| Add relevant links to core dashboards for each integration to facilitate deep dives.|

3. **General Application Metrics Section:** Widgets displaying core application metrics like response times, throughput, CPU, and memory usage.

4. **Global Context Variables:**

  * Use template variables like app, env, integration, and service to filter the dashboard dynamically.

  * This allows app owners to easily focus on specific environments or integrations when using the cloned dashboard.

5. **Context Links:**

  * _Custom Context Links:_ App owners should create custom context links within widget groups to connect to core dashboards that provide deeper insights into specific integration metrics. These links enable users to navigate seamlessly between the overview dashboard and detailed views, enhancing the monitoring and troubleshooting experience.

  * _Service Overview Pages:_ Leverage Datadog’s built-in context links on widget metrics to access related service overview pages directly. For example, clicking on a host or service name could take you to detailed host metrics or service traces, providing immediate access to additional context and details.

### Cloning the Central Dashboard Template

1. **Clone the Template:**

  * App owners clone the central App Overview Dashboard Template into their own workspace using Datadog's "Clone Dashboard" feature.

2. **Customize the Cloned Dashboard:**

  * **Delete Irrelevant Widget Groups:** Remove any widget groups for integrations that are not applicable to the specific application. For example, if the application does not use Redis, delete the Redis Integration Group from the cloned dashboard.

  * **Modify Relevant Widget Groups:** Update existing widgets to reflect application-specific configurations (e.g., specific SLOs, custom monitors).

  * **Add Edge-Case Widgets:** Add additional widgets to monitor any application-specific metrics or custom integrations not covered in the central template. For example, you might add a widget for a custom API response time metric or an integration with a third-party service.

  * **Update and Add Context Links:** Ensure that existing context links on integration widgets point to the relevant core dashboards. Add any additional custom context links needed to connect the overview dashboard to other detailed views or documentation relevant to the application.

3. **Save and Review:**

  * Save the customized dashboard and review it to ensure all necessary metrics and integrations are represented.

  * Test the cloned dashboard with relevant stakeholders to confirm it provides the needed insights.

### Adding Context Links to Core Dashboards

1. **Identify Core Dashboards:**

  * Determine which core dashboards are most relevant to the integrations included in the template (e.g., JVM performance, database health, message queue status).

2. **Link Integration Widgets to Core Dashboards:**

  * For each integration widget group, add custom context links to the appropriate core dashboards. This allows users to quickly navigate from high-level integration metrics to more detailed views.

  * Examples:

    * WebLogic thread state widget links to a core dashboard for thread and garbage collection analysis.

    * Redis memory usage widget links to a Redis-specific dashboard for deeper insights into memory allocation and eviction policies.

### Maintaining Consistency and Updates

1. **Version Control for the Central Template:**

  * Maintain a version history for the central template, documenting any changes or improvements.

  * Notify app owners of updates to the template, encouraging them to review their cloned dashboards for potential improvements.

2. **Centralized Changes:**

  * If a new integration or general monitoring need arises, update the central template with new widget groups or widgets.

  * Provide guidance for app owners to incorporate these changes into their cloned dashboards.

3. **Feedback Loop:**

  * Gather feedback from app owners on the effectiveness of the template.

  * Use this feedback to refine the central template over time, ensuring it evolves with the organization’s monitoring needs.

### Documentation and Best Practices

1. **Provide Documentation:**

  * Document the structure and intended use of the central App Overview Dashboard Template.

  * Include instructions on how to clone, customize, and maintain the cloned dashboards, as well as how to create and utilize custom context links effectively.

2. **Establish Best Practices:**

  * Create a set of best practices for app owners to follow when customizing their dashboards, such as how to name dashboards, organize widget groups, handle edge cases, and create custom context links.

By following this approach, app owners can create customized dashboards that provide a comprehensive view of their application’s performance and health, along with detailed insights into associated Datadog integrations. The use of custom context links to core dashboards and service overview pages enhances the ability to quickly access deeper information, facilitating efficient monitoring and troubleshooting.

### (Optional) Create Core Dashboards

We will start by creating a set of core dashboards, which are scoped product, integration, and other datasets grouped across multiple environments and applications. Each core dashboard should implement template variables based on your tagging and governance strategy.

Each core dashboard should have a simple name describing its scope, and be prefixed with the integration name, product, or application type it is associated like so:

\[ <DASHBOARD TYPE> \] <INTEGRATION/APP NAME> - <SHORT DESCRIPTION>

Here are some Core Dashboards that we recommend you create:

| **DASHBOARD NAME**| **DESCRIPTION**| **WIDGETS**| **SAMPLE TEMPLATE VARIABLES**|
|-|-|-|-|
| **\[ Integration \] System - Host Metrics**| Displays the most critical metrics for infrastructure hosts| Monitor List, Static CPU usage, CPU usage by host, CPU usage by CPU type, Memory Usage, etc| host, env, runtime, tier, platform, application, etc|
| **\[ Datadog Admin \] APM - Datadog Trace Agent Metrics**| An administrative dashboard displaying runtime metrics for Datadog trace agents running across your environment| Monitor List, Trace Agent CPU utilization per host, Span Writes per host, etc| host, env, runtime, tier, platform, application, etc|
| **\[ Datadog Admin \] Infrastructure - Datadog Agent Metrics**| An administrative dashboard displaying runtime metrics for Datadog agents running across your environment| Monitor List, Agent Up Checks, Agent CPU utilization per host, Agent memory utilization per host, etc| host, env, runtime, tier, platform, application, etc|

### ✅ Decision Point

* Reference your [Engagement Project Plan](https://docs.google.com/spreadsheets/d/1ok2QB6lyIshN6KPnzRrerfopiERnqt5-lQ9P8ZvLseA/edit?gid=671465123#gid=671465123) to input your decisions and create your strategy.

### ⭕ Action Items

| **STATUS**| **TASK**|
|-|-|
| Not Started| Create your Core Dashboards|
| Not Started| Create your App Overview Dashboards|
