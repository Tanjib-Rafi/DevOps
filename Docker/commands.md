- if docker image is private
  
```kubectl create secret docker-registry regcred --docker-username=<dockerhub-username> --docker-password=<dockerhub-password> --docker-email=<your-email> -n <namespace-name>```
