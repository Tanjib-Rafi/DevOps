### Enable IAM OIDC Provider
--- This step establishes trust between your Kubernetes cluster and IAM.
aws eks --region <region> update-cluster-config --name <cluster_name> --enable-oidc

### Attach policy to IAM user
aws iam create-role --role-name eks-ecr-role --assume-role-policy-document file://trust-policy.json
aws iam attach-role-policy --role-name eks-ecr-role --policy-arn <policy_arn>

### Associate the Role with a Kubernetes Service Account
kubectl annotate serviceaccount <service_account_name> \
  eks.amazonaws.com/role-arn=arn:aws:iam::<account_id>:role/eks-ecr-role
