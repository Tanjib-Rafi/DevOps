# User vs ServiceAccount in Kubernetes

| Type               | Format                                     | Typical Use             | Auth Source             |
| ------------------ | ------------------------------------------ | ----------------------- | ----------------------- |
| **User Account**   | Custom, like `alice` or `dev@example.com`  | Human users             | Certificate, OIDC, etc. |
| **ServiceAccount** | `system:serviceaccount:<namespace>:<name>` | Apps, controllers, bots | Managed by Kubernetes   |


User Account Identity in Kubernetes

Kubernetes doesn't manage user accounts directly. It trusts external identity systems (e.g., client certs, OIDC providers, etc.). So for users:

Define users in kubeconfig (locally).

Kubernetes sees the name from the client certificate or token as the user's identity.

Refer to that identity in RBAC using the name field.
    
Just make sure the Kubernetes API allows impersonating that user (via Impersonate RBAC permissions).

# What Kind of Certificate?

Kubernetes supports client certificate-based authentication. This uses X.509 certificates, specifically:

A client certificate (.crt)

A private key (.key)

Optionally, the CA certificate of the Kubernetes cluster

These certificates are used for mutual TLS (mTLS) between the kubectl client and the Kubernetes API server.

🧰 Where Are These Certificates Used?

They are typically referenced in ~/.kube/config (kubeconfig file):

🔧 How Are These Certificates Issued?

There are a few ways:

Manually using openssl or cfssl (good for simple setups or testing)

Cluster admin issues them using Kubernetes’ built-in certificate signing APIs

Tools like kubeadm issue certs when setting up a cluster

External CA or PKI (e.g., Vault, Active Directory Certificate Services)


📌 Example: Creating a Client Cert Manually (for user alice)

```openssl genrsa -out alice.key 2048```

```openssl req -new -key alice.key -out alice.csr -subj "/CN=alice"```

```openssl x509 -req -in alice.csr -CA ca.crt -CAkey ca.key -CAcreateserial -out alice.crt -days 365```


