- Retrieve AKS Cluster Credentials for kubectl Access Locally

```
az aks get-credentials --resource-group <RESOURCE_GROUP> --name <AKS_CLUSTER_NAME>
```

- Install Helm

```
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```

- Add the Prometheus Helm Repo, which includes Prometheus, Alertmanager, and Grafana

```helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
```
```
helm repo update
```

- Deploy Prometheus using Helm

```
helm install prometheus prometheus-community/kube-prometheus-stack -n monitoring --create-namespace
```

- Check Prometheus is running

```
kubectl get pods -n monitoring
```

- Access Prometheus

```
kubectl port-forward -n monitoring svc/prometheus-kube-prometheus-prometheus 9090:9090
```

- Open your browser and navigate to

```
http://localhost:9090
```
