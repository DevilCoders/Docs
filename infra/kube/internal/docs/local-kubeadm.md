# Setup Local kubeadm

[Guide](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/)

## Update apt sources and default packages

```shell
sudo apt update && sudo apt upgrade -y
```

## Install and setup container runtime (containerd)

```shell
sudo apt-get install -y containerd
```

```shell
cat <<EOF | sudo tee /etc/modules-load.d/containerd.conf
overlay
br_netfilter
EOF

sudo modprobe overlay
sudo modprobe br_netfilter

cat <<EOF | sudo tee /etc/sysctl.d/99-kubernetes-cri.conf
net.bridge.bridge-nf-call-iptables = 1
net.bridge.bridge-nf-call-ip6tables = 1
net.ipv4.ip_forward = 1
EOF

sudo sysctl --system

sudo mkdir -p /etc/containerd
containerd config default | sudo tee /etc/containerd/config.toml
sudo systemctl restart containerd
```

## Install kubeadm, kubelet, kubectl

```shell
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl

sudo curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg

echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list

#KUBEVERSION=1.23.1-00

sudo apt-get update
sudo apt-get install -y kubelet=$KUBEVERSION kubeadm=$KUBEVERSION kubectl=$KUBEVERSION
sudo apt-mark hold kubelet=$KUBEVERSION kubeadm=$KUBEVERSION kubectl=$KUBEVERSION
```

## Start and setup cluster

```shell
sudo kubeadm init --cri-socket /run/containerd/containerd.sock --pod-network-cidr 192.168.0.0/16

# Setup local config
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

# Allow scheduling on master node
kubectl taint nodes --all node-role.kubernetes.io/master-
```

## Install CNI plugin

```shell
kubectl apply -f https://github.com/coreos/flannel/raw/master/Documentation/kube-flannel.yml
```
