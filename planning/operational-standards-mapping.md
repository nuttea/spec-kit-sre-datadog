# Operational Standards to Maturity Levels Mapping

**Purpose**: Cross-reference guide showing which operational standards apply to each maturity level

**Created**: 2025-12-12
**Maintained By**: SRE Platform Team

---

## Overview

This document bridges the gap between:
- **Operational Standards** (HOW to implement) - Located in `notebooks/`
- **Maturity Levels** (WHAT to achieve) - Defined in `planning/level-definitions.md`

Use this guide to find detailed implementation instructions for each maturity level requirement.

---

## Complete Mapping Matrix

| Maturity Level | Operational Standards Required | Purpose |
|----------------|-------------------------------|---------|
| **Level 0: Foundation** | Platform Preparation<br>Tagging Strategy<br>Governance (Compliance) | Planning and discovery |
| **Level 1: Standardization** | Platform Preparation<br>Access Management<br>Data Monitoring<br>Data Visualization | Initial deployment |
| **Level 2: Optimization** | Tagging Strategy ⭐<br>Data Monitoring<br>Data Visualization<br>Access Management | Standardization |
| **Level 3: Intelligence** | Governance ⭐<br>Data Monitoring (Advanced)<br>Tagging Strategy<br>Access Management | Optimization & governance |
| **Level 4: Innovation** | Data Visualization (Advanced)<br>Governance | Automation & innovation |
| **Level 5: Excellence** | All Standards (Reference) | Leadership & excellence |

---

## Level 0: Foundation

### Required Operational Standards

#### 1. Platform Preparation
**Document**: [01-operational-standards-platform-preparation.md](../notebooks/01-operational-standards-platform-preparation.md)

**Why needed**:
- Planning Datadog org architecture
- Network egress strategy (proxy, firewall)
- API/App key management
- Site selection (US1, EU1, GovCloud)

**Key sections to review**:
- Network Egress Strategies
- Firewall Configuration
- Proxy Configuration (if needed)
- API Key Naming Strategy

**Supports Level 0 capabilities**:
- ✅ Infrastructure Discovery (need agent connectivity)
- ✅ Platform preparation planning

---

#### 2. Tagging Strategy
**Document**: [operational-standards-tagging-strategy.md](../notebooks/operational-standards-tagging-strategy.md)

**Why needed**:
- Draft tagging standard for org approval
- Understand UST requirements
- Plan tag enforcement

**Key sections to review**:
- Unified Service Tagging (UST) overview
- Reserved tags: env, service, version, source, host, device
- Recommended tags: team, runtime, journey, role, application
- Tag format standards (lowercase, underscores)
- Anti-patterns to avoid

**Supports Level 0 capabilities**:
- ✅ Tagging Audit (understand current vs target state)
- ✅ Tagging Strategy (draft for approval)

---

#### 3. Governance (Compliance Planning)
**Document**: [03-operational-standards-governance.md](../notebooks/03-operational-standards-governance.md)

**Why needed**:
- Identify regulatory requirements
- Plan compliance-specific configurations
- Understand data residency needs

**Key sections to review**:
- Compliance Frameworks:
  - PCI-DSS: US1 site only, HTTPS, Audit Trail
  - HIPAA: BAA required, no Zendesk, no log sharing
  - FedRAMP: GovCloud instance required
  - GDPR: EU1 site for data residency
- Agent deployment strategies for compliance

**Supports Level 0 capabilities**:
- ✅ Compliance Requirements identification
- ✅ Planning for regulated environments

---

### Level 0 Assessment Commands

When running these commands, reference operational standards for detailed guidance:

| Command | References | Why |
|---------|-----------|-----|
| `/level0-infra` | Platform Preparation | Agent deployment planning |
| `/level0-tagging` | Tagging Strategy | UST framework and format |
| `/level0-cost` | N/A | Cost baseline only |
| `/level0-healthcheck` | All Level 0 standards | Comprehensive planning |

---

## Level 1: Standardization

