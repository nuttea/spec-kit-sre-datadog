# SRE Spec Kit - Slash Command Reference

Complete reference for all available Claude Code slash commands in this repository.

---

## 🎯 Quick Reference

| Command | Purpose | Duration |
|---------|---------|----------|
| `/assess` | Quick maturity assessment | 10 min |
| `/assess-full` | Comprehensive assessment | 30 min |
| `/assess-to-notebook` | Assessment + save to Datadog Notebook | 12 min |
| `/assess-level[N]` | Specific level assessment | 15 min |
| `/level[N]-[task]` | Execute specific task | 10-20 min |
| `/gap-analysis` | Identify gaps to next level | 10 min |
| `/upgrade-plan` | Create upgrade roadmap | 15 min |
| `/generate-report` | Executive summary | 5 min |
| `/create-starter-notebooks` | Generate 14 notebook templates | 2 min |
| `/save-to-notebook` | Save any report to Datadog Notebook | 3 min |
| `/append-to-notebook` | Add to existing notebook | 2 min |

---

## 📊 Assessment Commands

### `/assess`
**Quick SRE Maturity Assessment**

Runs 10-minute quick assessment covering all 8 dimensions.

**Output:**
- Overall maturity level (0-5)
- Dimension scores (0-100)
- Top 3 strengths
- Top 3 gaps
- Recommended next steps

**When to use:** First time assessment, monthly check-ins

---

### `/assess-full`
**Comprehensive SRE Maturity Assessment**

Runs 30-minute comprehensive assessment with detailed analysis.

**Output:**
- Detailed dimensional analysis
- Prioritized gap analysis
- Actionable recommendations
- Upgrade path to next level
- Cost-benefit analysis
- Saved report in `maturity-levels/assessment-reports/`

**When to use:** Quarterly reviews, executive reporting, initial discovery

---

### `/assess-level0`
**Level 0: Foundation Assessment**

Assesses readiness for Level 0 (Discovery & Planning).

**Checks:**
- Infrastructure inventory completeness
- Cost baseline establishment
- Tagging strategy planning
- Team structure documentation

**Output:**
- Level 0 readiness score
- Completed vs missing items
- Recommended actions
- Time to completion

**When to use:** Starting SRE maturity journey

---

### `/assess-level1`
**Level 1: Reactive Assessment**

Assesses readiness for Level 1 (Initial Implementation).

**Checks:**
- Agent deployment (target: ≥80%)
- Monitor coverage (target: ≥5 critical monitors)
- Dashboard creation (target: core dashboards)
- Log collection (target: production logging)
- Incident tracking process

**Output:**
- Level 1 compliance percentage
- Pass/fail for each capability
- Gaps preventing Level 2 graduation
- Remediation steps

**When to use:** Validating basic monitoring deployment

---

## 📍 Level 0: Foundation Commands

### `/level0-infra`
**Infrastructure Discovery**

Complete infrastructure inventory and service discovery.

**Executes:**
- Query all monitored hosts
- Analyze cloud provider distribution
- Environment breakdown
- Calculate agent coverage
- Service discovery

**Output:**
- Infrastructure inventory report
- Coverage statistics
- Identified monitoring gaps
- Saved to `maturity-levels/level-0-foundation/infrastructure-inventory.md`

**When to use:** Initial discovery, quarterly infrastructure reviews

---

### `/level0-tagging`
**Tagging Audit**

Comprehensive audit of current tagging practices.

**Executes:**
- Query all hosts with tags
- Analyze required tag coverage (env, service, version, team)
- Identify tag format issues
- Service-level tagging check

**Output:**
- Tag compliance rates
- Identified format issues
- Recommended tagging standard
- Saved to `maturity-levels/level-0-foundation/tagging-audit-report.md`

**When to use:** Planning tagging strategy, compliance audits

---

### `/level0-cost`
**Cost Baseline**

Establish observability cost baseline.

**Executes:**
- Query total cloud spend (90 days)
- Cost breakdown by service/team/environment
- Identify top cost drivers
- Calculate key metrics

