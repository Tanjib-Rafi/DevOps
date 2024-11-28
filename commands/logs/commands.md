- ```kubectl logs <pod-name>```
- ```kubectl logs <pod-name> -c <container_name>```
- ```kubectl get pods --selector=<deployment-label>```
- ```kubectl get events --sort-by='.metadata.creationTimestamp'```
- ```kubectl describe pod <pod-name>```
- ```journalctl -u kubelet```
- ```kubectl top```
  
# check the connection between deployment and service

- ```kubectl get pods --show-labels```
- ```kubectl get pods --selector app=label_name --show-labels```
- ```kubectl get endpoints service_name```
- ```kubectl get pods --selector app=label_name --show-labels -o wide```
- ```kubectl port-forward service/service_name 8080:80```

# check ingress logs
- ```kubectl get pods -n kube-system | grep nginx-ingress```

# debugging tools (kubectl exec, stern)
