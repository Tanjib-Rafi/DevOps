- High CPU Usage Alert

```
100-avg by(instance)(rate(node_cpu_seconds_total{mode='idle'}[5m])*100) > 85
```

- Instance-Specific Alerts

```
100-avg by(instance)(rate(node_cpu_seconds_total{instance="production-server-1",mode='idle'}[5m])*100) > 80
```

- Memory Usage

```
(node_memory_MemTotal_bytes - node_memory_MemAvailable_bytes) / node_memory_MemTotal_bytes * 100
```
