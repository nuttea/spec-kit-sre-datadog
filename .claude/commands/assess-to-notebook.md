# Quick Assessment with Notebook

Run a quick SRE maturity assessment (10 minutes) and save results to a Datadog Notebook for sharing and tracking.

**This command will:**
1. Run full assessment across all 8 dimensions
2. Generate maturity scores and recommendations
3. Create a Datadog Notebook with:
   - Executive summary with scores
   - Key metrics graphs (infrastructure, logs, APM)
   - Gap analysis and recommendations
   - Historical tracking capability

**Execute these Datadog MCP queries:**

**Step 1: Run Assessment**
- Query infrastructure: `search_datadog_hosts` for agent coverage
- Query services: `search_datadog_services` for catalog completeness
- Query monitors: `search_datadog_monitors` for alerting coverage
- Query logs: `analyze_datadog_logs` for efficiency metrics
- Query spans: `search_datadog_spans` for APM adoption
- Query incidents: `search_datadog_incidents` for MTTR

**Step 2: Create Notebook**
Use `create_datadog_notebook` with:
- **Type**: "report" (assessment report)
- **Name**: "SRE Maturity Assessment - {date}"
- **Cells**: Include markdown summary + metric graphs + log analysis
- **Time span**: "7d" for context data
- **Take snapshots**: true (capture current state)

**Notebook Structure:**
1. **Executive Summary** (markdown) - Overall level, scores, status
2. **Infrastructure Graph** (metric) - Host count, agent status over time
3. **Log Efficiency** (logs) - Error rate analysis
4. **APM Coverage** (metric) - Span volume by service
5. **Gap Analysis** (markdown) - Top gaps and recommendations
6. **Action Items** (markdown) - Next steps by priority

**Deliver:**
1. Console output: Quick summary with maturity level
2. Notebook URL: Link to full report in Datadog
3. Tracking ID: Reference for future comparisons

**Output format:** Concise summary + Datadog Notebook link