### Required Operational Standards

#### 1. Platform Preparation (Deployment)
**Document**: [01-operational-standards-platform-preparation.md](../notebooks/01-operational-standards-platform-preparation.md)

**Why needed**:
- Deploy agents to 80%+ of infrastructure
- Configure proxy if needed
- Validate network connectivity

**Key sections to implement**:
- Agent installation procedures
- Proxy configuration
- Firewall rules validation

**Supports Level 1 capabilities**:
- ✅ Agent Deployment (80%+ coverage)
- ✅ Cloud provider integration

---

#### 2. Access Management (Basic RBAC)
**Document**: [02-operational-standards-access-management.md](../notebooks/02-operational-standards-access-management.md)

**Why needed**:
- Set up basic user access
- Provision teams with appropriate permissions
- Avoid OOTB role modifications

**Key sections to implement**:
- RBAC role hierarchy
- Baseline permissions (Standard role)
- User invitation process

**Supports Level 1 capabilities**:
- ✅ Basic RBAC configured
- ✅ Team members have access

---

#### 3. Data Monitoring (Basic Log Collection)
**Document**: [04-operational-standards-data-monitoring.md](../notebooks/04-operational-standards-data-monitoring.md)

**Why needed**:
- Configure log ingestion
- Use default "main" index
- Understand log flow

**Key sections to implement**:
- Basic log collection setup
- Default index configuration (15-day retention)
- Log source identification

**Supports Level 1 capabilities**:
- ✅ Log Collection from key services
- ✅ Basic log retention

---

#### 4. Data Visualization (Basic Dashboards)
**Document**: [05-operational-standards-data-visualization.md](../notebooks/05-operational-standards-data-visualization.md)

**Why needed**:
- Create infrastructure dashboards
- Set up monitor summary views
- Basic visualization patterns

**Key sections to implement**:
- Infrastructure dashboard templates
- Basic widget configuration
- Monitor summary widgets

**Supports Level 1 capabilities**:
- ✅ Basic Dashboards for infrastructure
- ✅ Service health visibility

---

### Level 1 Assessment Commands

| Command | References | Why |
|---------|-----------|-----|
| `/assess-level1` | All Level 1 standards | Validate deployment |

---

## Level 2: Optimization

### Required Operational Standards ⭐ MOST CRITICAL LEVEL

#### 1. Tagging Strategy (UST Compliance)
**Document**: [operational-standards-tagging-strategy.md](../notebooks/operational-standards-tagging-strategy.md) ⭐ **REQUIRED**

**Why needed**:
- Achieve 95% UST compliance (env, service, version)
- Implement recommended tags (team, runtime, etc.)
- Enforce tag standards

**Key sections to implement**:
- **CRITICAL**: Unified Service Tagging (UST) implementation
- Tag format enforcement (lowercase, underscores)
- Reserved tags: env, service, version, source, host, device
- Recommended tags: team, runtime, journey, role, application
- Tag validation in CI/CD
- Auto-inheritance from cloud providers

**Supports Level 2 capabilities**:
- ✅ Unified Tagging (95% compliance) - **BLOCKING FOR LEVEL 3**
- ✅ Cost attribution by service/team
- ✅ Filtering and aggregation efficiency

---

#### 2. Data Monitoring (Log Optimization)
**Document**: [04-operational-standards-data-monitoring.md](../notebooks/04-operational-standards-data-monitoring.md) ⭐ **REQUIRED**

**Why needed**:
- Optimize log costs (target: >60% exclusion)
- Create multi-index strategy
- Configure log pipelines

**Key sections to implement**:
- **CRITICAL**: Log Index Strategy
  - Index naming: `{log_type}_{environment}` (e.g., `app_logs_prod`)
  - Default "main" index as catch-all
  - Sequential filter evaluation
- Exclusion Filters (target: 60%+ excluded)
  - Drop debug logs
  - Drop non-critical events
  - Drop health check logs
