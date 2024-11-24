Enable IAM OIDC Provider
This step establishes trust between your Kubernetes cluster and IAM.
aws eks --region <region> update-cluster-config --name <cluster_name> --enable-oidc
