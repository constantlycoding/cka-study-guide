# Understand the Kubernetes API primitives
pod
```
k run nginx --image=nginx --restart=Never
k get po
```
replicaset
```
k run nginx --image=nginx --replicas=4
k get rs
```
deployment
```
k run nginx --image=nginx
k get deploy
```
namespace
```
k create ns dev
k config set-context --current --namespace=dev
k get sa default -ojson | jq -r '.metadata.namespace'
```
resource quota
```
apiVersion: v1
kind: ResourceQuota
metadata:
  name: compute-quota
  namespace: dev
spec:
  hard:
    requests.cpu: "4"
    requests.memory: 5Gi
    limits.cpu: "10"
    limits.memory: 10Gi
    pods: "10"
```
```
k get quota -n dev
```
# Understand the Kubernetes cluster architecture
| Component       | Responsibility                                                                     | Node   |Port |
| --------------- | ---------------------------------------------------------------------------------- | ------ |--- |
| etcd            | store cluster information                                                          | master | 2379 |
| kube-apiserver  | authenticate/validate request, retrieve/update etcd                                | master |
| kube-controller | monitor state of various components, work towards bringing system to desired state | master |
| kube-scheduler  | decide which pod goes to which node, filter/rank nodes                             | master |
| kubelet         | register node, create pods as instructed by kube-scheduler, monitor node and pods  | worker |
| kube-proxy      | create rules on each node to forward traffic to services to backend pods           | worker |
# Understand Services and other network primitives
ClusterIP
```
k expose pod redis --port=6379
k get svc
```
NodePort
```
k expose pod nginx --port=80 --dry-run -oyaml > nginx-svc.yaml
# Cannot specify nodePort
vim nginx-svc.yaml
# Add:
# spec:
#   type: NodePort
#   ports:
#   - port: 80
#     nodePort: 30008
k create -f nginx-svc.yaml
k get svc
```
