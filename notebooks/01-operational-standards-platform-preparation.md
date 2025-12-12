---
title: 'Operational Standards: Platform Preparation (1)'
author: Datadog Support
modified: 2025-12-01T06:45:33.183Z
tags: []
metadata:
  type: Documentation
time:
  live_span: 1h
template_variables: []
---


# Platform Preparation

## Platform Preparation Workflow

### Network Egress Strategies

#### Overview

This section outlines the prerequisites and best practices for ingesting telemetry from your environment into the Datadog SaaS platform. Your chosen approach will largely depend on your specific environment and security requirements.

#### Network Egress Overview Diagram

### Firewall Configuration

#### Background

Datadog requires certain domains and ports to be allow-listed in your network’s firewall. See the following [document](https://docs.datadoghq.com/agent/configuration/network/) for a complete list of domains and ports. Traffic is always outbound; Datadog will _never_ initiate traffic into your environment. The open ports [section](https://docs.datadoghq.com/agent/configuration/network/#open-ports) refers to ports the Agent uses to accept traffic, and they should be protected from untrusted traffic.

#### Supported Documentation

* [Network Traffic](https://docs.datadoghq.com/agent/configuration/network/)

#### ⭕ Action Items

| **STATUS**| **TITLE**| **DESCRIPTION**|
|-|-|-|
| Not Started| Submit Firewall Change Request| Submit a request to your Firewall team on an exclusion or allow list for the following ports and paths based on the Datadog Network Document linked above.|

### Proxy Configuration (Optional)

#### Background

By default, the Datadog Agents ship telemetry to Datadog over the open internet. If the infrastructure being monitored cannot reach out to the internet, we support configuring a proxy for this traffic.

#### Recommended Approach

We recommend that you choose a proxy stack that best fits the scale and availability requirements of your environment. While our documentation specifically recommends using HAProxy if traffic will be forwarded from more than 16-20 agents, most enterprise-grade proxies like F5, NGINX or Netscaler will work.

Once deployed, your proxy(s) will communicate with Datadog’s SaaS endpoints via HTTPS. You have the option to use HTTP when sending data to your proxy internally if you trust the traffic in that network. Otherwise, agents can communicate with your proxy via HTTPS. Please note, the additional overhead when using HTTPS is expected due to the nature of establishing connections.

#### Supported Documentation

* [Agent Proxy Configuration](#)

#### ⭕ Action Items

| **STATUS**| **TITLE**| **DESCRIPTION**|
|-|-|-|
| Not Started| Determine Proxy Method and Approach| Pick a proxy technology that meets your organization’s requirements for availability, throughput, and security.|
| Not Started| Submitted Change Request on provisioning a Proxy Server| You should deploy your proxy stack before you start onboarding your agents. This will ensure a more streamlined onboarding experience.|
| Not Started| Configure Proxy Configurations for Agent| Configure the Proxy configuration based on the proxy host created per agent per environment.|

### Credentials

#### Datadog API Keys

#### Background

API keys are used by Datadog agents and integrations to send metrics, logs, and traces into the Datadog platform. Unlike App keys, API keys are tied to an organization, so you can create them outside of a service account without risk of them being revoked when a user account is deleted. They can be created or viewed by any user with the necessary permissions. With this in mind, access to read/write API keys should be limited to a small number of users.

#### Supported Documentation

* [API Key Overview](#)

#### Recommended Approach

For best results, create multiple API keys and assign them to specific areas of your system or organization. This strategy enables you to disable data ingestion from particular components if you encounter high ingestion rates that lead to increased costs in your Datadog account.

Similar to App Keys, API Keys should be created with meaningful names. You may wish to use the following components in your naming convention:

| **COMPONENT**| **GUIDANCE**| **DESCRIPTION**| **EXAMPLES**|
|-|-|-|-|
| Environment| Recommended| The environment where the API key is used| dev, qa, stage, prod|
| Hosting Provider| Recommended| A short alias for a service or platform that you use to run workloads.| aws, azure, on-prem, cloudflare|
| Hosting Account/DataCenter| Recommended| An alias for a cloud account or datacenter.| aws-sandbox-account, azure-lab-subscription, etc|
| Business Unit| Optional: useful for large companies| A part of your business’s organization. Useful for auditing or controlling ingestion from several parts of your organization.| hr, biz-ops, engineering|
| Region| Optional: useful for multi-region environments| The location of where the ingest data is coming from.| us-east-1, us-west-1, etc|
| Cluster| Optional: useful for multi-tenant environments| The cluster where data is coming from. Can be the name of a Kubernetes cluster or vSphere clusters.| my-cluster-name|

Once you have identified the required components for your API key strategy, document the components and naming conventions centrally within your organization. Your documentation should include:

* A table defining the components of your naming convention, along with descriptions, relevance, and sample values.

* A short statement describing your organization's API key naming convention, along with sample API key names and descriptions.

#### Sample API Key Strategy

This API key strategy is ideal for a mid-sized customer monitoring a hybrid cloud environment.

| **COMPONENT**| **DESCRIPTION**| **EXAMPLES**|
|-|-|-|
| Environment| The environment where this API key is used| dev, qa, prod|
| Hosting Provider| Describes the hosting platform where this API key is used| azure, aws, on-prem|
| Hosting Account/DataCenter| Describes the cloud account or datacenter name where this API key is used| shared-services-account, cicd-account, office-dc|

**Naming Convention**:

The following naming convention is required for all API keys created in Datadog. Any key not following this convention will be revoked by the Datadog administration team.

Format: `<hosting-provider>\_<hosting-account-or-dc>\_<environment>`

**Samples**:

* `aws_cicd-account_prod` — API key used to monitor resources deployed to the AWS CI/CD account. This account is part of our production environment.

* `azure_analytics-dev-subscription_dev` — API key used to monitor resources deployed to the Azure Analytics subscription. This subscription is part of our development environment.

* `on-prem_office-dc_dev` — API key used to monitor resources deployed to the development environment in the office datacenter.

#### ✅ Decision Point

Reference your Engagement Project Plan to input your decisions and create your strategy.

#### ⭕ Action Items

| **STATUS**| **TASK**|
|-|-|
| Not Started| Create new Datadog API Keys for the organization account based on the Defined API Key Strategy|
| Not Started| Create the Procurement/Request process for API Keys based on the defined API Key Provisioning Strategy|

### Datadog App Keys

#### Background

App keys provide access to Datadog resources via the programmatic API, such as Dashboards, Monitors, and Service Catalog metadata. App keys are NOT used to send metrics, logs, and APM traces to a Datadog organization.

#### Supported Documentation

* [Application Key Overview](#)

#### Recommended Approach

**Prevent Individuals from Creating Their Own App Keys**

App keys are always tied to a Datadog user, meaning they are revoked when a user is deleted from your Datadog organization. We recommend managing app keys under service accounts for this reason, and we encourage you to prevent individual contributors from creating their own application keys.

**Creating App Keys**

App keys should be created by admins of your Datadog organization and distributed to development teams and automation through secure methods. It is important to use meaningful names when creating app keys that make it clear which service account they were created under and what their intended purpose is.

#### ✅ Decision Point

Reference your Engagement Project Plan to input your decisions and create your strategy.

#### ⭕ Action Items

| **STATUS**| **TASK**|
|-|-|
| Not Started| Create new Datadog App Keys for the organization account based on the Defined App Key Strategy|
| Not Started| Create the Procurement/Request process for App Key based on the defined App Key Provisioning Strategy|
