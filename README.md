# Lab M6.04 - Diagnose Degraded System and Write Root Cause Analysis

## Investigation Summary

This lab simulates a degraded production system where application performance deteriorated significantly. A systematic investigation was conducted using the RED (Rate, Errors, Duration) and USE (Utilization, Saturation, Errors) methodologies.

The investigation followed a structured approach:
1. Analyze service-level metrics using the RED method
2. Analyze resource-level metrics using the USE method
3. Correlate findings to identify the root cause
4. Propose mitigation and long-term solutions

---

## Key Findings

- Root cause: **Database connection pool exhaustion**
- Traffic increased 3x (500 → 1,500 requests/min)
- Error rate increased from 0.1% to 5%
- Latency increased from 300ms to 5,000ms (P95)
- CPU and memory remained within normal ranges
- Bottleneck identified at the database connection layer

---

## Timeline of Discovery

| Time | Action |
|------|--------|
| T+0 min  | Alert triggered — high latency detected |
| T+10 min | RED method confirmed increased traffic, errors, and latency |
| T+20 min | USE method showed CPU and memory normal |
| T+25 min | Identified database connection pool saturation |
| T+30 min | Root cause confirmed |
| T+40 min | Fix proposed and system stabilized |

---

## Repository Contents

- `rca/root-cause-analysis.md` — Full RCA document  
- `rca/investigation-notes.md` — Investigation process  
- `analysis/red-method-analysis.md` — RED method findings  
- `analysis/use-method-analysis.md` — USE method findings  
- `analysis/correlation-analysis.md` — Metric correlations  
- `proposals/immediate-fix.md` — Immediate mitigation  
- `proposals/long-term-fix.md` — Long-term solution  
- `proposals/prevention.md` — Prevention strategy  
- `screenshots/` — Supporting dashboard and metric visuals  

---

## Conclusion

Using structured methodologies like RED and USE enables efficient and reliable incident investigation. The combination of monitoring data and systematic analysis allowed rapid identification of the root cause and clear definition of corrective actions.