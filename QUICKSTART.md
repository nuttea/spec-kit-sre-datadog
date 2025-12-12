# SRE Spec Kit - Quick Start Guide

**Simple, command-based approach to SRE maturity assessment and implementation**

---

## 🚀 Getting Started (5 minutes)

### Prerequisites
- ✅ Datadog MCP Server installed and configured
- ✅ Datadog API/App keys with read permissions
- ✅ Claude Code CLI running
- ✅ This repository cloned locally

### Two Ways to Run Commands

This spec kit supports **two command formats** - use whichever you prefer:

#### Option A: Slash Commands (Direct) ⚡
```bash
/assess
```
Fast, explicit commands that execute immediately.

#### Option B: Natural Language (Conversational) 💬
```
Run maturity assessment to determine my current SRE level
```
Conversational prompts that Claude interprets.

**Both work identically!** Examples below show slash commands, but feel free to use natural language.

---

### First Time Setup

**Step 1: Verify Datadog MCP Connection**

**Slash command**:
```bash
# Natural language works too
Tell me about my Datadog organization. Query available hosts and services.
```

*Claude will verify MCP connectivity and show basic org info*

**Step 2: Determine Your Starting Level**

**Slash command**:
```bash
/assess
```

**Natural language**:
```
Run maturity assessment to determine my current SRE level
```

*Claude will execute comprehensive assessment across all 8 dimensions*

**Step 3: View Results and Next Steps**

Your assessment will show:
- Overall maturity level (0-5)
- Scores for each dimension
- Top strengths and critical gaps
- Recommended actions

---

## 📊 Command Categories

All commands are organized by purpose. Simply copy and paste into Claude Code:

| Category | Purpose | When to Use |
|----------|---------|-------------|
| **Assessment** | Determine current maturity level | First time, quarterly reviews |
| **Level 0** | Discovery and planning | New to Datadog or starting fresh |
| **Level 1** | Basic monitoring setup | Have agents, need monitoring |
| **Level 2** | Standardization | Have monitoring, need consistency |
| **Level 3** | Optimization | Have standards, need efficiency |
| **Level 4** | Automation | Have efficiency, need scale |
| **Level 5** | Excellence | Have scale, need innovation |

---

## 🎯 Phase 1: Assessment Commands

### Quick Maturity Check (10 minutes)

**Slash command**:
```bash
/assess
```

**Natural language**:
```
Run quick maturity assessment covering all 8 dimensions
```

---

### Comprehensive Assessment (30 minutes)

**Slash command**:
```bash
/assess-full
```

**Natural language**:
```
Run comprehensive SRE maturity assessment with detailed analysis of:
- Infrastructure coverage
- Tagging compliance
- Service catalog completeness
- Monitoring quality
- Log management efficiency
- Cost optimization
- Incident management
- Advanced capabilities

Generate detailed report with scores and recommendations
```

---

### Gap Analysis

**Slash command**:
```bash
/gap-analysis
```

**Natural language**:
```
Generate gap analysis from current level to target level with:
- Missing capabilities
- Prioritization by impact and effort
- Implementation roadmap
- Timeline estimates
```

---

### Upgrade Plan

**Slash command**:
```bash
/upgrade-plan
```

**Natural language**:
```
Create upgrade plan from my current level to the next level with:
- Prerequisite capabilities
- Implementation steps
- Effort estimates
- Quick wins
- Milestone timeline
```

---

### Generate Report

**Slash command**:
```bash
/generate-report
```

**Natural language**:
```
Generate executive summary of SRE maturity for leadership with:
- Current level and score
- Key strengths
- Top 3 gaps
- Recommended investments
- Expected ROI
```

---

## 📍 Level 0: Foundation Commands

**Purpose**: Discover current state and establish baseline

### Infrastructure Discovery

**Slash command**:
```bash
/level0-infra
```

**What it does**:
- Inventory all hosts with agents
- Identify cloud providers and regions
- List all monitored services
- Calculate agent deployment coverage
- Export results to markdown report

---

### Tagging Audit ⭐ RECOMMENDED FIRST

**Slash command**:
```bash
/level0-tagging
```

**What it does**:
- Analyze tag coverage across all hosts
- Identify missing required tags (env, service, version)
- Find inconsistent tag formats
- Generate tagging compliance report
- Recommend tagging strategy

**Why start here**: Tagging is the foundation for cost attribution, filtering, and Level 3 advancement.

---

### Cost Baseline

**Slash command**:
```bash
/level0-cost
```

