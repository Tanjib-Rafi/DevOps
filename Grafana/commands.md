- Find ConfigMap:

```
kubectl get configmap -n <namespace> | grep grafana
```

- Edit the ConfigMap:

```
kubectl edit configmap <grafana-configmap-name> -n <namespace>
```


# Use Helm Values (if installed via Helm)

```
helm upgrade grafana grafana/grafana -n <namespace> -f values.yaml
```

`
Instead of hardcoding SMTP passwords in ConfigMaps or Helm values, use a Kubernetes Secret and reference it.
`
