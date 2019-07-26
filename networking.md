# Understand the networking configuration on the cluster nodes
# Understand Pod networking concepts
# Understand service networking
```
ps -fC kube-proxy | grep proxy-mode
kubectl logs kube-proxy-cpm5m -nkube-system | grep proxy-mode
ps -fC kube-apiserver | grep service-cluster-ip-range
```
Pod IP range should not overlap Service IP range
```
k run nginx --image=nginx --restart=Never
k expose po nginx --port 80

k get po,svc -owide
iptables -L -t nat | grep nginx
cat /var/log/kube-proxy.log
```
IP range of node
```
ip a show <interface>
```
IP range of pod
```
k logs weave-net-v6slt weave -nkube-system | grep ipalloc
```
IP range of svc
```
ps -fC kube-apiserver | grep service-cluster-ip-range
```
# Deploy and configure network load balancer
Deployment, Service, ConfigMap, Auth
```
k create ns ingress-space

k config current-context
k config set-context kubernetes-admin@kubernetes --namespace=ingress-space

k create cm nginx-configuration
k create sa ingress-serviceaccount

ingress-role
ingress-rolebinding
ingress-controller

k expose deploy ingress-controller --type=NodePort --port=80 --name=ingress --dry-run -oyaml > ingress.yaml
vim ingress-service.yaml # add nodePort
k create -f ingress-service.yaml

k create -f ingress.yaml # in app-space
```
# Know how to use Ingress rules
Route to single application: ww<span>w.example.com
```
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: ingress-wear
spec:
  backend:
    serviceName: wear-service
    servicePort: 80
```
Route based on url: ww<span>w.example.com/watch ww<span>w.example.com/watch
```
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: ingress-wear-watch
spec:
  rules:
  - http:
      paths:
      - path: /wear
        backend:
          serviceName: wear-service
          servicePort: 80
      - path: /watch
        backend:
          serviceName: watch-service
          servicePort: 80
```
Route based on domain name: wear.example.com, watch.example.com
```
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: ingress-wear-watch
spec:
  rules:
  - host: wear.example.com
    http:
      paths:
      - backend:
          serviceName: wear-service
          servicePort: 80
  - host: watch.example.com
    http:
      paths:
      - backend:
          serviceName: watch-service
          servicePort: 80
```
# Know how to configure and use the cluster DNS
```
k run nginx --image=nginx --restart=Never
k expose po nginx --port 80

k run -it busybox --image=busybox --restart=Never -- sh
ping nginx
ping nginx.default
ping nginx.default.svc
ping nginx.default.svc.cluster.local

ping 10-32-0-2.default.pod
ping 10-32-0-2.default.pod.cluster.local
```
```
k run -it busybox --image=busybox --restart=Never -- sh
cat /etc/resolv.conf
```
```
cat /var/lib/kubelet/config.yaml | head -20
```
```
k get cm coredns -nkube-system --export -oyaml
```
# Understand CNI
```
ps -fC kubelet | grep cni
ls /opt/cni/bin/
ls /etc/cni/net.d/
```
```
k get ds weave-net -nkube-system
k logs weave-net-dmlxk weave -nkube-system
```
```
brctl show
ip a show <bridge>
```
```
docker ps
docker inspect <container-id> | jq -r '.[0].State.Pid'
nsenter -t <pid> -n ip r
```
ipam
