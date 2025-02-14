# using helm

- Identify the Helm Release
```
helm list -n monitoring
```

- Get the Current Helm Values
```
helm get values <release-name> -n monitoring > prometheus-values.yaml
```

- Upgrade the Helm Release with Changes
```
helm upgrade <release-name> prometheus-community/kube-prometheus-stack -f prometheus-values.yaml -n monitoring
```

