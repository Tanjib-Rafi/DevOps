### Nginx Ingress Controller

- using kubectl
  ```
  kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/cloud/deploy.yaml
  ```
  
- using helm
  ```
  helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
  ```
  ```
  helm repo update
  ```
  ```
  helm install nginx-ingress ingress-nginx/ingress-nginx --namespace kube-system
  ```

- restart nginx
   ```
  kubectl rollout restart deployment ingress-nginx-controller -n ingress-nginx
   ```
