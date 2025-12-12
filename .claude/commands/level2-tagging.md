# Level 2: Tagging Compliance Check

Execute comprehensive tagging compliance check for Level 2 (Proactive).

**Target:** ≥95% compliance with Unified Service Tagging (env, service, version)

**For detailed tagging implementation guidance**, see:
→ [operational-standards-tagging-strategy.md](../notebooks/operational-standards-tagging-strategy.md) ⭐ **REQUIRED FOR LEVEL 3**

This operational standard provides:
- Complete UST implementation guide
- Tag format enforcement (lowercase, underscores)
- Recommended tags beyond UST (team, runtime, journey, role, application)
- Tag validation in CI/CD pipelines
- Cost attribution tag requirements

**Step 1: Query All Resources with Tags**

**Hosts:**
```
search_datadog_hosts(
    context="Level 2: Comprehensive tagging compliance audit",
    filter="*",
    include_all_tags=True,
    max_tokens=50000
)
```

**Services:**
```
search_datadog_services(
    context="Level 2: Service tagging analysis",
    query="*",
    detailed_output=True,
    max_tokens=30000
)
```

**Step 2: Calculate UST Compliance**

For each resource, check presence of:
- `env` tag (required)
- `service` tag (required)
- `version` tag (required)

**Compliance Formula:**
```
UST Compliance % = (Resources with all 3 tags / Total Resources) × 100

Level 2 Target: ≥95%
```

**Step 3: Check Recommended Tags**

Additional tags for Level 2+:
- `team` tag (ownership)
- `application` tag (grouping)
- `runtime` tag (language/platform)

**Step 4: Validate Tag Quality**

Check for anti-patterns:
- ❌ CamelCase: `env:Production` → should be `env:prod`
- ❌ Inconsistent values: `env:production` vs `env:prod`
- ❌ Unbounded values: timestamps, IDs
- ❌ Special characters: spaces, slashes (except allowed)
- ❌ Too long: >200 characters

**Step 5: Identify Non-Compliant Resources**

Create lists of:
1. Resources missing `env` tag
2. Resources missing `service` tag
3. Resources missing `version` tag
4. Resources with format issues
5. Critical production resources non-compliant

**Prioritization:**
- **P0**: Production resources without tags
- **P1**: Staging resources without tags
- **P2**: Development resources without tags
- **P3**: Tag format improvements

**Step 6: Generate Remediation Plan**

For each non-compliant resource:
- Resource ID: [ID]
- Current tags: [LIST]
- Missing tags: [LIST]
- Recommended action: [DESCRIPTION]
- Owner: [TEAM]
- Priority: [P0/P1/P2/P3]

**Report Structure:**

## Level 2 Tagging Compliance Report

### Executive Summary
- Overall UST Compliance: [%]
- Target: 95%
- Status: [✅ Pass / ❌ Fail]
- Gap to target: [%]

### Compliance Breakdown

**By Tag:**
| Tag | Resources with Tag | Total Resources | Compliance % | Status |
|-----|-------------------|-----------------|--------------|--------|
| env | [N] | [N] | [%] | [✅/❌] |
| service | [N] | [N] | [%] | [✅/❌] |
| version | [N] | [N] | [%] | [✅/❌] |
| team | [N] | [N] | [%] | [INFO] |

**By Environment:**
| Environment | Compliance % | Status |
|-------------|--------------|--------|
| Production | [%] | [✅/❌] |
| Staging | [%] | [✅/❌] |
| Development | [%] | [✅/❌] |

### Non-Compliant Resources

**Critical (Production):** [COUNT]
- [Resource 1] - Missing: [TAGS]
- [Resource 2] - Missing: [TAGS]
- ...

**High Priority (Staging):** [COUNT]
**Medium Priority (Development):** [COUNT]

### Tag Quality Issues

**Format Issues:** [COUNT]
- [Issue description with examples]

**Consistency Issues:** [COUNT]
- [Issue description with examples]

### Remediation Roadmap

**Week 1-2:** Production compliance to 95%
- [ ] Tag [N] production hosts
- [ ] Tag [N] production services
- [ ] Fix [N] format issues

**Week 3-4:** Staging compliance to 95%
- [ ] Tag [N] staging resources

**Week 5-6:** Development compliance to 90%
- [ ] Tag [N] development resources

**Ongoing:** Maintain compliance
- [ ] Implement tag validation in CI/CD
- [ ] Create tagging runbooks
- [ ] Schedule quarterly audits

### Automation Opportunities

1. **CI/CD Integration**: Auto-tag new resources
2. **Validation**: Pre-deployment tag checks
3. **Monitoring**: Alert on untagged resources
4. **Documentation**: Update tagging standards

---

**After completing tagging analysis:**

Automatically create Datadog Notebook with advanced tagging strategy:

```
create_datadog_notebook(
    name="Level 2 - Optimization - Advanced Tagging Strategy - [DATE]",
    type="documentation",
    cells=... # Include tagging compliance report and recommendations
)
```

**Notebook naming format:**
- "Level 2 - Optimization - Advanced Tagging Strategy - YYYY-MM-DD"
- Example: "Level 2 - Optimization - Advanced Tagging Strategy - 2025-12-12"

Return notebook URL for team implementation tracking.

**Validation Query:**
```bash
# Re-run in 30 days to measure improvement
/level2-tagging
```