# Use label selectors to schedule Pods
```
k get no
k label no node01 disktype=ssd
k get no --show-labels
```
```
apiVersion: v1
kind: Pod
metadata:
  ...
spec:
  ...
  nodeSelector:
    disktype: ssd
```
# Understand the role of DaemonSets
* DaemonSets ensure that one replica of pod is always present in all nodes in cluster
* Replica is added automatically to new node
* Replica is removed automatically when node is removed
* Ignored by `kube-scheduler`
* Use cases: Monitoring agent, log collector
* In K8s: kube-proxy, Weave Net
```
k get ds kube-proxy -nkube-system
```
# Understand how resource limits can affect Pod scheduling
```
k apply -f https://k8s.io/examples/admin/resource/memory-defaults.yaml
k run nginx --image=nginx --restart=Never
k get po nginx -ojson | jq -r '.spec.containers[0].resources'
```
# Understand how to run multiple schedulers and how to configure Pods to use them
* Default scheduler distributes pods across nodes evenly considering various conditions (i.e. taints, tolerations, node affinity, etc)
* Use cases: Perform additional checks
* Set `scheduler-name` and `lock-object-name` as `my-scheduler` when create
```
apiVersion: v1
kind: Pod
metadata:
  ...
spec:
  ...
  schedulerName: my-scheduler
```
# Manually schedule a pod without a scheduler
```
apiVersion: v1
kind: Pod
metadata:
  ...
spec:
  ...
  nodeName: node01
```
* Kubelet can create static pods and ensure they stay alive by placing pod definition files in designated folder
* If file is modified, Kubelet recreates pod
* If file is removed, Kubelet deletes pod
* Since static pods are not dependent on K8s control plane, static pods can be used to deploy them as pods on a node
* Node name will be appended to pod name
* Like DaemonSets, ignored by `kube-scheduler`
```
ps -fC kubelet | cat | grep -- --pod-manifest-path
ps -fC kubelet | cat | grep -- --config
cat /var/lib/kubelet/config.yaml | grep staticPodPath
```
```
k run static-busybox --image=busybox --restart=Never --dry-run -oyaml --command -- sleep 1000 > /etc/kubernetes/manifests/static-busybox.yaml
```
# Display scheduler events
```
k get ev -owide
k logs kube-scheduler-master -nkube-system
k logs my-scheduler -nkube-system
```
# Know how to configure the Kubernetes scheduler
```
cat /etc/systemd/system/kube-scheduler.service
cat /etc/kubernetes/manifests/kube-scheduler.yaml (kubeadm)
ps -fC kube-scheduler | cat
```
