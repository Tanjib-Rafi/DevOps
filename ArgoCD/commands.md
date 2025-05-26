```kubectl create namespace argocd```

```kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml```


```kubectl port-forward svc/argocd-server -n argocd 8080:443```

```kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d```

```
argocd app create my-app \
  --repo https://github.com/your-org/my-git-repo.git \
  --path apps/my-app \
  --dest-server https://kubernetes.default.svc \
  --dest-namespace default
```
