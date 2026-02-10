![[namastedev.com_learn_namaste-frontend-system-design_alerting (2).png]]


## What is Alerting?
Alerting is the mechanism of notifying teams when something **critical or abnormal** happens in the system based on telemetry data.

Telemetry tells us *what is happening*.  
Alerting tells us *when we need to act*.

---

## Why Alerting is Needed
- We cannot continuously watch dashboards
- Critical issues must be acted on immediately
- Helps prevent downtime and poor user experience
- Enables faster incident response

Good alerting = peace of mind.

---

## How Alerting Works
1. Telemetry data is collected (metrics, logs, events)
2. Metrics are continuously monitored
3. Thresholds are defined for each metric
4. When a threshold is breached
5. An alert is triggered and sent to the responsible team

---

## Thresholds
Thresholds define **acceptable limits** for a metric.

Examples:
- API response time > 2 seconds
- Error rate > 2%
- CPU usage > 80%
- Memory usage > 75%
- Sudden spike in button clicks causing excessive API calls
- Drop in conversion rate
- Increase in failed form submissions

Thresholds can be set based on:
- Performance
- Resource utilization
- Errors
- User behavior
- Business metrics

---

## Types of Alerts

### Performance Alerts
- Page load time too high
- LCP / FCP / CLS beyond limits
- API latency spikes

### Resource Alerts
- High CPU usage
- High memory usage
- Resource exhaustion

### Error Alerts
- 5xx error spike
- API failures
- Client-side JS exception surge
- Network failures

### User Behavior Alerts
- Abnormal click patterns
- Too many retries
- Unexpected user drop-offs
- Unusual traffic spikes

---

## Alert Delivery Channels
Alerts can be sent through multiple channels depending on severity.

Examples:
- Email notifications
- Slack integration
- PagerDuty alerts
- SMS notifications
- PagerDuty phone calls (for critical incidents)

Higher severity → more aggressive alerting.

---

## Severity Levels
Alerts are usually categorized by severity:
- Info
- Warning
- Critical

Only critical alerts should wake someone up at night.

---

## On-Call System
- Engineers rotate on an on-call schedule
- On-call person monitors dashboards and SLIs
- Responsible for triaging and resolving incidents
- PagerDuty automatically routes alerts to the on-call engineer

If something critical happens:
- Alert is triggered
- On-call engineer gets notified (call/SMS)
- Issue is investigated and resolved

---

## Good Alerting vs Bad Alerting

Bad Alerting:
- Too many alerts
- Noisy alerts
- Alerts for non-critical issues
- Alert fatigue

Good Alerting:
- Actionable alerts
- Clear thresholds
- Correct severity
- Only alerts when human intervention is required

---

## Key Takeaway
Alerting converts telemetry signals into actionable notifications, ensuring critical issues are detected and resolved quickly without constant manual monitoring.

---

Some of the tools are - Opsgenie, Grafana, openTelemetry. pageDuty AND ZENDURY.
## One-Line Interview Summary
Alerting uses telemetry thresholds to notify teams when critical conditions occur, enabling fast incident response and reliable system operation.
