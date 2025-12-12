# Append to Existing Notebook

Add new findings or updates to an existing Datadog Notebook. Useful for ongoing investigations or tracking progress over time.

**Use cases:**
- Add weekly assessment updates to track maturity progression
- Document investigation steps in real-time
- Append cost optimization results to existing cost reports
- Add remediation updates to incident postmortems

**Required input:**
- **Notebook ID**: The ID of the notebook to update (from previous creation or Datadog URL)
- **Content type**: markdown, metric-graph, log-query
- **Title**: Section title for the new content
- **Content**: The actual content to append

**How to find Notebook ID:**
1. From previous command output
2. From Datadog URL: `https://app.datadoghq.com/notebook/<NOTEBOOK_ID>`
3. Run `search_datadog_notebooks` to find by name

**Example operations:**

**1. Append weekly progress:**
```
Notebook ID: abc-123-xyz
Content: "## Week 2 Update\n**Date**: 2025-12-19\n**Level**: 2 → 2.5\n**Progress**: Fixed 5/7 'No Data' monitors"
```

**2. Add new metric visualization:**
```
Notebook ID: abc-123-xyz
Type: metric
Query: "avg:trace.express.request{service:burger-api}.rollup(avg, 3600)"
Title: "API Latency Improvement"
Time range: last 7 days
```

**3. Document investigation step:**
```
Notebook ID: abc-123-xyz
Content: "### Finding: High Error Rate Root Cause\nAnalyzed logs from burger-api service. Identified database connection pool exhaustion during peak hours (12pm-2pm UTC)."
```

**Execute using:**
`edit_datadog_notebook` with:
- **id**: Target notebook ID
- **cells**: Append new cell(s) to existing cells array

**Important notes:**
- This command APPENDS content (doesn't replace)
- Preserves all existing cells
- Maintains chronological order
- Cannot remove cells (use Datadog UI for deletions)

**Deliver:**
- Confirmation of append
- Updated notebook URL
- Cell count before/after