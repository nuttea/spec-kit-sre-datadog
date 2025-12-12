# Upgrade Plan Generator

Generate step-by-step upgrade plan from current level to next level.

**Purpose:** Create actionable implementation plan with concrete steps, milestones, and validation criteria.

**For implementation details on each step**, refer to:
→ [Operational Standards Mapping](../planning/operational-standards-mapping.md) - Complete guide showing which operational standards to use at each level

**Key operational standards by level**:
- Level 0→1: Platform Preparation, Access Management
- Level 1→2: **Tagging Strategy** (critical!), Data Monitoring, Data Visualization
- Level 2→3: Governance, Advanced Log Optimization
- Level 3→4: Advanced automation (beyond standard guides)

**Step 1: Validate Current Level**
Run assessment to confirm current level and capabilities.

**Step 2: Identify Target Level Requirements**

Review target level graduation criteria:
- Required capabilities
- Success metrics
- Validation methods

**Step 3: Create Implementation Steps**

For each missing capability, define:

**Implementation Step Template:**
```
## Step [N]: [Capability Name]

**Objective:** [What to achieve]
**Current State:** [Where we are]
**Target State:** [Where we need to be]

**Actions:**
1. [Specific action] - Owner: [Role/Team] - Duration: [Time]
2. [Specific action] - Owner: [Role/Team] - Duration: [Time]
3. [Specific action] - Owner: [Role/Team] - Duration: [Time]

**Validation:**
- MCP Query: `[Query to validate completion]`
- Success Criteria: [Measurable outcome]
- Expected Result: [What good looks like]

**Dependencies:**
- Prerequisite: [What must be done first]
- Blockers: [Known issues]

**Resources Required:**
- Team time: [Person-days]
- Tools: [Software/services needed]
- Budget: $[Amount if applicable]
```

**Step 4: Define Milestones**

Create milestone checkpoints:

**Milestone 1** (Week 2):
- [ ] [Capability 1] validated
- [ ] [Capability 2] validated
- MCP Validation: [Query to confirm]

**Milestone 2** (Week 4):
- [ ] [Capability 3] validated
- [ ] [Capability 4] validated
- MCP Validation: [Query to confirm]

**Final Milestone** (Week N):
- [ ] All capabilities validated
- [ ] Graduation criteria met
- [ ] Ready for next level

**Step 5: Risk Assessment**

Identify potential risks:
- Technical risks: [Description + mitigation]
- Resource risks: [Description + mitigation]
- Timeline risks: [Description + mitigation]

**Step 6: Success Metrics**

Define how to measure success:
- Agent coverage: [Current %] → [Target %]
- Tagging compliance: [Current %] → [Target %]
- Cost optimization: $[Current] → $[Target savings]
- MTTR: [Current time] → [Target time]

**Deliverable:**

Create upgrade plan and save to:
`maturity-levels/upgrade-plan-level[N]-to-level[N+1]-[DATE].md`

Include:
- Executive summary with timeline
- Detailed implementation steps
- Milestone schedule
- Resource allocation
- Risk mitigation strategies
- Success metrics and validation queries
- Sign-off checklist

**Quick Actions Section:**
```bash
# Copy these commands to execute each step:

# Step 1: [Task]
/level[N]-[specific-command]

# Step 2: [Task]
/level[N]-[specific-command]

# Validate completion
/assess-level[N+1]
```

**After creating upgrade plan:**

Automatically create Datadog Notebook with roadmap:

```
create_datadog_notebook(
    name="Level [CURRENT] to Level [NEXT] - Upgrade Plan - [DATE]",
    type="runbook",
    cells=... # Include complete upgrade plan with phases and commands
)
```

**Notebook naming format:**
- "Level [N] to Level [N+1] - Upgrade Plan - YYYY-MM-DD"
- Example: "Level 2 to Level 3 - Upgrade Plan - 2025-12-12"

Return notebook URL for team tracking and project management.