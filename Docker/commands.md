> if docker image is private


```kubectl create secret docker-registry regcred --docker-username=<dockerhub-username> --docker-password=<dockerhub-password> --docker-email=<your-email> -n <namespace-name>```

> If you're storing secrets in files, you can create a secret.yml


```
apiVersion: v1
kind: Secret
metadata:
  name: regcred
  namespace: my-namespace
type: kubernetes.io/dockerconfigjson
data:
  .dockerconfigjson: <base64-encoded-docker-config>

```

> To generate the base64-encoded .dockerconfigjson file:

```
echo -n '{"auths":{"https://index.docker.io/v1/":{"username":"mydocker_username","password":"mydocker_password","email":"mydockeremail@gmail.com"}}}' | base64
```

> Paste the encoded string in place of <base64-encoded-docker-config>
