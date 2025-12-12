# CLAUDE.md Strategy for SRE Spec Kit

This document defines how CLAUDE.md files will be used throughout the SRE Spec Kit to guide Claude Code in using Datadog MCP effectively for assessments and implementations.

## Purpose of CLAUDE.md Files

Each directory in the spec kit contains a CLAUDE.md file that provides:
1. **Context** - What this directory represents in the maturity framework
2. **Instructions** - How Claude should assist users in this phase
3. **MCP Patterns** - Common Datadog MCP queries for this level
4. **Assessment Guidance** - How to evaluate current state
5. **Implementation Steps** - Recommended actions to progress
6. **Best Practices** - Datadog-specific recommendations

## CLAUDE.md Hierarchy

```
/CLAUDE.md                          # Root: Overall spec kit guidance
├── maturity-levels/CLAUDE.md       # Maturity framework overview
│   ├── level-0-foundation/CLAUDE.md
│   ├── level-1-reactive/CLAUDE.md
│   ├── level-2-proactive/CLAUDE.md
│   ├── level-3-managed/CLAUDE.md
│   ├── level-4-optimized/CLAUDE.md
│   └── level-5-excellence/CLAUDE.md
├── assessment-tools/CLAUDE.md      # Assessment methodology
├── implementation-playbooks/CLAUDE.md # Implementation guidance
└── reference-architectures/CLAUDE.md  # Reference patterns
```

## Root CLAUDE.md (/CLAUDE.md)

**Purpose**: Provides overall guidance for working with the SRE Spec Kit

**Key Sections**:
```markdown
# SRE Spec Kit with Datadog Observability

## Repository Purpose
[Overview of the spec kit and its maturity-based approach]

## How to Use This Repository
1. Start with maturity assessment in level-0-foundation/
2. Use Datadog MCP to query current state
3. Follow implementation guides for current level
4. Progress through maturity levels systematically

## Available Tools
- Datadog MCP: For querying observability data
- Atlassian MCP: For Datadog implementation best practices
- Assessment tools: Automated maturity scoring
- Implementation playbooks: Step-by-step guides

## When User Arrives
1. Understand their goal (assess, implement, optimize)
2. Determine current maturity level
3. Guide them to appropriate directory
4. Execute relevant MCP queries
5. Provide actionable recommendations

## Key Datadog MCP Tools
[List of primary MCP tools with brief descriptions]
```

## Maturity Level CLAUDE.md Template

Each maturity level directory should contain a CLAUDE.md following this pattern:

```markdown
# Level [N]: [Name] - Claude Guidance

## Level Overview
[Brief description of this maturity level]

**Key Characteristics**:
- Posture: [Reactive/Proactive/Managed/etc.]
- Automation: [Level of automation]
- Ownership: [Centralized/Distributed/etc.]

## When User Arrives at This Level

### Initial Assessment
Execute these MCP queries to understand current state:

'''
# Query 1: [Purpose]
[mcp_tool_name](parameters)

# Query 2: [Purpose]
[mcp_tool_name](parameters)

# Query 3: [Purpose]
[mcp_tool_name](parameters)
'''

### Interpreting Results
- If [condition]: User is ready for this level
- If [condition]: User should complete Level [N-1] first
- If [condition]: User may already be at Level [N+1]

## Core Capabilities Assessment

For each capability in this level:

### Capability: [Name]
**Criteria**: [Success criteria]
**MCP Query**:
'''
[specific query with parameters]
'''
**Expected Result**: [What good looks like]
**If Below Threshold**: [Remediation steps]
**If Above Threshold**: [Optimization opportunities]

## Implementation Guidance

### Prerequisites from Previous Level
- [ ] [Capability from Level N-1]
- [ ] [Capability from Level N-1]
- [ ] [Capability from Level N-1]

### Step-by-Step Implementation
1. **[Step Name]**
   - Action: [What to do]
   - MCP Validation: [How to verify]
   - Success Criteria: [What success looks like]
   - Common Issues: [Known problems and solutions]

2. **[Step Name]**
   [Same structure]

## Common MCP Query Patterns for This Level

### Pattern: [Pattern Name]
**Use Case**: [When to use this]
**Query**:
'''python
# Example with explanation
mcp__datadog-mcp__search_datadog_[resource](
    query="[example query]",
    from="now-[timeframe]"
)
'''
**Interpreting Results**: [How to read the output]

## Graduation Criteria to Next Level

Before advancing to Level [N+1], validate:
- [ ] [Criterion with MCP validation query]
- [ ] [Criterion with MCP validation query]
- [ ] [Criterion with MCP validation query]

**Graduation Check Command**:
'''
# Run all validation queries
[composite query or script]
'''

## Troubleshooting

### Issue: [Common Problem]
**Symptoms**: [How to recognize]
**MCP Diagnosis**: [Query to confirm]
**Resolution**: [How to fix]

## Best Practices

### Datadog-Specific Recommendations
- [Best practice with rationale]
- [Best practice with rationale]

### Anti-Patterns to Avoid
- ❌ [What not to do and why]
- ❌ [What not to do and why]

## Related Documentation
- [Link to capability docs]
- [Link to implementation guides]
- [Link to templates]

## Reference Queries Library
[Link to mcp-queries/ subdirectory]
```

