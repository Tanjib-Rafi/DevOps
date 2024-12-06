### Install prometheus using helm:

- ```helm repo add prometheus-community https://prometheus-community.github.io/helm-charts```

  
- ```helm repo update```

  
- ```helm install prometheus prometheus-community/prometheus --namespace monitoring```


### Locally check prometheus web ui :
```kubectl port-forward -n monitoring svc/prometheus-server 9090:80```