- Archiving Strategy
  - Archive to S3, Azure Blob, or use Flex Logs
  - Compliance-driven retention periods
- Pipeline Configuration
  - Parsing for structured logs
  - Attribute extraction
  - Log enrichment

**Supports Level 2 capabilities**:
- ✅ Log Management optimization
- ✅ Log exclusion ratio >60%
- ✅ Cost reduction through efficiency

---

#### 3. Data Visualization (Dashboard Maturity)
**Document**: [05-operational-standards-data-visualization.md](../notebooks/05-operational-standards-data-visualization.md) ⭐ **REQUIRED**

**Why needed**:
- Standardize dashboard layouts
- Implement template variables
- Create SLO-driven dashboards

**Key sections to implement**:
- **CRITICAL**: App Overview Dashboard Template
  - Clone and customize per application
  - Monitor/SLO summary at top (5-second health check)
  - Integration-specific widget groups
  - Context links to core dashboards
- Template Variables
  - Standard variables: app, env, integration, service
  - Dynamic filtering across dashboards
- SLO Widgets
  - SLO summary widgets
  - Error budget tracking
  - Burn rate alerts
- Design Patterns
  - Few-click drill-down from summary to detail
  - Consistent layouts across applications

**Supports Level 2 capabilities**:
- ✅ Dashboard Maturity
- ✅ Template variables usage
- ✅ SLO widget integration
- ✅ Standardized layouts

---

#### 4. Access Management (Datadog Teams)
**Document**: [02-operational-standards-access-management.md](../notebooks/02-operational-standards-access-management.md) ⭐ **REQUIRED**

**Why needed**:
- Implement team-based RBAC
- Set up Datadog Teams
- Control asset access by team

**Key sections to implement**:
- **CRITICAL**: Datadog Teams Setup
  - Mirror organizational structure
  - Team-based asset organization
  - Team-based permissions
- Custom Role Creation
  - Developer role (baseline permissions + monitor create)
  - Development Manager role (+ team management)
- RBAC Hierarchy
  - Do NOT modify OOTB roles
  - Baseline: Datadog Standard - API keys - user invites
  - Progressive permission grants

**Supports Level 2 capabilities**:
- ✅ Team-Based RBAC
- ✅ Service catalog with ownership
- ✅ Asset organization by team

---

### Level 2 Assessment Commands

| Command | References | Why |
|---------|-----------|-----|
| `/level2-tagging` | Tagging Strategy | UST compliance validation |
| `/assess-level2` | All Level 2 standards | Full validation |

---

## Level 3: Intelligence

### Required Operational Standards

#### 1. Governance & Compliance (Automation)
**Document**: [03-operational-standards-governance.md](../notebooks/03-operational-standards-governance.md) ⭐ **REQUIRED**

**Why needed**:
- Implement governance scorecard
- Automate compliance validation
- Production readiness checks

**Key sections to implement**:
- Production Readiness Framework
- Compliance Automation
  - Automated data residency checks
  - Retention policy enforcement
  - Audit trail validation
- Agent Deployment Strategies
  - Compliance-driven deployment patterns
  - Per-regulation requirements

**Supports Level 3 capabilities**:
- ✅ Governance Scorecard
- ✅ Production readiness automation
- ✅ Compliance automation

---

#### 2. Advanced Log Optimization
**Document**: [04-operational-standards-data-monitoring.md](../notebooks/04-operational-standards-data-monitoring.md)

**Why needed**:
- Advanced cost optimization
- Multi-index mastery
- Archive strategies

**Key sections to implement**:
- Multi-index strategies
- Advanced exclusion filters
- Archive rehydration workflows
- Flex Logs hybrid approach
- Log-based metrics

**Supports Level 3 capabilities**:
- ✅ Cost Optimization (20% reduction target)
- ✅ Log efficiency >60% exclusion

---

#### 3. Advanced Tagging (Cost Attribution)
**Document**: [operational-standards-tagging-strategy.md](../notebooks/operational-standards-tagging-strategy.md)