## Maturity Level-Specific Guidance

### Level 0: Foundation
**Primary Goal**: Discovery and planning
**MCP Focus**:
- Infrastructure inventory
- Current state analysis
- Cost baseline
- Gap identification

**Key Instruction Pattern**:
```
When user enters Level 0:
1. Run infrastructure discovery queries
2. Analyze current coverage gaps
3. Estimate cost baseline
4. Generate healthcheck report
5. Recommend tagging strategy
6. Create implementation roadmap
```

### Level 1: Reactive
**Primary Goal**: Basic monitoring deployment
**MCP Focus**:
- Agent deployment validation
- Monitor coverage check
- Dashboard creation guidance
- Log collection verification

**Key Instruction Pattern**:
```
When user enters Level 1:
1. Validate agent coverage (target: 80%)
2. Check critical monitor creation
3. Verify log collection from key services
4. Ensure basic dashboards exist
5. Validate cloud integration metrics
```

### Level 2: Proactive
**Primary Goal**: Standardization and SLO tracking
**MCP Focus**:
- Tagging compliance audit
- SLO coverage analysis
- APM integration validation
- Log pipeline efficiency

**Key Instruction Pattern**:
```
When user enters Level 2:
1. Audit tagging compliance (target: 95%)
2. Validate SLO coverage (target: 80% of critical services)
3. Check APM instrumentation
4. Analyze log pipeline efficiency
5. Verify service catalog completeness
```

### Level 3: Managed
**Primary Goal**: Optimization and governance
**MCP Focus**:
- Cost optimization queries
- Governance scorecard calculation
- Unused resource detection
- Compliance validation

**Key Instruction Pattern**:
```
When user enters Level 3:
1. Analyze cost by service/team
2. Calculate production readiness scores
3. Identify unused/low-traffic services
4. Validate compliance requirements
5. Check fleet automation coverage
```

### Level 4: Optimized
**Primary Goal**: Advanced automation
**MCP Focus**:
- Workflow automation metrics
- RUM performance analysis
- Incident automation rate
- Self-service platform adoption

**Key Instruction Pattern**:
```
When user enters Level 4:
1. Query workflow execution metrics
2. Analyze RUM user experience data
3. Calculate incident automation percentage
4. Measure platform adoption
5. Track error tracking efficiency
```

### Level 5: Excellence
**Primary Goal**: Innovation and leadership
**MCP Focus**:
- Comprehensive platform metrics
- Cross-org analytics
- Innovation tracking
- Business impact correlation

**Key Instruction Pattern**:
```
When user enters Level 5:
1. Generate comprehensive platform report
2. Analyze innovation metrics
3. Track community contributions
4. Correlate observability to business KPIs
5. Document unique use cases
```

## MCP Query Composition Patterns

### Pattern: Capability Validation
```markdown
## Pattern: Validate [Capability]

'''python
# Step 1: Query current state
result1 = mcp__datadog-mcp__search_[resource](...)

# Step 2: Calculate compliance
total_count = len(result1)
compliant_count = [count matching criteria]
compliance_rate = compliant_count / total_count

# Step 3: Compare to threshold
if compliance_rate >= THRESHOLD:
    status = "✅ Pass"
else:
    status = "❌ Needs Work"

# Step 4: Generate recommendations
if status == "❌ Needs Work":
    [specific remediation steps]
'''
```