**Output:**
- Cost baseline report
- Spending trends
- Top cost drivers
- Optimization opportunities
- Saved to `maturity-levels/level-0-foundation/cost-baseline-report.md`

**When to use:** Initial cost assessment, budget planning

---

### `/level0-healthcheck`
**Generate Health Check Report**

Comprehensive Level 0 health check combining all discoveries.

**Executes:**
- All Level 0 discovery tasks
- Compile comprehensive report
- Executive summary
- Recommendations

**Output:**
- Complete health check report
- Infrastructure overview
- Tagging assessment
- Cost baseline
- Action items
- Saved to `maturity-levels/level-0-foundation/healthcheck-report-[DATE].md`

**When to use:** Completing Level 0 assessment, leadership reporting

---

## 📍 Level 2: Proactive Commands

### `/level2-tagging`
**Tagging Compliance Check**

Comprehensive tagging compliance validation for Level 2.

**Target:** ≥95% UST compliance

**Executes:**
- Query all resources with tags
- Calculate UST compliance (env, service, version)
- Check recommended tags (team, application)
- Validate tag quality
- Identify non-compliant resources

**Output:**
- Compliance percentage
- Non-compliant resource list
- Remediation roadmap
- Saved to `maturity-levels/level-2-proactive/tagging-compliance-report-[DATE].md`

**When to use:** Validating Level 2 tagging standards, quarterly compliance checks

---

## 📍 Level 3: Managed Commands

### `/level3-cost`
**Cost Optimization Analysis**

Comprehensive cost optimization for Level 3.

**Target:** 20%+ cost reduction from baseline

**Executes:**
- Query current costs by service/team
- Identify unused/idle services
- Analyze log optimization opportunities
- Check metric cardinality
- Calculate potential savings

**Output:**
- Current cost breakdown
- Optimization opportunities with savings
- Prioritization matrix
- Implementation roadmap
- Cost governance recommendations
- Saved to `maturity-levels/level-3-managed/cost-optimization-report-[DATE].md`

**When to use:** Cost optimization initiatives, quarterly FinOps reviews

---

## 🔧 Utility Commands

### `/gap-analysis`
**Gap Analysis Generator**

Identifies gaps between current and target maturity level.

**Executes:**
- Assess current state
- Identify missing capabilities for target level
- Prioritize gaps (High/Medium/Low)
- Create implementation roadmap
- Calculate ROI

**Output:**
- Comprehensive gap inventory
- Prioritization matrix
- Phased implementation roadmap
- Resource requirements
- Saved to `maturity-levels/gap-analysis-level[N]-to-level[M]-[DATE].md`

**When to use:** Planning upgrades, resource allocation, quarterly planning

---

### `/upgrade-plan`
**Upgrade Plan Generator**

Step-by-step plan from current level to next level.

**Executes:**
- Validate current level
- Identify target requirements
- Create implementation steps
- Define milestones
- Risk assessment

**Output:**
- Detailed implementation steps
- Milestone schedule
- Resource allocation
- Validation queries
- Risk mitigation
- Saved to `maturity-levels/upgrade-plan-level[N]-to-level[N+1]-[DATE].md`

**When to use:** Starting level upgrade, sprint planning

---

### `/generate-report`
**Executive Report Generator**

Executive-level maturity report for leadership.

**Executes:**
- Compile all assessment data
- Create business-focused summary
- Calculate ROI projections
- Industry comparisons

**Output:**
- Executive summary (1 page)
- Maturity scorecard
- Business impact analysis
- Competitive positioning
- Roadmap and resource requirements
- Multiple formats: full report, one-pager, slide outline
- Saved to `reports/executive-report-[DATE].md`

**When to use:** Leadership presentations, quarterly business reviews, budget justification

---

### `/create-starter-notebooks`
**Create Starter Notebook Templates**

Generate comprehensive notebook templates for common SRE workflows.

**Executes:**
- Create `notebooks/` directory structure
- Generate 14+ starter templates
- Include pre-filled Datadog MCP queries
- Add checklists and best practices

