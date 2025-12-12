# Level 0: Generate Health Check Report

Generate comprehensive Level 0 health check report combining all discovery findings.

**For detailed implementation guidance**, refer to these operational standards:
- → [01-operational-standards-platform-preparation.md](../notebooks/01-operational-standards-platform-preparation.md) - Network, proxy, API keys
- → [operational-standards-tagging-strategy.md](../notebooks/operational-standards-tagging-strategy.md) - UST framework
- → [03-operational-standards-governance.md](../notebooks/03-operational-standards-governance.md) - Compliance requirements

See also: [Operational Standards Mapping](../planning/operational-standards-mapping.md) for complete Level 0 guidance.

**Task: Create Initial Health Check Report**

**Execute all Level 0 discovery tasks:**

1. **Infrastructure Discovery**
   - Run infrastructure inventory
   - Capture host counts and distribution

2. **Tagging Audit**
   - Run tagging compliance check
   - Capture compliance rates

3. **Cost Baseline**
   - Run cost analysis
   - Capture spending metrics

4. **Coverage Analysis**
   - Calculate monitoring gaps
   - Identify unmonitored resources

**Compile Comprehensive Report:**

## Executive Summary

**Organization**: [Datadog Org Name]
**Assessment Date**: [DATE]
**Assessment Type**: Level 0 - Foundation Health Check
**Overall Readiness**: [%]

## Key Findings

**Strengths:**
1. [Finding 1]
2. [Finding 2]
3. [Finding 3]

**Critical Gaps:**
1. [Gap 1] - Impact: [High/Med/Low]
2. [Gap 2] - Impact: [High/Med/Low]
3. [Gap 3] - Impact: [High/Med/Low]

## Infrastructure Overview

| Metric | Count | Status |
|--------|-------|--------|
| Total Hosts | [N] | - |
| Monitored Hosts | [N] | [%] |
| Cloud Instances | [N] | - |
| Agent Coverage | [%] | [✅/⚠️/❌] |
| Services Discovered | [N] | - |
| Environments | [N] | - |

**Cloud Provider Distribution:**
- AWS: [%]
- Azure: [%]
- GCP: [%]
- On-Premise: [%]

## Tagging Assessment

| Tag | Coverage | Status |
|-----|----------|--------|
| env | [%] | [✅/⚠️/❌] |
| service | [%] | [✅/⚠️/❌] |
| version | [%] | [✅/⚠️/❌] |
| team | [%] | [✅/⚠️/❌] |

**Tag Quality Issues:**
- [Issue 1]
- [Issue 2]
- [Issue 3]

## Cost Baseline

- **Monthly Cloud Spend**: $[AMOUNT]
- **Top Cost Driver**: [Service/Team] - $[AMOUNT]
- **Observability Cost Estimate**: $[AMOUNT] ([%] of infrastructure)

## Monitoring Gaps

**Critical Gaps:**
1. [Gap description] - [N] resources affected
2. [Gap description] - [N] resources affected
3. [Gap description] - [N] resources affected

## Recommendations

**High Priority (Next 30 days):**
1. [Recommendation] - Effort: [Low/Med/High]
2. [Recommendation] - Effort: [Low/Med/High]
3. [Recommendation] - Effort: [Low/Med/High]

**Medium Priority (30-60 days):**
1. [Recommendation]
2. [Recommendation]

**Long Term (60+ days):**
1. [Recommendation]
2. [Recommendation]

## Proposed Tagging Strategy

**Required Tags:**
- `env`: Environment (prod, staging, dev)
- `service`: Service name (lowercase, underscores)
- `version`: Deployment version (semver)

**Recommended Tags:**
- `team`: Owning team
- `application`: Application grouping
- `cost_center`: For cost attribution

**Tag Format Standards:**
- Use lowercase
- Use underscores (not hyphens)
- No timestamps or unbounded values
- Consistent naming across environments

## Next Steps

**To Complete Level 0:**
- [ ] [Action item]
- [ ] [Action item]
- [ ] [Action item]

**Timeline to Level 1:** [Estimated weeks/months]

---

**After completing health check:**

Automatically create Datadog Notebook with comprehensive health check results:

```
create_datadog_notebook(
    name="Level 0 - Foundation - Health Check - [DATE]",
    type="documentation",
    cells=... # Include complete health check report with all sections
)
```

**Notebook naming format:**
- "Level 0 - Foundation - Health Check - YYYY-MM-DD"
- Example: "Level 0 - Foundation - Health Check - 2025-12-12"

Include all report sections:
- Infrastructure summary
- Agent coverage analysis
- Tagging compliance
- Monitoring gaps
- Cost baseline
- Recommendations with action items
- Timeline to Level 1

Return notebook URL for team review and leadership presentation.