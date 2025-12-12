---
title: <CUSTOMER> - HealthCheck Account Analysis
author: Datadog Support
modified: 2025-12-01T07:03:32.020Z
tags: []
metadata: {}
time:
  live_span: 1w
template_variables: []
---



# Overview of Global Health Check

- This health check was conducted on the behalf of <CUSTOMER>
- The metrics below are for 1 week

## What is this health-check about?
The purpose of this Health Check is to ensure that **<CUSTOMER>** are deploying & using Datadog in the most optimal way, they are also used to identify areas for improvement or where further support may be needed in terms of best practices and guidance.

## Top Action Items - From Healthcheck & Existing Goals

Product | Component
------|------
Tags|Infrastructure host tag (env, team)
Datadog Teams | Creating team in Datadog and populating notification details 
Datadog Role Restrictions | Admin (Platform), Standard (Infra), Read-Only (NOC Monitoring), Limited Read Only (Vendor/SI)
Monitors | Priority tagging for monitors based on Severity
Monitors | Routing Monitors to the correct team with Notification Rules
Monitors | Configuring Tags & Tags Policies on Monitors
Notification Integration | Microsoft Team's Handle setup for priority and team alerting
Fleet Management Strategy | Upgrading Datadog Agent with remote configuration enabled
Logs | Meaningful use and exclusion of existing logs piped in
SAML Team Mappings | For mapping [Datadog Team to IDP provided team](https://docs.datadoghq.com/account_management/saml/mapping/#map-saml-attributes-to-teams)
SAML Role Mappings |For mapping[ Datadog Role to IDP provided role](https://docs.datadoghq.com/account_management/saml/mapping/#map-saml-attributes-to-datadog-roles)

---

> Below you can see some of the metrics and data gathered from your account

---


## Tagging best practices

Below are Datadog's [tagging requirements](https://docs.datadoghq.com/getting_started/tagging/#overview):

1.  Tags must **start with a letter** and after that may contain the characters listed below:
    -   Alphanumerics, Underscores, Minuses, Colons, Periods, Slashes (Other special characters are converted to underscores)
2.  Tags can be **up to 200 characters** long and support Unicode letters

3.  **Tags are converted to lowercase. Therefore, `CamelCase` tags are not recommended.**

4.  A tag can be in the format `value` or `<KEY>:<VALUE>`. Commonly used tag keys are `env`, `instance`, and `name`. The key always precedes the first colon of the global tag definition.
5.  Tags should not originate from [unbounded](https://docs.datadoghq.com/api/latest/metrics/#tag-configuration-cardinality-estimator) sources, such as epoch timestamps, user IDs, or request IDs
6.  Limitations (such as downcasing) only apply to metric tags, not log attributes or span tags.

**Resources**
- [Join an interactive session on effective tagging with Datadog](https://dtdg.co/hc-tagging)

# Infrastructure

**Resources**
- [Join an interactive session to power up your Infrastructure monitoring](https://dtdg.co/hc-infra)

> **Summary (OPTIONAL)**

Component | Value | Score
------|------ | -----
Hosts with an agent ||
Agents with cloud integrations | | 
Agents with `env` tags | | 
Agents with business tags | | 

## Hosts with an agent

**Best Practices** 
- The agent offers more real time telemetry and enables the capability to turn on any integration.

**Resources**
- [Why should I install the Datadog Agent on my cloud instances? ](https://docs.datadoghq.com/agent/guide/why-should-i-install-the-agent-on-my-cloud-instances/#pagetitle)
- Any EC2s or VMs with the Agent installed count as a single instance (no double-billing).

[![https://us3.datadoghq.com/s/e5f1e8ef-6129-11f0-9806-2e69c1c6be5f/tw5-ce9-ed6](https://p.us3.datadoghq.com/s/image/e5f1e8ef-6129-11f0-9806-2e69c1c6be5f/tw5-ce9-ed6.png)](https://us3.datadoghq.com/s/e5f1e8ef-6129-11f0-9806-2e69c1c6be5f/tw5-ce9-ed6)

### Agents with `env` or `team` tags 

**Best Practices** 
- The `env` tag is common through all the products and provide consistency on any search.
- Business tags ensures better ownership of each data object available in the platform
- Example of business tags: `team` `cost_center` `squad` `business_unit` 

**Resources**
- [Best practices for tagging your infrastructure and applications](https://www.datadoghq.com/blog/tagging-best-practices/)
- [Unified Service Tagging](https://docs.datadoghq.com/getting_started/tagging/unified_service_tagging/?tab=kubernetes "https://docs.datadoghq.com/getting_started/tagging/unified_service_tagging/?tab=kubernetes")
You can check if any of the business tags are already being used in the following places:
- [Host Map group by tag](/infrastructure/map?groupby=team)
- [Usage attribution page](/billing/usage-attribution) (only available to admins)

[![https://us3.datadoghq.com/s/e5f1e8ef-6129-11f0-9806-2e69c1c6be5f/kis-uaq-mvg](https://p.us3.datadoghq.com/s/image/e5f1e8ef-6129-11f0-9806-2e69c1c6be5f/kis-uaq-mvg.png)](https://us3.datadoghq.com/s/e5f1e8ef-6129-11f0-9806-2e69c1c6be5f/kis-uaq-mvg)

[![https://us3.datadoghq.com/s/e5f1e8ef-6129-11f0-9806-2e69c1c6be5f/zaz-if2-qkb](https://p.us3.datadoghq.com/s/image/e5f1e8ef-6129-11f0-9806-2e69c1c6be5f/zaz-if2-qkb.png)](https://us3.datadoghq.com/s/e5f1e8ef-6129-11f0-9806-2e69c1c6be5f/zaz-if2-qkb)

# Monitors

Monitoring and alerting is an art that requires defining clear monitoring goals, choose the detection method, monitor at the appropriate level of detail, say what's happening, set the alert conditions either using thresholds or anomalies and notify your teams with actionable alerts to help troubleshoot and recover faster.

**Resources**

* [Monitoring 101: Collecting the right data](https://www.datadoghq.com/blog/monitoring-101-collecting-data/)
* [Monitoring 101: Alerting on what matters](https://www.datadoghq.com/blog/monitoring-101-alerting/)
* [Monitoring 101: Investigating performance issues](https://www.datadoghq.com/blog/monitoring-101-investigation/)
* [Alerting 101: Status checks](https://www.datadoghq.com/blog/alerting-101-status-checks/)
* [Alerting 101: Timeseries metric checks](https://www.datadoghq.com/blog/alerting-101-metric-checks/)
* [Join an interactive session on creating effective monitors and SLOs](https://dtdg.co/hc-monitoring)
* [Monitor Quality](/monitors/suggestions)
* [Monitor Notifications Overview Dashboard](/dash/integration/30532/monitor-notifications-overview)

## Monitors triggering more than 15 times in the past week

**Best Practice** 
- Monitors triggering more than 15 times per week would indicate alert fatigue.
- Review current thresholds and consider using the monitor in Composite with anomaly detection

[![https://us3.datadoghq.com/s/e5f1e8ef-6129-11f0-9806-2e69c1c6be5f/8n4-a7e-sbi](https://p.us3.datadoghq.com/s/image/e5f1e8ef-6129-11f0-9806-2e69c1c6be5f/8n4-a7e-sbi.png)](https://us3.datadoghq.com/s/e5f1e8ef-6129-11f0-9806-2e69c1c6be5f/8n4-a7e-sbi)

[![https://us3.datadoghq.com/s/e5f1e8ef-6129-11f0-9806-2e69c1c6be5f/zjt-p59-sz8](https://p.us3.datadoghq.com/s/image/e5f1e8ef-6129-11f0-9806-2e69c1c6be5f/zjt-p59-sz8.png)](https://us3.datadoghq.com/s/e5f1e8ef-6129-11f0-9806-2e69c1c6be5f/zjt-p59-sz8)

# Log Management

**Resources:**
- [Logging Without Limits](https://docs.datadoghq.com/logs/guide/getting-started-lwl/)
- [Log Parsing - Best Practices](https://docs.datadoghq.com/logs/guide/log-parsing-best-practice/)
- [Best Practices for Log Management](https://docs.datadoghq.com/logs/guide/best-practices-for-log-management/)
- [Join an interactive session to optimize your Log Management](https://dtdg.co/hc-logs)

## Overall Exclusion Ratio

[![https://us3.datadoghq.com/s/e5f1e8ef-6129-11f0-9806-2e69c1c6be5f/25n-b3j-c9h](https://p.us3.datadoghq.com/s/image/e5f1e8ef-6129-11f0-9806-2e69c1c6be5f/25n-b3j-c9h.png)](https://us3.datadoghq.com/s/e5f1e8ef-6129-11f0-9806-2e69c1c6be5f/25n-b3j-c9h)

## Indexed logs going through a pipeline 

**Best Practice** 
- Datadog's Log Explorer works best with structured data. Even JSON logs can benefit from categorization and enrichment of data.

**Resources**
- [Log Pipelines](https://docs.datadoghq.com/logs/log_configuration/pipelines/?tab=source) 
- [Unparsed Logs ingested](/logs?query=datadog.pipelines%3Afalse&cols=host%2Cservice%2Csource)

[![https://us3.datadoghq.com/s/e5f1e8ef-6129-11f0-9806-2e69c1c6be5f/b2j-d7g-inr](https://p.us3.datadoghq.com/s/image/e5f1e8ef-6129-11f0-9806-2e69c1c6be5f/b2j-d7g-inr.png)](https://us3.datadoghq.com/s/e5f1e8ef-6129-11f0-9806-2e69c1c6be5f/b2j-d7g-inr)

## Log status per index

**Best Practices** 
- DEBUG logs are often only required during troubleshooting time. Index them only when needed.
- Set up [multiple indexes](https://docs.datadoghq.com/logs/guide/best-practices-for-log-management/#set-up-multiple-indexes-for-log-segmentation) if you want to segment your logs for different retention periods or daily quotas, usage monitoring, and billing.

**Resources**
-  [Log Indexes](https://docs.datadoghq.com/logs/log_configuration/indexes/#switch-off-switch-on) 
-  [Indexed debug logs query](/logs?query=status%3Adebug&cols=host%2Cservice&index=&messageDisplay=inline&stream_sort=desc&viz=timeseries)

[![https://us3.datadoghq.com/s/e5f1e8ef-6129-11f0-9806-2e69c1c6be5f/3m3-us3-jsy](https://p.us3.datadoghq.com/s/image/e5f1e8ef-6129-11f0-9806-2e69c1c6be5f/3m3-us3-jsy.png)](https://us3.datadoghq.com/s/e5f1e8ef-6129-11f0-9806-2e69c1c6be5f/3m3-us3-jsy)

## Multi-line index logs

**Best Practice**
- Multi-line logs should be transformed into single line for better analysis and reduce event indexing volume.

**Resources**
-  [Advance log collection - multi-line aggregation](https://docs.datadoghq.com/agent/logs/advanced_log_collection/?tab=configurationfile#multi-line-aggregation) 


**How to find multi-line logs?**

There is no foolproof way to determine in app which of the logs you are sending are multi-line without knowing something about the log pattern, such as what regex determines a new log entry (usually a date/time). Thus, if your logs are not sent in JSON, the onus of determining which lines are multi-line is on those configuring log collection.  

You can use the below widget as a starting point for identifying logs that might benefit from multi-line aggregation. Another mechanism would be to browse your log patterns to see if any patterns identified might be a component of a multi-line log. 

[![https://us3.datadoghq.com/s/e5f1e8ef-6129-11f0-9806-2e69c1c6be5f/3z7-x59-p2h](https://p.us3.datadoghq.com/s/image/e5f1e8ef-6129-11f0-9806-2e69c1c6be5f/3z7-x59-p2h.png)](https://us3.datadoghq.com/s/e5f1e8ef-6129-11f0-9806-2e69c1c6be5f/3z7-x59-p2h)

# Dashboards 

**Best Practices**

-   An attention-grabbing **About** group with a banner image, concise copy, useful links, and good typography hierarchy
-   A brief annotated **Overview** group with the most important statistics at the top
-   Simple graph titles and title-case group names
-   Symmetry in high density mode
-   Well-formatted, concise notes
-   Color coordination between related groups, notes within groups, and graphs within groups
-   Remove unused Dashboards or Lists
-   Leverage Template variables to allow you dynamically filter widgets
-   Utilize Event Overlays to add extra dimensions and context for troubleshooting
-   Revisit Dashboards not been updated/viewed in 90 days to verify if they are relevant

**Resources** 
- [Integration Dashboard](https://docs.datadoghq.com/developers/integrations/create-an-integration-dashboard/)
- [Join an interactive session on better visualizations with Dashboards](https://dtdg.co/hc-dashboarding)
