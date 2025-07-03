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