**What it does**:
- Query total cloud spend (last 90 days)
- Break down costs by service and team
- Calculate observability cost as % of infrastructure
- Identify top cost drivers
- Create cost baseline report

**Note**: Requires Cloud Cost Management enabled and tagging compliance.

---

### Complete Health Check

**Slash command**:
```bash
/level0-healthcheck
```

**What it does**:
- Complete validation across all Level 0 dimensions
- Infrastructure inventory summary
- Agent deployment coverage
- Tag compliance status
- Current monitoring gaps
- Cost baseline
- Recommended next steps

**Best for**: Comprehensive baseline assessment (combines all Level 0 checks)

---

## 📍 Level 1: Reactive Commands

**Purpose**: Deploy basic monitoring and alerting

### Agent Deployment Validation
```
Run Level 1 agent deployment validation:
1. Check agent coverage (target: 80%+)
2. Verify agents in production environment
3. Validate agent versions
4. Check cloud integration status
5. Generate deployment status report
```

### Monitor Coverage Check
```
Run Level 1 monitor coverage check:
1. Count configured monitors
2. Verify critical service monitors exist
3. Check monitor status (alerting/ok)
4. Identify services without monitors
5. Generate monitor coverage report
```

### Basic Dashboard Creation
```
Help me create Level 1 basic dashboards for:
1. Infrastructure overview (CPU, memory, disk)
2. Service health by environment
3. Log volume by service
4. Active alerts summary

Use Datadog best practice templates
```

### Log Collection Verification
```
Run Level 1 log collection verification:
1. Check logs from production services
2. Verify log sources are tagged properly
3. Measure log ingestion rate
4. Identify services not sending logs
5. Generate log coverage report
```

---

## 📍 Level 2: Proactive Commands

**Purpose**: Standardize tagging and implement SLOs

### Tagging Compliance Check
```
Run Level 2 tagging compliance check (target: 95%):
1. Audit env, service, version tags
2. Check team tag coverage
3. Identify non-compliant resources
4. Generate compliance report
5. Create remediation task list

Export results to maturity-levels/level-2-proactive/tagging-compliance-report.md
```

### SLO Coverage Analysis
```
Run Level 2 SLO coverage analysis:
1. List all critical services
2. Identify services with defined SLOs
3. Calculate SLO coverage percentage (target: 80%)
4. Find services needing SLOs
5. Generate SLO implementation plan
```

### APM Integration Status
```
Run Level 2 APM integration check (target: 70%):
1. List all services in catalog
2. Identify services with APM traces
3. Check trace volume and quality
4. Find services needing instrumentation
5. Generate APM adoption report
```

### Log Pipeline Validation
```
Run Level 2 log pipeline validation:
1. Check pipeline coverage
2. Calculate exclusion ratio (target: 60%+)
3. Identify unparsed logs
4. Analyze optimization opportunities
5. Generate pipeline efficiency report
```

### Service Catalog Completeness
```
Run Level 2 service catalog audit:
1. Verify all services are registered
2. Check ownership assignments
3. Validate metadata completeness
4. Identify missing documentation
5. Generate catalog completeness report
```

---

## 📍 Level 3: Managed Commands

**Purpose**: Optimize costs and implement governance

### Cost Optimization Analysis
```
Run Level 3 cost optimization analysis:
1. Calculate cost per service/team
2. Identify unused or low-traffic services
3. Find log optimization opportunities
4. Analyze metric cardinality issues
5. Generate cost reduction recommendations (target: 20% savings)

Save report to maturity-levels/level-3-managed/cost-optimization-report.md
```

### Governance Scorecard
```
Run Level 3 governance scorecard calculation:
1. Calculate production readiness scores
2. Check compliance with standards
3. Validate team ownership
4. Measure automation coverage
5. Generate governance maturity report
```

### Unused Service Detection
```
Run Level 3 unused service detection:
1. Query services with low traffic (<100 req/day)
2. Identify services with no recent deployments
3. Find zombie dashboards (not viewed in 90d)
4. List monitors with no recent alerts
5. Generate decommissioning candidate list
```

### Production Readiness Check
```
Run Level 3 production readiness check for service: [SERVICE_NAME]

Validate:
1. SLO defined and tracking
2. Monitors configured with proper routing
3. Dashboard exists with key metrics
4. Logs being collected and parsed
5. APM instrumentation active
6. Team ownership assigned
7. Documentation links present

Generate readiness score and recommendations
```

---

## 📍 Level 4: Optimized Commands