**Why needed**:
- Enable cost chargebacks
- Service-level cost tracking
- Team cost attribution

**Key sections to implement**:
- Business tags: cost_center, business_unit
- Cost attribution tags
- Team ownership for chargebacks

**Supports Level 3 capabilities**:
- ✅ Cost Optimization with attribution
- ✅ Team-based cost tracking

---

### Level 3 Assessment Commands

| Command | References | Why |
|---------|-----------|-----|
| `/level3-cost` | Tagging Strategy, Data Monitoring | Cost optimization validation |

---

## Level 4: Innovation & Level 5: Excellence

### Operational Standards as Foundation

**All operational standards remain relevant** but are fully mastered:
- Tagging: 99%+ compliance, continuous governance
- Access: Advanced RBAC patterns, automated provisioning
- Governance: Compliance leadership, industry recognition
- Monitoring: Log excellence, predictive analysis
- Visualization: Dashboard innovation, custom analytics

**Beyond operational standards**:
- Custom ML models for observability
- Proprietary automation frameworks
- Industry-specific patterns
- Thought leadership contributions
- Innovation shared publicly

---

## Operational Standards Documents Reference

### 1. Platform Preparation
**File**: `notebooks/01-operational-standards-platform-preparation.md`

**Topics**:
- Network Egress Strategies
- Firewall Configuration
- Proxy Configuration
- API Key Naming Strategy

**Used in levels**: 0 (planning), 1 (deployment)

---

### 2. Access Management
**File**: `notebooks/02-operational-standards-access-management.md`

**Topics**:
- RBAC Role Hierarchy
- Do Not Modify OOTB Roles
- Baseline: Datadog Standard Role
- Custom Roles: Developer, Development Manager
- Datadog Teams Setup
- Team-Based Permissions

**Used in levels**: 1 (basic), 2 (teams), 3 (advanced), 4-5 (mastery)

---

### 3. Governance
**File**: `notebooks/03-operational-standards-governance.md`

**Topics**:
- Compliance Frameworks:
  - PCI-DSS: US1 site, HTTPS, Audit Trail
  - HIPAA: BAA, no Zendesk chat
  - FedRAMP: GovCloud instance
  - GDPR: EU1 site, data residency
- Agent Deployment by Compliance Need
- Data Retention Requirements
- Production Readiness Framework

**Used in levels**: 0 (planning), 3 (automation), 4-5 (excellence)

---

### 4. Data Monitoring
**File**: `notebooks/04-operational-standards-data-monitoring.md`

**Topics**:
- Log Index Strategy
  - Default "main" index (catch-all, 15-day retention)
  - Per-environment indexes: `{log_type}_{env}`
  - Sequential filter evaluation
- Exclusion Filters
  - Target: >60% excluded for cost optimization
  - Debug/trace log filtering
  - Health check log exclusions
- Archiving Strategy
  - S3, Azure Blob, or Flex Logs
  - Rehydration workflows
  - Compliance-driven retention
- Log Pipelines
  - Parsing and attribute extraction
  - Log enrichment
  - Metric generation from logs

**Used in levels**: 1 (basic collection), 2 (optimization), 3 (advanced), 4-5 (excellence)

---

### 5. Data Visualization
**File**: `notebooks/05-operational-standards-data-visualization.md`

**Topics**:
- Dashboard Design Patterns
  - Monitor/SLO summary at top
  - 5-second health check principle
  - Few-click drill-down architecture
- App Overview Dashboard Template
  - Clone and customize per service
  - Integration-specific widget groups
  - Context links to related dashboards
- Template Variables
  - Standard variables: app, env, integration, service
  - Dynamic filtering
  - Consistent UX across dashboards
- SLO Widgets
  - SLO summary
  - Error budget visualization
  - Burn rate alerts

**Used in levels**: 1 (basic), 2 (standardization), 3-4 (advanced), 5 (innovation)

---

### 6. Tagging Strategy
**File**: `notebooks/operational-standards-tagging-strategy.md`

