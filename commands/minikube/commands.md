start minikube:
- ```minikube start --nodes=1```
add node:
- ```minikube node add```

Test Loadbalancer and Nodeport:
- ```minikube tunnel```

- HTTP: http://192.168.49.2:32568/
- HTTPS: https://192.168.49.2:30639/
