# Gap Analysis Generator

Generate comprehensive gap analysis between current level and target level.

**Usage:** This command takes your current maturity level and identifies all gaps preventing you from reaching your target level.

**For implementation guidance on each gap**, refer to:
→ [Operational Standards Mapping](../planning/operational-standards-mapping.md) - Shows which operational standards to use for each capability

**Parameters:**
- Current Level: [Detected from assessment or user-specified]
- Target Level: [User-specified or Current + 1]

**Execute Gap Analysis:**

**Step 1: Assess Current State**
Run comprehensive assessment if not recently completed.

**Step 2: Identify Missing Capabilities**

For target level, check each required capability:
- Agent coverage targets
- Tagging compliance requirements
- SLO coverage expectations
- Monitoring standards
- Log management efficiency
- Cost optimization practices
- Incident management maturity
- Advanced feature adoption

**Step 3: Prioritize Gaps**

Categorize each gap:
- **High Priority**: Blocking graduation, high business impact
- **Medium Priority**: Important but not blocking
- **Low Priority**: Nice-to-have, future optimization

For each gap, provide:
- Current state: [Description with metrics]
- Target state: [Description with metrics]
- Gap size: [Quantified difference]
- Business impact: [High/Medium/Low]
- Implementation effort: [Low/Medium/High]
- Dependencies: [Prerequisites]
- Timeline estimate: [Days/weeks]

**Step 4: Create Implementation Roadmap**

Organize gaps into phases:

**Phase 1 - Quick Wins** (0-30 days):
- [Gap 1] - Effort: Low, Impact: High
- [Gap 2] - Effort: Low, Impact: Medium

**Phase 2 - Foundation** (30-60 days):
- [Gap 3] - Effort: Medium, Impact: High
- [Gap 4] - Effort: Medium, Impact: Medium

**Phase 3 - Advanced** (60-90 days):
- [Gap 5] - Effort: High, Impact: Medium
- [Gap 6] - Effort: Medium, Impact: Low

**Step 5: Calculate ROI**

For each gap closure:
- Cost savings potential: $[AMOUNT]
- MTTR improvement: [%]
- Efficiency gain: [METRIC]
- Risk reduction: [DESCRIPTION]

**Deliverable:**

Create gap analysis report and save to:
`maturity-levels/gap-analysis-level[N]-to-level[M]-[DATE].md`

Include:
- Executive summary
- Detailed gap inventory
- Prioritization matrix
- Implementation roadmap with phases
- Resource requirements
- ROI projections
- Risk assessment
- Success metrics

**Report Format:**

```markdown
# Gap Analysis: Level [N] → Level [M]

## Executive Summary
[Current state, target state, overall gap]

## Gap Inventory

### High Priority Gaps
| Gap | Current | Target | Impact | Effort | Timeline |
|-----|---------|--------|--------|--------|----------|
| [Gap 1] | [State] | [State] | High | Medium | 2 weeks |

### Medium Priority Gaps
[Same format]

### Low Priority Gaps
[Same format]

## Implementation Roadmap
[Phased approach]

## Resource Requirements
[Team, tools, budget]

## ROI Analysis
[Cost-benefit breakdown]

## Success Metrics
[How to measure success]
```

**After completing gap analysis:**

Automatically create Datadog Notebook with results:

```
create_datadog_notebook(
    name="Level [CURRENT] to [TARGET] - Gap Analysis - [DATE]",
    type="documentation",
    cells=... # Include full gap analysis markdown
)
```

**Notebook naming format:**
- "Level [N] to Level [M] - Gap Analysis - YYYY-MM-DD"
- Example: "Level 2 to Level 3 - Gap Analysis - 2025-12-12"

Include notebook URL in response for team collaboration and tracking.