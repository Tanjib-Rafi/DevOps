- Get the grafana service file

```
kubectl get svc prometheus-grafana -n monitoring -o yaml > grafana.yaml
```
```
kubectl apply -f grafana.yaml
```

> This retrieves the live YAML of the existing Grafana service running in your Kubernetes cluster.
It includes the current state of the service, including automatically assigned fields (e.g., IPs, annotations).
If Grafana was installed via Helm, this YAML is not the source code—it’s just the deployed result.
✅ Use when you want to inspect or manually edit an existing Kubernetes object.


- Get the grafana default helm settings
```
helm show values grafana/grafana > values.yaml
```
```
helm upgrade --install grafana grafana/grafana -f values.yaml -n monito
```

> This fetches the default Helm values for the Grafana Helm chart before deployment.
It contains configuration options before they are applied, including service type, persistence, authentication, dashboards, etc.
This is not the live configuration but the default settings that Helm uses.
✅ Use when you want to modify Grafana’s settings before deploying or upgrading with Helm.

> ***If Grafana was installed via Helm, always update values.yaml instead of editing manually.***
