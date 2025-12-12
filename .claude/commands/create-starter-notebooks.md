# Create Starter Notebooks

Generate starter notebook templates in `notebooks/` directory for common SRE observability workflows.

**This command will create:**

## 📁 Directory Structure
```
notebooks/
├── assessments/
│   ├── weekly-assessment-template.md
│   ├── quarterly-review-template.md
│   └── level-readiness-template.md
├── investigations/
│   ├── performance-investigation-template.md
│   ├── error-spike-investigation-template.md
│   └── cost-investigation-template.md
├── postmortems/
│   ├── incident-postmortem-template.md
│   └── outage-analysis-template.md
├── runbooks/
│   ├── service-onboarding-runbook.md
│   ├── alert-response-runbook.md
│   └── cost-optimization-runbook.md
└── reports/
    ├── executive-report-template.md
    ├── monthly-metrics-report.md
    └── team-health-report.md
```

## 📝 Template Types

### 1. Assessment Templates
- **Weekly Assessment**: Quick checkpoint format with scoring
- **Quarterly Review**: Comprehensive assessment with trends
- **Level Readiness**: Specific level validation checklist

### 2. Investigation Templates
- **Performance Investigation**: Latency/throughput analysis workflow
- **Error Spike Investigation**: Error rate root cause analysis
- **Cost Investigation**: Usage and cost anomaly investigation

### 3. Postmortem Templates
- **Incident Postmortem**: 5-whys, timeline, remediation items
- **Outage Analysis**: Customer impact, RCA, prevention measures

### 4. Runbook Templates
- **Service Onboarding**: New service monitoring setup checklist
- **Alert Response**: Triage and resolution procedures
- **Cost Optimization**: Cost reduction implementation guide

### 5. Report Templates
- **Executive Report**: Business-focused metrics and ROI
- **Monthly Metrics**: KPI tracking and trends
- **Team Health**: Team performance and maturity metrics

## 🎯 Each Template Includes

1. **Metadata Section**
   - Title, Date, Owner, Status
   - Related services/teams
   - Priority and severity

2. **Objective Section**
   - Clear goal statement
   - Success criteria
   - Scope definition

3. **Data Collection Section**
   - Required Datadog MCP queries
   - Data sources and time ranges
   - Validation steps

4. **Analysis Framework**
   - Structured analysis sections
   - Decision trees and flowcharts
   - Evaluation criteria

5. **Action Items Section**
   - Prioritized tasks
   - Owners and deadlines
   - Tracking mechanisms

6. **References Section**
   - Links to dashboards
   - Related notebooks
   - Documentation links

## 🔧 Template Features

- **Pre-filled MCP queries**: Ready-to-run Datadog queries
- **Checklists**: Step-by-step workflows
- **Decision frameworks**: Structured analysis guides
- **Best practices**: Embedded guidance and tips
- **Datadog integration**: Links to push to Datadog Notebooks

## 📊 Usage Pattern

```bash
# Step 1: Create starter notebooks
/create-starter-notebooks

# Step 2: Copy relevant template
cp notebooks/investigations/performance-investigation-template.md \
   notebooks/investigations/burger-api-latency-2025-12-12.md

# Step 3: Fill in the template with your data

# Step 4: Save to Datadog Notebook (optional)
/save-to-notebook
```

## 🎨 Template Customization

Templates are markdown files that you can:
- Edit to match your team's workflow
- Add custom sections
- Embed team-specific queries
- Version control in git

## 💡 Integration with Existing Commands

Templates work seamlessly with:
- `/assess` → Use assessment templates
- `/level0-infra` → Use investigation templates
- `/gap-analysis` → Use report templates
- `/save-to-notebook` → Push completed notebooks to Datadog

## 🚀 Deliver

After running this command:
1. Creates `notebooks/` directory structure
2. Generates 15+ starter templates
3. Provides template index with descriptions
4. Ready to use immediately

**Output location:** `notebooks/` directory in repository root