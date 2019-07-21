# Understand Kubernetes cluster upgrade process
* No other component version should be higher that kube-apiserver
* kubectl can be at any version
* K8s supports only up to recent 3 minor versions
* Upgrade one minor version at a time
* Upgrade master nodes, then worker nodes
* While master is being upgraded, control plane components go down briefly
* Workloads on worker nodes are not impacted
Master
```
kubeadm upgrade plan
```
```
sudo apt-get update
apt install kubeadm=1.12.0-00
kubeadm upgrade apply v1.12.0
```
```
apt install kubelet=1.12.0-00
systemctl restart kubelet
```
Worker
```
k drain node01
```
```
apt install kubeadm=1.12.0-00
apt install kubelet=1.12.0-00
kubeadm upgrade node config --kubelet-version $(kubelet --version | cut -d ' ' -f 2)
kubeadm upgrade node config --kubelet-version v1.12.0
systemctl restart kubelet
```
```
k uncordon node01
```
# Facilitate operating system upgrades
# Implement backup and restore methodologies
Resource configuration
```
k get all --all-namespaces -oyaml > all-deploy-services.yaml
```
etcd
```
ETCDCTL_API=3 etcdctl version

ETCDCTL_API=3 etcdctl snapshot save /tmp/snapshot-pre-boot.db \
  --endpoints=https://[127.0.0.1]:2379 \
  --cacert=/etc/kubernetes/pki/etcd/ca.crt \
  --cert=/etc/kubernetes/pki/etcd/server.crt \
  --key=/etc/kubernetes/pki/etcd/server.key

ETCDCTL_API=3 etcdctl snapshot status /tmp/snapshot-pre-boot.db \
  --write-out=table

ETCDCTL_API=3 etcdctl snapshot restore /tmp/snapshot-pre-boot.db \
  --endpoints=https://[127.0.0.1]:2379 \
  --cacert=/etc/kubernetes/pki/etcd/ca.crt \
  --name=master \
  --cert=/etc/kubernetes/pki/etcd/server.crt \
  --key=/etc/kubernetes/pki/etcd/server.key \
  --data-dir /var/lib/etcd-from-backup \
  --initial-cluster=master=https://127.0.0.1:2380 \
  --initial-cluster-token etcd-cluster-1 \
  --initial-advertise-peer-urls=https://127.0.0.1:2380   
```
restart etcd with correct `data-dir` and `initial-cluster-token` and volumemounts

