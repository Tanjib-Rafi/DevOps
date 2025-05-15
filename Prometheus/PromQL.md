- High CPU Usage Alert

```
100-avg by(instance)(rate(node_cpu_seconds_total{mode='idle'}[5m])*100) > 85
```

- Instance-Specific Alerts

```
100-avg by(instance)(rate(node_cpu_seconds_total{instance="production-server-1",mode='idle'}[5m])*100) > 80
```