**Template Categories:**
- **Assessments** (3): Weekly, quarterly, level-readiness
- **Investigations** (3): Performance, error spikes, cost anomalies
- **Postmortems** (2): Incident analysis, outage reports
- **Runbooks** (3): Service onboarding, alert response, cost optimization
- **Reports** (3): Executive, monthly metrics, team health

**Output:**
- Complete `notebooks/` directory
- 14 markdown templates ready to use
- Template index with descriptions
- Integration guide for Datadog Notebooks

**Template Features:**
- Pre-filled MCP queries
- Checklists and workflows
- Decision frameworks
- Variable substitution
- Git-friendly markdown format

**When to use:**
- Initial repository setup
- Establishing team standards
- Creating consistent documentation practices
- Onboarding new team members

---

## 📓 Notebook Integration Commands

### `/assess-to-notebook`
**Quick Assessment with Notebook**

Run quick assessment and automatically save results to a Datadog Notebook for sharing and tracking.

**Executes:**
- Complete assessment (all 8 dimensions)
- Create Datadog Notebook with:
  - Executive summary with scores
  - Infrastructure metrics graphs
  - Log efficiency analysis
  - APM coverage metrics
  - Gap analysis and recommendations
  - Historical tracking

**Output:**
- Console: Quick summary with maturity level
- Notebook: Full report with visualizations
- Link to Datadog Notebook URL

**Notebook Details:**
- Type: "report"
- Auto-named: "SRE Maturity Assessment - [DATE]"
- Snapshots enabled for point-in-time capture
- 7-day context for metric graphs

**When to use:**
- Monthly assessments for team sharing
- Executive reporting with visual data
- Progress tracking over time
- Cross-team collaboration

---

### `/save-to-notebook`
**Save Report to Notebook**

Utility to save any report or findings to a Datadog Notebook.

**Parameters:**
- Report type: assessment, investigation, incident-postmortem, cost-analysis, gap-analysis
- Title: Custom notebook title (or auto-generate)
- Include graphs: Add relevant metrics visualizations
- Time range: 1h, 4h, 1d, 7d, 30d

**Notebook Structure:**
1. Header (markdown): Title, date, metadata
2. Summary (markdown): Key findings and scores
3. Metrics (optional): Type-specific visualizations
4. Details (markdown): Full analysis with tables
5. Recommendations (markdown): Action items
6. Footer (markdown): Generated by SRE Spec Kit

**Type Mapping:**
- `assessment` → "report"
- `investigation` → "investigation"
- `incident-postmortem` → "postmortem"
- `cost-analysis` → "documentation"
- `gap-analysis` → "runbook"

**When to use:**
- After any major analysis
- When findings need to be shared
- For documentation purposes
- Creating searchable records in Datadog

---

### `/append-to-notebook`
**Append to Existing Notebook**

Add new findings to an existing Datadog Notebook.

**Use Cases:**
- Weekly assessment updates for progression tracking
- Real-time investigation documentation
- Cost optimization results over time
- Remediation updates to incident postmortems

**Required:**
- Notebook ID (from URL or previous command)
- Content type (markdown, metric-graph, log-query)
- Section title
- Content to append

**How to Find Notebook ID:**
- From previous command output
- From Datadog URL: `https://app.datadoghq.com/notebook/<ID>`
- Run `search_datadog_notebooks` by name

