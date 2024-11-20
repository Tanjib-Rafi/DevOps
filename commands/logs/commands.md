- kubectl logs <pod-name>
- kubectl logs <pod-name> -c <container_name>
- kubectl get pods --selector=<deployment-label>
- kubectl get events --sort-by='.metadata.creationTimestamp'
- kubectl describe pod <pod-name>
- journalctl -u kubelet
- kubectl top

# debugging tools (kubectl exec, stern)