**Purpose**: Implement advanced automation

### Workflow Automation Metrics
```
Run Level 4 workflow automation analysis:
1. Query workflow execution counts
2. Calculate auto-remediation percentage (target: 30%)
3. Measure MTTR improvement
4. Identify automation opportunities
5. Generate automation maturity report
```

### RUM Performance Analysis
```
Run Level 4 RUM performance analysis:
1. Query user session metrics
2. Analyze page load performance
3. Check Core Web Vitals compliance
4. Identify slow user journeys
5. Generate UX optimization recommendations
```

### Incident Automation Rate
```
Run Level 4 incident automation analysis:
1. Query incident creation metrics
2. Calculate auto-triage percentage
3. Measure MTTR reduction vs baseline
4. Identify manual incident patterns
5. Generate automation opportunities report
```

### Platform Adoption Metrics
```
Run Level 4 platform adoption analysis:
1. Measure self-service platform usage
2. Track onboarding automation
3. Calculate team adoption rates
4. Identify adoption barriers
5. Generate platform effectiveness report
```

---

## 📍 Level 5: Excellence Commands

**Purpose**: Demonstrate innovation and leadership

### Comprehensive Platform Report
```
Generate Level 5 comprehensive platform report:
1. All maturity dimension scores
2. Innovation metrics
3. Industry benchmark comparison
4. Platform effectiveness KPIs
5. ROI demonstration
6. Recommendations for thought leadership

Export to maturity-levels/level-5-excellence/platform-excellence-report.md
```

### Innovation Tracking
```
Run Level 5 innovation analysis:
1. Count custom integrations
2. Track workflow automation created
3. Measure unique use cases
4. Calculate platform contributions
5. Generate innovation portfolio
```

---

## 🔧 Utility Commands

### Save Assessment Results
```
Save my current assessment results to:
maturity-levels/my-assessment-[DATE].md

Include:
- Overall maturity level
- Dimension scores
- Gap analysis
- Recommended actions
- Timeline estimates
```

### Generate Gap Analysis
```
Generate gap analysis from current level [N] to target level [M]:
1. List missing capabilities
2. Prioritize by impact and effort
3. Create implementation roadmap
4. Estimate timeline
5. Identify dependencies

Export to gap-analysis-level[N]-to-level[M].md
```

### Create Upgrade Plan
```
Create upgrade plan from Level [N] to Level [N+1]:
1. List prerequisite capabilities
2. Define implementation steps
3. Estimate effort for each step
4. Identify quick wins
5. Create milestone timeline

Save to maturity-levels/upgrade-plan-to-level[N+1].md
```

### Export All Queries
```
Export all MCP queries used in assessment to:
assessment-tools/mcp-query-library/executed-queries-[DATE].md

Include query results and timestamps
```

---

## 🎓 Learning Commands

### Explain Maturity Level
```
Explain what Level [N] means:
- Key characteristics
- Core capabilities required
- Success criteria
- Typical timeline
- Common challenges
```

### Show Level Requirements
```
Show detailed requirements for Level [N]:
- Agent coverage target
- Tagging compliance target
- SLO coverage target
- Expected capabilities
- Graduation criteria
```

### Compare Levels
```
Compare Level [N] vs Level [M]:
- Key differences
- Capability gaps
- Effort estimate
- Business value
- Timeline
```

---

## 📋 Report Commands

### Generate Executive Summary
```
Generate executive summary of SRE maturity:
- Current level and score
- Key strengths
- Top 3 gaps
- Recommended investments
- Expected ROI
- Timeline to next level

Format for leadership presentation
```

### Create Quarterly Review
```
Generate quarterly maturity review comparing:
- Current quarter scores
- Previous quarter scores
- Progress toward targets
- Achievements
- Upcoming initiatives

Save to reports/quarterly-review-[QUARTER].md
```

### Export Metrics Dashboard
```
Create metrics dashboard showing:
- Maturity level trend
- Dimension scores over time
- Cost optimization savings
- MTTR reduction
- Automation percentage

Save dashboard definition to Datadog
```

---

## 🆘 Troubleshooting Commands

### Diagnose MCP Connection
```
Diagnose Datadog MCP connection:
1. Test API connectivity
2. Verify permissions
3. Check query execution
4. Show error details
5. Recommend fixes
```

### Validate Query Results
```
Validate query results for [DIMENSION]:
1. Re-run query
2. Compare against expected format
3. Check for anomalies
4. Verify data freshness
5. Explain results
```