### Pattern: Gap Analysis
```markdown
## Pattern: Identify [Gaps]

'''python
# Step 1: Get expected coverage
expected_resources = mcp__datadog-mcp__search_[primary_resource](...)

# Step 2: Get actual coverage
actual_coverage = mcp__datadog-mcp__search_[secondary_resource](...)

# Step 3: Calculate gaps
gaps = [items in expected but not in actual]

# Step 4: Prioritize gaps
high_priority = [filter by criticality]
medium_priority = [filter by impact]
low_priority = [remaining items]

# Step 5: Generate action plan
for gap in high_priority:
    [specific remediation]
'''
```

### Pattern: Trend Analysis
```markdown
## Pattern: Analyze [Metric] Trend

'''python
# Step 1: Get historical data
metrics_7d = get_datadog_metric(
    queries=[...],
    from="now-7d",
    to="now"
)

# Step 2: Get current data
metrics_24h = get_datadog_metric(
    queries=[...],
    from="now-24h",
    to="now"
)

# Step 3: Calculate trend
trend = (current - baseline) / baseline * 100

# Step 4: Interpret
if trend > 10%:
    status = "📈 Improving"
elif trend < -10%:
    status = "📉 Degrading - Investigate"
else:
    status = "➡️ Stable"
'''
```

## Response Format Guidelines

When Claude provides MCP query results, use this format:

```markdown
## Assessment Results: [Capability Name]

### Current State
- **Metric**: [Value from MCP query]
- **Target**: [Expected value for this level]
- **Status**: [✅ Pass | ⚠️ Warning | ❌ Fail]

### Analysis
[Interpretation of results]

### Recommendations
1. [Specific action] - Priority: [High/Medium/Low]
2. [Specific action] - Priority: [High/Medium/Low]

### Next Steps
'''bash
# Execute these commands/queries next
[follow-up actions]
'''

### Related Resources
- [Link to implementation guide]
- [Link to template]
- [Link to best practice doc]
```

## Progressive Disclosure Strategy

Claude should reveal information progressively:

1. **Initial Contact**: High-level overview and simple assessment
2. **After Assessment**: Detailed gap analysis with priorities
3. **During Implementation**: Step-by-step guidance with validation
4. **Post-Implementation**: Optimization opportunities and next level preview

## Context-Aware Assistance

CLAUDE.md files should enable Claude to be context-aware:

```markdown
## Context Detection

### If user mentions "cost"
→ Focus on: cost optimization queries, CCM data, usage attribution
→ Relevant tools: get_datadog_metric(use_cloud_cost=true)

### If user mentions "compliance"
→ Focus on: data residency, retention policies, audit trail
→ Relevant tools: governance validation queries

### If user mentions "performance"
→ Focus on: APM data, RUM insights, synthetic tests
→ Relevant tools: search_datadog_spans, search_datadog_rum_events

### If user mentions "security"
→ Focus on: security signals, vulnerability tracking, compliance
→ Relevant tools: security monitoring queries
```

## Error Handling Guidance

CLAUDE.md should guide Claude on handling common issues:

```markdown
## Common MCP Query Issues

### Issue: "No results returned"
**Possible Causes**:
- Timeframe too narrow
- Query syntax incorrect
- Resource doesn't exist yet
- Permissions insufficient

**Resolution Steps**:
1. Expand timeframe: from="now-7d" → from="now-30d"
2. Simplify query: Try wildcard "*"
3. Verify resource exists with broader search
4. Check API key permissions

### Issue: "Too many results"
**Resolution**:
- Add filters to narrow scope
- Use start_at for pagination
- Increase max_tokens if truncated
- Focus on critical resources first

### Issue: "Query timeout"
**Resolution**:
- Reduce timeframe
- Add more specific filters
- Split into smaller queries
- Use indexes parameter for logs
```

## Success Metrics for CLAUDE.md Effectiveness

A well-designed CLAUDE.md should enable:
- ✅ User can assess maturity level in <30 minutes
- ✅ Claude provides actionable recommendations (not generic advice)
- ✅ MCP queries execute successfully 95%+ of the time
- ✅ User knows exactly what to do next
- ✅ Progress is measurable and visible
- ✅ Documentation is self-service

## Maintenance Guidelines

CLAUDE.md files should be updated when:
- New Datadog MCP tools become available
- Maturity criteria evolve
- Common user questions emerge
- Best practices change
- New compliance requirements added

---

**Note**: This strategy ensures Claude Code can provide intelligent, context-aware guidance at every stage of the SRE maturity journey using Datadog MCP as the objective assessment mechanism.