**Operations:**
- APPENDS content (doesn't replace)
- Preserves existing cells
- Maintains chronological order
- Cannot remove cells (use UI for deletions)

**When to use:**
- Ongoing investigations
- Weekly/monthly progress updates
- Multi-phase projects
- Continuous improvement tracking

---

## 📚 Command Usage Patterns

### Pattern 1: New to SRE Spec Kit
```bash
# Step 1: Quick assessment
/assess

# Step 2: Based on results, run full assessment
/assess-full

# Step 3: Generate gap analysis
/gap-analysis

# Step 4: Create upgrade plan
/upgrade-plan
```

### Pattern 2: Monthly Check-in
```bash
# Quick assessment
/assess

# Compare to previous month
# Review progress on action items
# Update stakeholders
```

### Pattern 3: Quarterly Review
```bash
# Comprehensive assessment
/assess-full

# Generate executive report
/generate-report

# If advancing levels, create upgrade plan
/upgrade-plan
```

### Pattern 4: Starting Level 0
```bash
# Run all Level 0 discovery tasks
/level0-infra
/level0-tagging
/level0-cost

# Generate health check
/level0-healthcheck

# Assess Level 0 completion
/assess-level0
```

### Pattern 5: Validating Level Completion
```bash
# For Level 1
/assess-level1

# For Level 2
/assess-level2
# ... etc
```

---

## 🎓 Command Tips

### Best Practices

1. **Start Simple**
   - Begin with `/assess` for quick overview
   - Progress to `/assess-full` when ready

2. **Regular Cadence**
   - Run `/assess` monthly
   - Run `/assess-full` quarterly
   - Generate reports for stakeholders

3. **Track Progress**
   - All commands save results with timestamps
   - Compare reports over time
   - Demonstrate continuous improvement

4. **Use Level-Specific Commands**
   - Focus on your current level tasks
   - Don't skip levels
   - Validate before advancing

5. **Leverage Reports**
   - Use `/generate-report` for leadership
   - Use `/gap-analysis` for team planning
   - Use `/upgrade-plan` for implementation

### Time Management

| Activity | Command | Recommended Frequency |
|----------|---------|----------------------|
| Quick check | `/assess` | Monthly |
| Deep dive | `/assess-full` | Quarterly |
| Leadership update | `/generate-report` | Quarterly |
| Level validation | `/assess-level[N]` | Before advancing |
| Cost review | `/level3-cost` | Monthly (Level 3+) |
| Tagging audit | `/level2-tagging` | Quarterly (Level 2+) |

---

## 🆘 Troubleshooting

### Command Not Working?

1. **Check Datadog MCP Connection**
   ```
   # Verify connection
   Tell me about my Datadog organization
   ```

2. **Verify Permissions**
   - Ensure API keys have read permissions
   - Check MCP server configuration

3. **Review Command Syntax**
   - Commands are case-sensitive
   - Use exact command names from this doc

4. **Check Prerequisites**
   - Some commands require previous commands
   - Example: `/upgrade-plan` needs `/assess-full` first

### Getting Errors?

- **"No data returned"**: Check timeframe parameters
- **"Permission denied"**: Verify API key permissions
- **"Query timeout"**: Reduce query scope or timeframe
- **"Invalid query"**: Check Datadog MCP documentation

---

## 📖 Additional Resources

- **Quick Start Guide**: [QUICKSTART.md](./QUICKSTART.md)
- **Planning Documents**: [planning/](./planning/)
- **Level Definitions**: [planning/level-definitions.md](./planning/level-definitions.md)
- **MCP Query Patterns**: [planning/mcp-query-patterns.md](./planning/mcp-query-patterns.md)
- **Assessment Methodology**: [planning/assessment-methodology.md](./planning/assessment-methodology.md)

---

## 🔄 Command Development Roadmap

### Available Now ✅
- Assessment commands (all levels)
- Level 0 task commands (complete)
- Level 2 tagging command
- Level 3 cost command
- Utility commands (gap analysis, upgrade plan, reports)
- **Notebook integration commands (NEW)** - Save assessments to Datadog Notebooks

### Coming Soon 🚧
- Level 1 specific task commands
- Level 4 automation commands
- Level 5 excellence commands
- Batch command execution
- Custom report templates

### Future Enhancements 💡
- Interactive command wizard
- Automated scheduling
- Integration with CI/CD
- Real-time dashboards
- Multi-org support

---

**Need help?** Ask Claude: *"Explain the /[command-name] command"* or *"Show me examples of /[command-name]"*

**Last Updated**: 2025-12-12
**Total Commands**: 17 (13 original + 4 notebook/template commands)
