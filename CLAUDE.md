# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This repository contains a comprehensive set of Datadog operational standards and implementation guides for SRE teams. The documentation is structured as markdown-based notebooks that provide strategic frameworks for deploying and operating Datadog at enterprise scale.

## Document Structure

All documentation is located in the `notebooks/` directory and follows a numbered sequence:

- `00-healthcheck-account-analysis.md` - Initial Datadog account health assessment template
- `01-operational-standards-platform-preparation.md` - Network egress, proxy configuration, API/App key strategies
- `02-operational-standards-access-management.md` - RBAC roles, Datadog Teams setup, permission management
- `03-operational-standards-governance.md` - Compliance strategies (GDPR, HIPAA, FedRAMP, PCI-DSS), agent deployment
- `04-operational-standards-data-monitoring.md` - Log management, indexing strategies, archiving approaches
- `05-operational-standards-data-visualization.md` - Dashboard design patterns, visualization best practices
- `operational-standards-tagging-strategy.md` - Comprehensive tagging framework (reserved tags, integration tags, recommended tags)

## Key Concepts

### Tagging Strategy
The repository emphasizes a strict tagging framework based on Datadog's Unified Service Tagging (UST):
- **Reserved tags**: `env`, `service`, `version`, `source`, `host`, `device`
- **Critical recommended tags**: `team`, `runtime`, `journey`, `role`, `application`
- **Format**: lowercase with underscores (not hyphens or camelCase)
- Tags must not originate from unbounded sources (timestamps, user IDs, request IDs)

### Access Management Hierarchy
1. **Do not modify OOTB roles** (Datadog Admin, Standard, Read-only)
2. **Baseline**: Use Datadog Standard Role as starting point, exclude API key and user invite permissions
3. **Custom roles**: Developer, Development Manager (add more as needed)
4. **Datadog Teams**: Mirror organizational structure for asset organization and RBAC

### Compliance Requirements
Documents outline specific requirements for:
- **PCI-DSS**: US1 site only, HTTPS endpoints, Audit Trail required
- **HIPAA**: BAA required, no Zendesk chat, no log sharing
- **FedRAMP**: GovCloud instance only (Moderate level)
- **GDPR**: EU1 site for data residency

### Log Management Philosophy
- Default "main" index is catch-all (15-day retention)
- Create indexes by log type + environment for granular control
- Use exclusion filters for irrelevant logs (debug, non-critical)
- Archive to external storage (S3, Azure Blob) or use Flex Logs for hybrid approach
- Logs evaluated sequentially through index filters; only one index per log

### Dashboard Design Principles
1. **Monitor/SLO summary at top** for immediate health status
2. **App Overview Dashboard Template** as baseline (clone and customize per application)
3. **Integration-specific widget groups** with context links to core dashboards
4. **Template variables** for dynamic filtering (app, env, integration, service)
5. Dashboards should enable 5-second health assessment with few-click drill-down

## Document Conventions

### Action Item Tables
Documents use standardized tables with STATUS | TITLE | DESCRIPTION or STATUS | TASK columns to track implementation steps.

### Decision Points
Marked with `✅ Decision Point` sections that reference engagement project plans (Google Sheets links in original docs).

### Resource Links
Each section includes "Supported Documentation" with links to official Datadog docs and best practices.

## Working with These Documents

### When Editing
- Maintain the frontmatter YAML structure (title, author, modified, tags, metadata, time, template_variables)
- Preserve the hierarchical heading structure
- Keep action item tables formatted consistently
- Update `modified` date in frontmatter when making changes
- Maintain the placeholder `<CUSTOMER>` in healthcheck template for customer-specific customization

### When Creating New Documents
- Follow the naming convention: `##-operational-standards-<topic>.md`
- Include complete frontmatter with appropriate metadata type (usually "Documentation")
- Structure with clear sections: Background, Supported Documentation, Recommended Approach, Decision Points, Action Items
- Use tables for structured information (strategies, tag definitions, roles)

### Content Patterns
- **Background sections**: Explain the "why" and Datadog's implementation
- **Recommended Approach sections**: Provide prescriptive guidance with sample strategies
- **Best Practices**: Bulleted lists with clear rationale
- **Resources**: Always link to official Datadog documentation

## Special Considerations

### Customer-Specific Information
The healthcheck document (`00-healthcheck-account-analysis.md`) includes:
- Placeholder `<CUSTOMER>` for customer name
- Embedded Datadog dashboard widget images (hosted URLs)
- Pre-formatted queries and links to Datadog UI specific to the US3 site
- Summary tables with empty values to be filled during actual healthcheck

### Compliance Sensitivity
Governance documentation includes regulatory requirements - ensure accuracy when editing compliance-related content as it impacts customer legal obligations.

### API Key Naming Strategy
Documents emphasize meaningful API key naming conventions with components: environment, hosting provider, hosting account/datacenter, optional business unit/region/cluster. Format: `<hosting-provider>_<hosting-account-or-dc>_<environment>`