**Topics**:
- Unified Service Tagging (UST)
  - env: Environment (prod, staging, dev)
  - service: Service name (lowercase_with_underscores)
  - version: Deployment version (semantic versioning)
- Reserved Tags (6 total)
  - env, service, version, source, host, device
- Recommended Tags (5+ total)
  - team: Team ownership
  - runtime: Language/platform (nodejs, python, java)
  - journey: User journey/business capability
  - role: Infrastructure role (webserver, database)
  - application: Application grouping
- Tag Format Standards
  - Lowercase only
  - Underscores (not hyphens or camelCase)
  - No spaces, no special characters
  - No unbounded values (timestamps, IDs)
- Implementation Approaches
  - Auto-inheritance from cloud providers
  - Agent configuration (datadog.yaml)
  - Container labels → tags
  - APM environment variables
- Enforcement
  - CI/CD validation
  - Pre-deployment tag checks
  - Automated remediation

**Used in levels**: 0 (planning), 2 (95% compliance), 3 (cost attribution), 4-5 (excellence)

---

## Usage Guide

### For Assessment Commands

When running assessments, consult operational standards to understand gaps:

**Example workflow for Level 2 advancement**:

1. Run `/assess` → Discover you're at Level 1, need Level 2
2. Run `/gap-analysis` → Identifies "Tagging compliance 45%, need 95%"
3. **Consult**: [operational-standards-tagging-strategy.md](../notebooks/operational-standards-tagging-strategy.md)
4. Implement UST tags using guide
5. Run `/level2-tagging` → Validate progress
6. Run `/assess-level2` → Confirm graduation

---

### For Implementation Planning

When planning capability implementation:

**Example: Implementing Level 2 Log Management**

1. **Assessment shows**: "Log exclusion ratio <20%, need >60%"
2. **Consult**: [04-operational-standards-data-monitoring.md](../notebooks/04-operational-standards-data-monitoring.md)
3. **Learn**:
   - How to design indexes by environment
   - How to configure exclusion filters
   - What logs to exclude (debug, trace, health checks)
4. **Implement**: Following the guide's recommendations
5. **Validate**: Re-run assessment to confirm >60% exclusion

---

### For Team Training

Operational standards serve as training materials:

**Level 0 → 1 Training Path**:
1. Read [Platform Preparation](../notebooks/01-operational-standards-platform-preparation.md) - Agent deployment
2. Read [Access Management](../notebooks/02-operational-standards-access-management.md) - RBAC basics
3. Run `/level0-healthcheck` to baseline
4. Implement based on guides
5. Validate with `/assess-level1`

**Level 1 → 2 Training Path**:
1. Read [Tagging Strategy](../notebooks/operational-standards-tagging-strategy.md) - **START HERE**
2. Read [Log Management](../notebooks/04-operational-standards-data-monitoring.md)
3. Read [Dashboard Standards](../notebooks/05-operational-standards-data-visualization.md)
4. Run `/level2-tagging` to audit current state
5. Implement based on guides
6. Validate with `/assess-level2`

---

## Command-Specific References

### Assessment Commands

| Command | Operational Standards to Reference |
|---------|-----------------------------------|
| `/assess` | All standards (for comprehensive understanding) |
| `/assess-full` | All standards (detailed assessment) |
| `/assess-level0` | Platform Prep, Tagging, Governance |
| `/assess-level1` | Platform Prep, Access, Monitoring, Visualization |
| `/gap-analysis` | Standards relevant to target level |
| `/upgrade-plan` | Standards relevant to next level |

### Level 0 Commands

| Command | Operational Standards to Reference |
|---------|-----------------------------------|
| `/level0-infra` | [01-platform-preparation.md](../notebooks/01-operational-standards-platform-preparation.md) |
| `/level0-tagging` | [tagging-strategy.md](../notebooks/operational-standards-tagging-strategy.md) ⭐ |
| `/level0-cost` | N/A (cost baseline only) |
| `/level0-healthcheck` | All Level 0 standards |

