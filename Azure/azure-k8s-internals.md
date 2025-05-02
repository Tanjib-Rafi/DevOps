### 1 master node & 2 worker node

- master node with public ip , worker node will have private ip

    `ssh <your-username>@<vm-public-ip>`

- On the master node, run the following to install packages:

### Steps to Install `kubeadm` on Ubuntu:

1. **Update your apt packages:** Run this command to make sure all your apt packages are up to date:

   `sudo apt update && sudo apt upgrade -y`

2. **Install dependencies:** Install dependencies required for Kubernetes:

   `sudo apt install -y apt-transport-https ca-certificates curl`

3. **Create the keyring directory if it doesn't exist

    `sudo mkdir -p /etc/apt/keyrings`

4. **Add Kubernetes signing key:** Run this command to add the Kubernetes GPG key:

   `curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.28/deb/Release.key | sudo tee /etc/apt/keyrings/kubernetes-apt-keyring.asc > /dev/null-`

5. **Add Kubernetes repository:** Add the Kubernetes apt repository to your system:

   `secho "deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.asc] https://pkgs.k8s.io/core:/stable:/v1.28/deb/ /" | sudo tee /etc/apt/sources.list.d/kubernetes.list`

6. **Update packages
   
    `sudo apt update`
   
7. **Install** `kubeadm`**,** `kubelet`**, and** `kubectl`**:

   `sudo apt update sudo apt install -y kubeadm kubelet kubectl`

8. **Mark them to not be upgraded:** To prevent `kubeadm`, `kubelet`, and `kubectl` from being accidentally upgraded, use this command:

   `sudo apt-mark hold kubeadm kubelet kubectl`

9. **Verify Installation:** To verify if `kubeadm` is installed correctly, you can check the version:

   `kubeadm version`



# **Container Runtime** (containerd or Docker) - Manages actual containers (pods)
Why?
Kubernetes does not run containers directly-it needs a container runtime (like containerd or Docker) to actually start, stop, and manage containers on each node.
If the runtime isn’t running or installed, Kubernetes cannot create or manage pods.

```
# Install containerd
sudo apt update
sudo apt install -y containerd

# Configure containerd
sudo mkdir -p /etc/containerd
sudo containerd config default | sudo tee /etc/containerd/config.toml

# Start and enable containerd
sudo systemctl restart containerd
sudo systemctl enable containerd
```

# **br_netfilter Kernel Module** - Enables pod networking and network policies
Why?
Kubernetes networking relies on Linux bridges for pod-to-pod communication.

The br_netfilter kernel module allows iptables to see bridged traffic, which is essential for Kubernetes networking and network policies to work.

Without this, your pods may not be able to communicate, and network policies won’t be enforced.

- Load kernel modules for Kubernetes

```
cat <<EOF | sudo tee /etc/modules-load.d/k8s.conf
br_netfilter
EOF
sudo modprobe br_netfilter
```

# **IP Forwarding** - 	Allows network traffic between pods, nodes, and services
Why?
Kubernetes needs to route network traffic between pods, services, and external endpoints.

Enabling net.ipv4.ip_forward tells the Linux kernel to allow forwarding of network packets between interfaces.

Without IP forwarding, pods cannot communicate across nodes, and services like LoadBalancer/NodePort won’t work.

```
cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-iptables  = 1
net.ipv4.ip_forward                 = 1
EOF
sudo sysctl --system
```

# **Disabling Swap** - Ensures stable, predictable memory for Kubernetes components
Why?
Kubernetes expects nodes to have predictable memory availability.

If swap is enabled, the Linux kernel might move some memory pages to disk, causing unpredictable delays.

Kubernetes will refuse to start if swap is on, to ensure performance and stability.

```
sudo swapoff -a
sudo sed -i '/ swap / s/^\(.*\)$/#\1/g' /etc/fstab
```

- After running kubeadm init, only the root user can run kubectl because the kubeconfig lives at /etc/kubernetes/admin.conf.

Running the three commands makes sure your non-root user (the one you're SSHed in as) can control the cluster via kubectl.

`
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
`

# Configure crictl for containerd

`sudo crictl config runtime-endpoint unix:///run/containerd/containerd.sock`

- On the master node, initialize the Kubernetes cluster using kubeadm:

`
sudo kubeadm init --pod-network-cidr=10.244.0.0/16
`

```
Why this specific CIDR (10.244.0.0/16)?
This CIDR block is commonly used for Flannel (a network plugin) and allows the Kubernetes network to work smoothly with internal IPs for pods. It’s a private network used internally by the cluster.
```

- Apply Flannel CNI

`
kubectl apply -f https://raw.githubusercontent.com/flannel-io/flannel/master/Documentation/kube-flannel.yml
`

- Check Flannel status
`kubectl get pods -n kube-flannel -w`


# Compare the CA from your kubeconfig with the cluster’s CA
`diff <(grep certificate-authority-data ~/.kube/config | awk '{print $2}' | base64 -d) /etc/kubernetes/pki/ca.crt`

```
When you reset or re-initialize your cluster with kubeadm, it generates a new CA and new admin credentials.

If you had an old ~/.kube/config from a previous cluster, it will not match the new CA, causing TLS errors.

Always update your kubeconfig after (re)initializing your cluster.
```

# Generates and prints a kubeadm join command, which you can run on a new worker node to join it to your existing Kubernetes cluster.
`
kubeadm token create --print-join-command
`
