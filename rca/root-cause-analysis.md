# Root Cause Analysis: High Latency Incident

## Executive Summary

**Incident:** API latency increased from 300ms (P95) to 5,000ms (P95)  
**Impact:** Users experienced slow response times and a 5% error rate  
**Duration:** 60 minutes  
**Root Cause:** Database connection pool exhaustion  
**Status:** Resolved  

---

## Timeline

| Time | Event |
|------|-------|
| T+0 min | High latency detected |
| T+5 min | Investigation started |
| T+10 min | RED method confirmed elevated traffic, errors, and latency |
| T+20 min | USE method applied to infrastructure |
| T+25 min | Database connection pool at 100% utilization |
| T+30 min | Root cause identified |
| T+40 min | Fix proposed and system stabilized |

---

## Root Cause

**Problem:** Database connection pool exhaustion

### Why it happened:

1. Traffic increased significantly (3x normal load)
2. Connection pool size was limited to 20 connections
3. No dynamic scaling for connection pool
4. Requests queued waiting for available connections
5. Requests timed out, causing errors and latency

---

## Evidence

- RED method showed:
  - Traffic increased 3x
  - Error rate increased 50x
  - Latency increased 16x

- USE method showed:
  - CPU and memory remained normal
  - Database connection pool at 100% utilization

- Correlation analysis:
  - Traffic spike directly led to connection pool exhaustion
  - Connection exhaustion caused queuing and timeouts

---

## Impact

- Users affected: High number of active users experienced delays
- Error rate: 5%
- Latency: Increased to 5,000ms (P95)
- Severity: High (service degraded but not completely down)

---

## Resolution

### Immediate Fix

Increased database connection pool size:

```python
DB_CONNECTION_POOL_SIZE = 50  # Previously 20
```

### Result

- Latency returned to near-normal levels
- Error rate decreased significantly
- Connection pool utilization stabilized

---

## Lessons Learned

### What Went Well

- Monitoring detected the issue quickly  
- Structured RED/USE approach led to fast diagnosis  
- Root cause identified efficiently  

### What Went Wrong

- No monitoring on connection pool utilization  
- No capacity planning for increased traffic  
- No auto-scaling mechanism  

---

## Action Items

### Immediate

- Increase connection pool size  
- Add alert for connection pool utilization > 80%  

### Short-term

- Implement monitoring for connection pool usage  
- Perform load testing under high traffic  

### Long-term

- Implement dynamic connection pool scaling  
- Establish capacity planning practices  
- Improve communication between teams for traffic events  

---

## Prevention

To prevent recurrence:

- Monitor connection pool utilization  
- Implement alerts for saturation  
- Enable dynamic scaling of resources  
- Perform load testing regularly