### Level 2+ Commands

| Command | Operational Standards to Reference |
|---------|-----------------------------------|
| `/level2-tagging` | [tagging-strategy.md](../notebooks/operational-standards-tagging-strategy.md) ⭐ |
| `/level3-cost` | [tagging-strategy.md](../notebooks/operational-standards-tagging-strategy.md), [04-data-monitoring.md](../notebooks/04-operational-standards-data-monitoring.md) |

### Reporting Commands

| Command | Operational Standards to Reference |
|---------|-----------------------------------|
| `/generate-report` | All standards (for executive context) |

---

## Quick Reference: "Where Do I Find...?"

### "Where do I find tagging requirements?"
→ [operational-standards-tagging-strategy.md](../notebooks/operational-standards-tagging-strategy.md)

### "Where do I find log index strategy?"
→ [04-operational-standards-data-monitoring.md](../notebooks/04-operational-standards-data-monitoring.md)

### "Where do I find RBAC setup?"
→ [02-operational-standards-access-management.md](../notebooks/02-operational-standards-access-management.md)

### "Where do I find compliance requirements?"
→ [03-operational-standards-governance.md](../notebooks/03-operational-standards-governance.md)

### "Where do I find dashboard templates?"
→ [05-operational-standards-data-visualization.md](../notebooks/05-operational-standards-data-visualization.md)

### "Where do I find agent deployment?"
→ [01-operational-standards-platform-preparation.md](../notebooks/01-operational-standards-platform-preparation.md)

---

## Critical Path to Level 3

Most organizations get stuck between Level 1 and Level 2. Here's the critical path:

### Blocker: Tagging Compliance

**Gap**: 45% → 95% UST compliance

**Solution**:
1. **Read**: [operational-standards-tagging-strategy.md](../notebooks/operational-standards-tagging-strategy.md)
2. **Focus on**:
   - Page: "Unified Service Tagging (UST)" section
   - Implement: env, service, version on all resources
   - Validate: Use tag format standards (lowercase, underscores)
3. **Run**: `/level0-tagging` to audit current state
4. **Implement**: Following the guide's recommendations
5. **Validate**: `/level2-tagging` to confirm 95%+

This single operational standard is the **#1 blocker** for Level 2 → Level 3 advancement.

---

## Integration with Assessment Framework

### How It Works Together

```
┌─────────────────────────────────────┐
│  1. Run Assessment                  │
│     /assess or /assess-full         │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│  2. Identify Gaps                   │
│     "Tagging: 45%, need 95%"        │
│     "Log exclusion: 20%, need 60%"  │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│  3. Consult Operational Standards   │
│     → tagging-strategy.md           │
│     → data-monitoring.md            │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│  4. Implement Following Guide       │
│     - Add UST tags (env/svc/ver)    │
│     - Create log exclusion filters  │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│  5. Validate Progress               │
│     /level2-tagging → 90% ✅        │
│     /assess → Level 2 achieved ✅   │
└─────────────────────────────────────┘
```

---

## Maintenance

### Keeping This Mapping Current

When operational standards are updated:
1. Review maturity level mappings
2. Update cross-references if capabilities change
3. Update command references if new standards added
4. Communicate changes to teams

### When to Update

- New operational standard created → Add to relevant levels
- Operational standard deprecated → Remove references
- Maturity level criteria change → Update mappings
- New command created → Add to command reference table

---

## Related Documentation

- [Level Definitions](./level-definitions.md) - Complete maturity framework
- [Assessment Methodology](./assessment-methodology.md) - How assessments work
- [Notebook Naming Conventions](./notebook-naming-conventions.md) - Automated notebook names
- [COMMANDS.md](../COMMANDS.md) - All slash commands
- [QUICKSTART.md](../QUICKSTART.md) - Getting started guide

---

**Last Updated**: 2025-12-12
**Version**: 1.0
**Status**: ✅ Complete interconnected framework
