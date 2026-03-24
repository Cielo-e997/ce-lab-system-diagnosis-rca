# Correlation Analysis

## Observed Patterns

During the incident, several metrics showed strong correlation:

- Traffic increased significantly (3x)
- Latency increased sharply (16x)
- Error rate increased dramatically (50x)
- Database connection pool reached 100% utilization

---

## Metric Correlation

### Traffic vs Latency
- As request rate increased, latency also increased
- Indicates system could not handle additional load efficiently

### Traffic vs Errors
- Higher traffic led to more failed requests
- Suggests system saturation or resource bottleneck

### Latency vs Error Rate
- Latency spikes occurred alongside increased error rates
- Indicates requests were timing out

### Connection Pool vs Latency
- Connection pool reached 100% utilization
- Requests began queuing for available connections
- Directly caused latency increase

---

## Key Insight

The system degradation was not caused by CPU or memory limitations, but by a bottleneck at the database connection layer.

---

## Conclusion

There is a clear cause-and-effect relationship:

Traffic spike → Connection pool exhaustion → Request queuing → Latency increase → Timeouts → Error rate increase

This confirms that the database connection pool was the primary bottleneck and root cause of the incident.