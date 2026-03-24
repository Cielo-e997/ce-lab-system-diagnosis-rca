# Investigation Notes

## Initial Situation

The system showed degraded performance with increased latency and error rates. Alerts indicated abnormal behavior in production.

---

## Step 1: Applied RED Method

### Rate
- Observed a significant increase in request volume
- Traffic increased from normal baseline to 3x higher

### Errors
- Error rate increased from 0.1% to 5%
- Increase in 5XX responses

### Duration
- Latency increased from 300ms (P95) to 5,000ms
- Significant impact on user experience

---

## Step 2: Applied USE Method

### CPU
- Utilization normal (~45%)
- No signs of saturation

### Memory
- Stable (~70%)
- No swapping or memory pressure

### Database Connection Pool
- Utilization reached 100%
- Requests waiting for connections
- Timeout errors observed

---

## Step 3: Correlation

- Traffic spike coincided with latency increase
- Connection pool saturation aligned with error spikes
- No correlation with CPU or memory usage

---

## Conclusion

The investigation confirmed that the system degradation was caused by database connection pool exhaustion.

The RED method identified the symptoms, while the USE method pinpointed the root cause at the resource level.