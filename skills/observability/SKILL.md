# skill: observability
# purpose: Build dashboards, monitoring, and metrics systems
# triggers: Task type = "observability"

## RPOLES Integration

Observability tasks use the **full RPOLES flow** — these are full feature implementations
with specific focus on data visualization and alerting.

| Phase | Skill | Output |
|-------|-------|--------|
| Review | dev-review | Requirements understood, metrics defined |
| Plan | dev-plan | Dashboard design, data flow planned |
| Outline | dev-outline | Component structure, data models |
| Locate | dev-locate | Existing metrics, visualization patterns |
| Implement | dev-implement | Dashboard, alerts, pipelines |
| Test | dev-test | Data validation, query testing |
| Ship | dev-ship | Deployed dashboard, documentation |

## Phase-Specific Actions

### REVIEW — Understand Observability Requirements

```bash
# 1. Read task requirements
# 2. Identify what needs monitoring
# 3. List key metrics and KPIs
# 4. Define alert thresholds
```

**Key questions:**
- What's being observed? (system, service, metric)
- What are the key metrics? (latency, errors, throughput)
- Who is the audience? (on-call, management, dev team)
- What triggers alerts?

**Output:** Requirements in task file

```markdown
## Observability Requirements

**Target System:** [system name]

**Key Metrics:**
- Metric 1: [definition, units]
- Metric 2: [definition, units]

**Alerts:**
- Alert 1: threshold, conditions

**Audience:** [on-call/dev team/management]
```

### PLAN — Design the Observability Stack

```bash
# 1. Choose visualization tool (Grafana, custom dashboard, etc.)
# 2. Define data sources
# 3. Plan metrics collection
# 4. Design alert rules
```

**Output:** Design in task file

```markdown
## Observability Design

**Visualization:** [Grafana/Custom/Other]

**Data Sources:**
- Source 1: [description]
- Source 2: [description]

**Metrics Collection:**
- Agent/mode: [push/pull]
- Interval: [frequency]
- Retention: [duration]

**Dashboard Layout:**
- Panel 1: [metric, visualization type]
- Panel 2: [metric, visualization type]
```

### OUTLINE — Component Structure

```bash
# 1. Define dashboard configuration files
# 2. Plan alert rules
# 3. Design data pipelines if needed
# 4. Document data models
```

**Output:** Outline in task file

```markdown
## Implementation Outline

**Files to Create:**
| File | Purpose |
|------|---------|
| dashboards/<name>.json | Dashboard config |
| alerts/<name>.yml | Alert rules |
| pipelines/<name>.py | Data processing |
```

### LOCATE — Find Existing Patterns

```bash
# Check existing dashboards
ls ~/claude-workspace/dashboards/
ls ~/claude-workspace/grafana/

# Review existing metrics
grep -r "metric" ~/claude-workspace/ --include="*.py" | head -10

# Check monitoring configs
ls ~/claude-workspace/config/monitoring/
```

**Output:** Existing patterns documented

### IMPLEMENT — Build the Observability Layer

```bash
# 1. Create dashboard configuration
# 2. Define alert rules
# 3. Set up metrics collection
# 4. Test data flows
# 5. Commit incrementally

git add .
git commit -m "[task/NNN] observability: add [component]"
git push
```

**Common artifacts:**
- Grafana dashboard JSON
- Prometheus alert rules `.yml`
- Data collection scripts
- Documentation

### TEST — Validate Data and Queries

```bash
# 1. Verify data is being collected
# 2. Test queries return expected results
# 3. Validate alert conditions fire correctly
# 4. Check dashboard rendering
```

**Output:** Validated dashboard and alerts

### SHIP — Deploy and Document

```bash
# 1. Deploy dashboard configuration
# 2. Enable alert rules
# 3. Document in task file
# 4. Move task to done/
```

## Common Observability Patterns

### Metric Collection
```python
# Example: Metrics collection
from prometheus_client import Counter, Gauge, start_http_server

REQUEST_COUNT = Counter('requests_total', 'Total requests')
REQUEST_LATENCY = Gauge('request_latency_ms', 'Request latency')

def track_request():
    REQUEST_COUNT.inc()
    # track latency...
```

### Alert Rules
```yaml
# Example: Prometheus alert rules
groups:
  - name: critical
    rules:
      - alert: HighErrorRate
        expr: rate(http_requests_total{status="500"}[5m]) > 0.1
        for: 5m
        annotations:
          summary: "High error rate detected"
```

### Dashboard Query
```sql
-- Example: Dashboard query
SELECT
  time_bucket('5m', timestamp) as time,
  avg(latency_ms) as avg_latency
FROM requests
WHERE timestamp > now() - interval '1 hour'
GROUP BY time
ORDER BY time
```

## Artifacts

| Artifact | Location | When |
|---------|---..----|---..---|
| Dashboard config | dashboards/ | Implement |
| Alert rules | alerts/ | Implement |
| Collection scripts | scripts/ | Implement |
| Documentation | docs/ | Ship |

## Checkpoints

```bash
checkpoint --phase review --description "Observability requirements understood" --next "Proceed to design"
checkpoint --phase outline --description "Component structure defined" --next "Proceed to locate"
checkpoint --phase locate --description "Existing patterns identified" --next "Proceed to implement"
checkpoint --phase implement --description "Dashboard and alerts created" --next "Proceed to test"
checkpoint --phase test --description "Data validated, queries tested" --next "Proceed to ship"
checkpoint --phase ship --description "Observability deployed" --next "Task complete"
```

## Success Criteria

- [ ] Metrics collected accurately
- [ ] Dashboard renders correctly
- [ ] Alerts fire on correct conditions
- [ ] Documentation complete
- [ ] Task file complete with Result + Agent Log

---

*Observability is visibility RPOLES. Review→Plan→Outline→Locate→Implement→Test→Ship.*
