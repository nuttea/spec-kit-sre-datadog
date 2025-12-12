---
title: 'Operational Standards: Access Management (2)'
author: Datadog Support
modified: 2025-12-01T06:46:19.251Z
tags: []
metadata:
  type: Documentation
time:
  live_span: 1h
template_variables: []
---


# Access Management

## Access Management Workflow

### Overview

In the strategy described below, we aim to deliver frameworks that enable your teams to onboard Datadog quickly, while providing safeguards to avoid security vulnerabilities and unexpected costs within your Datadog organization.

## RBAC

## Datadog Role Strategy

### Background

Datadog roles are the cornerstone of permission management in your Datadog organization. Users and Service Accounts are assigned multiple roles; these permissions are added together to determine the full permission set for that principal. Due to this behavior, a user cannot “assume” permissions for a single role assigned to them when logging in.

### Supported Documentation

* [Access Control](https://docs.datadoghq.com/account_management/rbac/?tab=datadogapplication)

### Recommended Approach

#### _Do Not Modify Datadog’s OOTB roles_

One important rule when onboarding a Datadog organization is to **avoid editing the Datadog Admin Role, Data Standard Role, and Datadog Read-only Role**. Changing the permissions for these roles can lock you out of administering your account and interfere with Datadog Support’s ability to assist when submitting tickets. Your custom permission model should be implemented via Custom Roles only.

#### _Set a Baseline_

We recommend that you use the permissions in the **Datadog Standard Role** as a starting point for any new custom roles. You should also exclude the following permissions from your organization’s custom roles, along with any other permissions you deem unnecessary:

| **PERMISSION NAME**| **DESCRIPTION**|
|-|-|
| Access Management| User Access Invite|
| API and Application Keys| All permissions|

#### _Creating Roles_

Once we’ve determined our baseline, we can start creating some basic custom roles for Developers and Managers who will use the Datadog platform. Keep in mind that no roles described will include the permissions defined in our baseline exclusions. We recommend creating the following custom roles as a starting point:

| **ROLE NAME**| **ROLE DESCRIPTION**|
|-|-|
| Developer| Role assigned to individual contributors within your development teams, who use Datadog to monitor their systems.|
| Development Manager| Role assigned to managers and leadership of your development teams. This role is essentially a developer role with permission to edit Datadog teams.|

You may decide that additional roles are necessary for the various personas present in your organization. If this is the case, we encourage you to create additional roles as needed.

We strongly recommend defining and provisioning your roles using a modern Infrastructure as Code (IaC) tool, such as Terraform. This will ensure that the standards set forth in this document are enforced via automation.

### ✅ Decision Point

* Reference your [Engagement Project Plan](https://docs.google.com/spreadsheets/d/1ok2QB6lyIshN6KPnzRrerfopiERnqt5-lQ9P8ZvLseA/edit?gid=671465123#gid=671465123) to input your decisions and create your strategy.

### ⭕ Action Items

| **STATUS**| **TASK**|
|-|-|
| Not Started| Create new Datadog Roles for organization account based on the Defined Roles Strategy|
| Not Started| Create the Procurement/Request process for Datadog Roles based on the defined Roles Provisioning Strategy|

## Datadog Teams Setup

### Background

Datadog Teams enables user groups to organize their assets within Datadog and automatically filter their experience to prioritize these assets. Teams also offer role-based access to specific Datadog resources, such as providing editor access to Dashboards and Monitors. Therefore, implementing an effective team strategy can enhance both the efficiency and security of your overall access management.

### Supported Documentation

* [Teams Overview](https://docs.datadoghq.com/account_management/teams/)

* [Team Management](https://docs.datadoghq.com/account_management/teams/manage/)

* [Managing Monitors with Teams](https://www.datadoghq.com/blog/manage-monitors-with-datadog-teams/)

### Recommended Approach

We recommend that you begin by defining your organization's core functional teams and aligning these with the specific observability needs of each team. This will involve identifying key roles, responsibilities, and the specific data each team needs to monitor. Start by consulting with team leads and stakeholders to understand their requirements, then create teams within Datadog that mirror your organizational structure.

1. **Define Team Roles and Responsibilities**

  * Identify key stakeholders within your organization (e.g., Engineering, DevOps, Security, SRE, Application Support, etc.).

  * Determine the observability requirements for each team, including which metrics, logs, and traces are most critical.

  * Assign roles within Datadog, ensuring that each team has appropriate access to the data they need.

2. **Gather Team Details**

  * Members

  * Links

  * Name and Description

  * Avatar and Banner

  * Page Layout

  * Permissions

  * Notifications

3. **Establish Team Permissions**

  * Use Datadog's Role-Based Access Control (RBAC) to assign appropriate permissions to each team.

  * Ensure sensitive data is accessible only to authorized teams while maintaining overall visibility for observability purposes.

4. **Ongoing Management and Iteration**

  * Regularly review and adjust team configurations as your organization evolves.

  * Conduct periodic audits to ensure teams have the necessary access and resources.

#### _Team Suggestions (Optional)_

Below are some potential team names and their primary focus areas for a typical organization using Datadog:

* **Engineering**: Focuses on application performance, code deployment, and overall system health.

* **DevOps**: Monitors CI/CD pipelines, infrastructure health, and automation processes.

* **Security**: Oversees security-related metrics, incident detection, and response.

* **Site Reliability Engineering (SRE)**: Responsible for uptime, system reliability, and service-level objectives (SLOs).

* **Application Support**: Monitors application performance and user experience, focusing on issue resolution.

* **Network Operations (NetOps)**: Tracks network performance, connectivity issues, and traffic analysis.

* **Business Intelligence (BI)**: Analyzes business metrics, KPIs, and user behavior to support decision-making.

### ⭕ Action Items

| **STATUS**| **TASK**|
|-|-|
| Not Started| Create Datadog teams aligning with each focus area in your operation|
| Not Started| Update team details (notification settings, documentation, name, description, avatar, banner, and permissions)|

## Datadog Service Accounts

### Background

You can think of Service Accounts as Datadog users for your automation tools. They provide a stable framework to assign permissions and provision application keys for workloads that need access to Datadog’s programmatic API. Service Accounts are assigned permissions through one or many Datadog Roles. Once created, you can create application keys within the scope of service accounts. These application keys will then be coupled with your Datadog organization, without the risk of being revoked due to Datadog users leaving your organization.

### Supported Documentation

* [Service Accounts](https://docs.datadoghq.com/account_management/org_settings/service_accounts/)

### Recommended Approach

#### _Roles for your Service Accounts_

Service accounts are assigned roles akin to Datadog user accounts to provide access to various Datadog products. Therefore, you should either utilize your existing custom roles with baseline exclusions or create new custom roles for each service account. To keep things simple, we will proceed with our existing custom roles in this implementation.

#### _Creating Service Accounts_

As we begin our implementation, we should create service accounts linked to specific use cases, including agent deployments, automation, and experimentation. These service accounts will be utilized across multiple teams and should be provisioned by a trusted security administrator.

When creating service accounts, an email address is required. We recommend using a group email address that corresponds to the team responsible for Datadog administration within your organization.

To start, create the service accounts according to the Engagement Project Plan.

### ✅ Decision Point

* Reference your [Engagement Project Plan](https://docs.google.com/spreadsheets/d/1ok2QB6lyIshN6KPnzRrerfopiERnqt5-lQ9P8ZvLseA/edit?gid=671465123#gid=671465123) to input your decisions and create your strategy.

### ⭕ Action Items

| **STATUS**| **TASK**|
|-|-|
| Not Started| Create new Datadog Service Accounts for organization account(s) based on the Defined Service Account Strategy.|
| Not Started| Create the Procurement/Request process for Service Accounts based on the defined Service Account Provisioning Strategy.|

## SSO Configuration & Setup

### 

### 

### Background

Configuring SAML for your Datadog account will let you and all your teammates log in to Datadog using the credentials stored in your organization’s Active Directory, LDAP, or other identity store that has been configured with a SAML Identity Provider. Datadog supports many methods for Single-Sign-On (SSO).

### Supported Documentation

* [SSO Setup Overview](https://docs.datadoghq.com/account_management/saml/)

### Recommended Approach

#### _Setup SSO to Manage Access for Your Organization_

To effectively manage access, we recommend the following SSO setup workflow:

1. **Log In**: Access your Datadog account using your email and password. Ensure you have admin privileges for the following steps.

2. **Configure SAML**:

  * Navigate to **Organization Settings** → **Login Methods** (under Authentication).

  * Select **Configure SAML**.

3. **Download Metadata**: Obtain Datadog’s service provider metadata.

4. **Set Up Your IdP**: Configure the Identity Provider (IdP) of your choice.

5. **Upload IdP Metadata**: In the Datadog UI, upload the metadata from your IdP.

6. **Enable SAML**: Click the **Upload and Enable** button in the Datadog UI to activate SAML authentication.

7. **Self-Updating Metadata**: Configure self-updating Service Provider metadata in your IdP. [Learn more here](https://docs.datadoghq.com/account_management/saml/#self-updating-datadog-sp-metadata).

8. **Role and Team Mappings**: Set up SAML role and team mappings. [Find details here](https://docs.datadoghq.com/account_management/saml/mapping/).

9. **Enable JIT Provisioning**: Activate Just-In-Time (JIT) provisioning to automatically create new user accounts on their first login. [Instructions available here](https://docs.datadoghq.com/account_management/saml/#just-in-time-jit-provisioning). It’s advisable to set the read-only role as the default, allowing SAML mappings to take precedence.

10. **IdP-Initiated Login**: Enable IdP-initiated login to redirect users to your IdP when accessing the Datadog site.

11. **Testing**: Log in as a new test user without an existing Datadog account to verify that everything functions correctly.

12. **Enable Strict SAML**: Once testing is complete, consider enabling strict SAML to restrict logins to your IdP. [More information here](https://docs.datadoghq.com/account_management/saml/#saml-strict).

### ⭕ Action Items

| **STATUS**| **TASK**|
|-|-|
| Not Started| Configure the SSO within your Datadog Organization|
| Not Started| Create the Teams Mappings (SAML Group Mappings)|
| Not Started| Create the Role Mappings (SAML Group Mappings)|