### Debug Assessment Failure
```
Debug assessment failure:
1. Show error messages
2. Identify failed queries
3. Check permissions needed
4. Recommend workarounds
5. Create issue report
```

---

## 💡 Best Practices

### Before Running Assessments
1. Ensure Datadog MCP is connected
2. Have API keys with appropriate permissions
3. Allow 10-30 minutes for comprehensive assessments
4. Save results for tracking progress

### During Implementation
1. Start with Level 0 even if you think you're higher
2. Validate each capability before advancing
3. Save all reports for audit trail
4. Use pre-built commands rather than custom queries

### After Assessment
1. Review results with team
2. Prioritize gaps by impact and effort
3. Create concrete action items
4. Schedule quarterly reassessments

---

## 📚 Command Reference

Full command reference: [COMMANDS.md](./COMMANDS.md)
Planning documents: [planning/](./planning/)
Level definitions: [planning/level-definitions.md](./planning/level-definitions.md)

---

## 🚦 Quick Decision Tree

**Not sure where to start?** Choose your scenario:

### 1. "I'm new to this spec kit"
**Run**:
```bash
/assess
```
*Determines your current maturity level and provides next steps*

---

### 2. "I need to fix tagging" (Most common gap)
**Run**:
```bash
/level0-tagging
```
*Identifies tagging compliance issues - the #1 blocker for advancement*

---

### 3. "I want to advance to next level"
**Run**:
```bash
/gap-analysis
/upgrade-plan
```
*Shows what's missing and creates step-by-step roadmap*

---

### 4. "I need a report for leadership"
**Run**:
```bash
/generate-report
```
*Creates executive summary with ROI and recommendations*

---

### 5. "I want to validate my current level"
**Run**:
```bash
/assess-level0  # or /assess-level1, /assess-level2, etc.
```
*Checks if you meet all requirements for a specific level*

---

### 6. "I need to save/share results"
**Run**:
```bash
/save-to-notebook
```
*Saves your assessment or report to Datadog Notebook for team collaboration*

---

## ⏱️ Time Estimates

| Command Type | Duration |
|--------------|----------|
| Quick assessment | 10 minutes |
| Comprehensive assessment | 30 minutes |
| Level-specific check | 15-20 minutes |
| Gap analysis | 10 minutes |
| Report generation | 5 minutes |
| Upgrade plan | 15 minutes |

---

## 🎯 Success Metrics

Track your progress:
- ✅ Assessment completed
- ✅ Current level identified
- ✅ Gaps documented
- ✅ Action plan created
- ✅ Quarterly reviews scheduled
- ✅ Team alignment achieved

---

## 📖 All Available Slash Commands

### Assessment Commands
| Command | Purpose | Time |
|---------|---------|------|
| `/assess` | Quick maturity check | 10 min |
| `/assess-full` | Comprehensive assessment | 30 min |
| `/assess-level0` | Level 0 validation | 15 min |
| `/assess-level1` | Level 1 validation | 15 min |
| `/gap-analysis` | Identify gaps to next level | 10 min |
| `/upgrade-plan` | Generate upgrade roadmap | 15 min |

### Level 0 Commands
| Command | Purpose | Time |
|---------|---------|------|
| `/level0-infra` | Infrastructure inventory | 5 min |
| `/level0-tagging` | Tagging compliance audit | 5 min |
| `/level0-cost` | Cost baseline | 5 min |
| `/level0-healthcheck` | Complete health check | 20 min |

### Level 2+ Commands
| Command | Purpose | Time |
|---------|---------|------|
| `/level2-tagging` | Advanced tagging strategy | 10 min |
| `/level3-cost` | Detailed cost optimization | 15 min |

### Reporting Commands
| Command | Purpose | Time |
|---------|---------|------|
| `/generate-report` | Executive summary | 10 min |
| `/save-to-notebook` | Save to Datadog | 2 min |
| `/assess-to-notebook` | Assessment as notebook | 12 min |
| `/append-to-notebook` | Append to existing notebook | 2 min |
| `/create-starter-notebooks` | Generate 14 templates | 5 min |

### Utility Commands
| Command | Purpose | Time |
|---------|---------|------|
| `/help` | List all commands | instant |

**Total**: 19 slash commands available

For detailed command reference, see [COMMANDS.md](./COMMANDS.md)

---

**Need Help?** Simply ask Claude: *"Show me available commands for [TASK]"*

**Ready to start?** Run `/assess` now!

---

**Last Updated**: 2025-12-12