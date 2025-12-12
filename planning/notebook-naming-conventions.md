# Datadog Notebook Naming Conventions

**Purpose**: Standardized naming for automated Datadog Notebook creation

**Last Updated**: 2025-12-12

---

## Naming Pattern

```
Level [N] - [Level Name] - [Report Type] - YYYY-MM-DD
```

### Components:

1. **Level Number** (`[N]`): 0-5, detected from assessment
2. **Level Name**: Official maturity level name
3. **Report Type**: Type of assessment or report
4. **Date**: ISO format (YYYY-MM-DD)

---

## Level Names Reference

| Level | Name |
|-------|------|
| 0 | Foundation |
| 1 | Standardization |
| 2 | Optimization |
| 3 | Intelligence |
| 4 | Innovation |
| 5 | Excellence |

---

## Notebook Naming by Command

### Assessment Commands

| Command | Notebook Name Format | Example |
|---------|---------------------|----------|
| `/assess` | `Level [N] - [Level Name] - Quick Assessment - YYYY-MM-DD` | `Level 2 - Optimization - Quick Assessment - 2025-12-12` |
| `/assess-full` | `Level [N] - [Level Name] - Comprehensive Assessment - YYYY-MM-DD` | `Level 2 - Optimization - Comprehensive Assessment - 2025-12-12` |
| `/assess-level0` | `Level 0 - Foundation - Validation Report - YYYY-MM-DD` | `Level 0 - Foundation - Validation Report - 2025-12-12` |
| `/assess-level1` | `Level 1 - Standardization - Validation Report - YYYY-MM-DD` | `Level 1 - Standardization - Validation Report - 2025-12-12` |

### Level 0 Commands

| Command | Notebook Name Format | Example |
|---------|---------------------|----------|
| `/level0-infra` | `Level 0 - Foundation - Infrastructure Discovery - YYYY-MM-DD` | `Level 0 - Foundation - Infrastructure Discovery - 2025-12-12` |
| `/level0-tagging` | `Level 0 - Foundation - Tagging Audit - YYYY-MM-DD` | `Level 0 - Foundation - Tagging Audit - 2025-12-12` |
| `/level0-cost` | `Level 0 - Foundation - Cost Baseline - YYYY-MM-DD` | `Level 0 - Foundation - Cost Baseline - 2025-12-12` |
| `/level0-healthcheck` | `Level 0 - Foundation - Health Check - YYYY-MM-DD` | `Level 0 - Foundation - Health Check - 2025-12-12` |

### Level 2+ Commands

| Command | Notebook Name Format | Example |
|---------|---------------------|----------|
| `/level2-tagging` | `Level 2 - Optimization - Advanced Tagging Strategy - YYYY-MM-DD` | `Level 2 - Optimization - Advanced Tagging Strategy - 2025-12-12` |
| `/level3-cost` | `Level 3 - Intelligence - Cost Optimization - YYYY-MM-DD` | `Level 3 - Intelligence - Cost Optimization - 2025-12-12` |

### Analysis Commands

| Command | Notebook Name Format | Example |
|---------|---------------------|----------|
| `/gap-analysis` | `Level [N] to Level [M] - Gap Analysis - YYYY-MM-DD` | `Level 2 to Level 3 - Gap Analysis - 2025-12-12` |
| `/upgrade-plan` | `Level [N] to Level [N+1] - Upgrade Plan - YYYY-MM-DD` | `Level 2 to Level 3 - Upgrade Plan - 2025-12-12` |

### Reporting Commands

| Command | Notebook Name Format | Example |
|---------|---------------------|----------|
| `/generate-report` | `Level [N] - [Level Name] - Executive Report - YYYY-MM-DD` | `Level 2 - Optimization - Executive Report - 2025-12-12` |

---

## Notebook Organization in Datadog

### Recommended Folder Structure

When organizing in Datadog UI, group by:

1. **By Level**:
   ```
   📁 Level 0 - Foundation
      - Infrastructure Discovery - 2025-12-12
      - Tagging Audit - 2025-12-12
      - Cost Baseline - 2025-12-12
   📁 Level 1 - Standardization
   📁 Level 2 - Optimization
      - Quick Assessment - 2025-12-12
      - Gap Analysis - 2025-12-12
   ...
   ```

2. **By Date** (for tracking progress):
   ```
   📁 2025-Q4
      - Level 2 - Quick Assessment - 2025-12-12
      - Level 0 - Tagging Audit - 2025-12-12
   📁 2025-Q1
   ...
   ```

