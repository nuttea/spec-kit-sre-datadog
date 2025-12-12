# Quick SRE Maturity Assessment

Run a quick SRE maturity assessment (10 minutes) covering all 8 dimensions:

1. **Infrastructure Coverage** - Agent deployment percentage
2. **Tagging Compliance** - Unified service tagging coverage
3. **Service Catalog** - Service inventory completeness
4. **Monitoring Quality** - Monitor coverage and alert quality
5. **Log Management** - Log pipeline efficiency
6. **Cost Optimization** - Cost tracking and optimization
7. **Incident Management** - MTTR and incident tracking
8. **Advanced Capabilities** - APM, RUM, automation adoption

**Execute these Datadog MCP queries:**

- Query infrastructure: `search_datadog_hosts` for agent coverage
- Query services: `search_datadog_services` for catalog completeness
- Query monitors: `search_datadog_monitors` for alerting coverage
- Query logs: `analyze_datadog_logs` for efficiency metrics
- Query incidents: `search_datadog_incidents` for MTTR

**Deliver:**
1. Overall maturity level (0-5)
2. Score for each dimension (0-100)
3. Status indicators (✅ Pass / ⚠️ Warning / ❌ Fail)
4. Top 3 strengths
5. Top 3 gaps
6. Recommended next steps

**Output format:** Concise summary suitable for quick review.