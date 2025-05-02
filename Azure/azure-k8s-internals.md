\### 1 master node & 2 worker node

\- master node with public ip , worker node will have private ip

    `ssh <your-username>@<vm-public-ip>`

\- On the master node, run the following:

\`

### Steps to Install `kubeadm` on Ubuntu:

1. **Update your apt packages:** Run this command to make sure all your apt packages are up to date:

   `sudo apt update && sudo apt upgrade -y`

2. **Install dependencies:** Install dependencies required for Kubernetes:

   `sudo apt install -y apt-transport-https ca-certificates curl`

3. **Add Kubernetes signing key:** Run this command to add the Kubernetes GPG key:

   `curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -`

4. **Add Kubernetes repository:** Add the Kubernetes apt repository to your system:

   `sudo sh -c 'echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" > /etc/apt/sources.list.d/kubernetes.list'`

5. **Install** `kubeadm`**,** `kubelet`**, and** `kubectl`**:

   `sudo apt update sudo apt install -y kubeadm kubelet kubectl`

6. **Mark them to not be upgraded:** To prevent `kubeadm`, `kubelet`, and `kubectl` from being accidentally upgraded, use this command:

   `sudo apt-mark hold kubeadm kubelet kubectl`

7. **Verify Installation:** To verify if `kubeadm` is installed correctly, you can check the version:

   `kubeadm version`

`
sudo kubeadm init --pod-network-cidr=10.244.0.0/16
`

Why this specific CIDR (10.244.0.0/16)?
This CIDR block is commonly used for Flannel (a network plugin) and allows the Kubernetes network to work smoothly with internal IPs for pods. It’s a private network used internally by the cluster.

\`