3. **By Report Type** (for leadership):
   ```
   📁 Executive Reports
      - Level 2 - Executive Report - 2025-12-12
   📁 Assessments
   📁 Audits
   ...
   ```

---

## Benefits

### 1. **Searchability**
- Easy to find notebooks by level: search "Level 0"
- Easy to find by type: search "Tagging Audit"
- Easy to find by date: search "2025-12"

### 2. **Chronological Tracking**
- Date suffix enables sorting by time
- Can track maturity progression over time
- Compare assessments month-over-month

### 3. **Team Collaboration**
- Level prefix helps teams find relevant content
- Consistent naming reduces confusion
- Easy to share specific notebooks

### 4. **Automated Workflows**
- Standard naming enables automation
- Can trigger workflows based on notebook name pattern
- Easy to archive old notebooks

---

## Usage in Commands

### In Slash Command Files

Commands include instructions like:

```markdown
**After completing assessment:**

Automatically create Datadog Notebook with results:

\`\`\`
create_datadog_notebook(
    name="Level [DETECTED_LEVEL] - [Level Name] - Assessment - [DATE]",
    type="documentation",
    cells=... # Include full assessment markdown
)
\`\`\`

**Notebook naming format:**
- "Level [N] - [Level Name] - Assessment - YYYY-MM-DD"
- Example: "Level 2 - Optimization - Assessment - 2025-12-12"

Include notebook URL in response for easy sharing.
```

### Dynamic Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `[DETECTED_LEVEL]` | Level number from assessment (0-5) | `2` |
| `[Level Name]` | Corresponding level name | `Optimization` |
| `[CURRENT]` | Current level for comparisons | `2` |
| `[TARGET]` | Target level for comparisons | `3` |
| `[DATE]` | ISO format date (YYYY-MM-DD) | `2025-12-12` |
| `[N]`, `[M]` | Generic level placeholders | `2`, `3` |

---

## Implementation Notes

### For Claude Code

When executing commands that create notebooks:
1. Detect the current maturity level from assessment
2. Map level number to level name using the reference table
3. Format date as YYYY-MM-DD
4. Construct notebook name using the pattern
5. Create notebook with formatted markdown content
6. Return notebook URL to user

### Error Handling

If level cannot be detected:
- Use "Level Unknown" as prefix
- Still include report type and date
- Log warning for manual review

Example: `Level Unknown - Assessment - 2025-12-12`

---

## Examples by Use Case

### Quarterly Reviews
```
Level 2 - Optimization - Q4 Assessment - 2025-12-15
Level 2 - Optimization - Gap Analysis - 2025-12-15
Level 2 - Optimization - Executive Report - 2025-12-15
```

### Level Advancement Campaign
```
Level 0 - Foundation - Tagging Audit - 2025-11-01
Level 0 - Foundation - Tagging Audit - 2025-11-15
Level 0 - Foundation - Tagging Audit - 2025-12-01
Level 1 - Standardization - Validation Report - 2025-12-15
```

### Leadership Reporting
```
Level 2 - Optimization - Executive Report - 2025-10-01
Level 2 - Optimization - Executive Report - 2025-11-01
Level 2 - Optimization - Executive Report - 2025-12-01
Level 3 - Intelligence - Executive Report - 2026-01-01
```

---

## Future Enhancements

### Potential Additions

1. **Team Prefix** (optional):
   - `[Team] - Level [N] - [Report] - [Date]`
   - Example: `Platform-SRE - Level 2 - Assessment - 2025-12-12`

2. **Environment Suffix** (for multi-tenant):
   - `Level [N] - [Report] - [Environment] - [Date]`
   - Example: `Level 2 - Assessment - Production - 2025-12-12`

3. **Version Numbers** (for iterations):
   - `Level [N] - [Report] - [Date] - v[Version]`
   - Example: `Level 2 - Assessment - 2025-12-12 - v2`

---

## Related Documentation

- [Notebook Templates Spec](./notebook-templates-spec.md) - Template content structure
- [Assessment Methodology](./assessment-methodology.md) - Assessment scoring and levels
- [Level Definitions](./level-definitions.md) - Detailed level requirements
- [COMMANDS.md](../COMMANDS.md) - Full command reference

---

**Maintained By**: SRE Platform Team
**Version**: 1.0
**Last Review**: 2025-12-12
