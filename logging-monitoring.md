# Understand how to monitor all cluster components
```
git clone https://github.com/kubernetes-incubator/metrics-server.git
cd metrics-server
k create -f deploy/1.8+/
```
```
k top no
k top po
```
```
k get cs
```
# Understand how to monitor applications
```
k describe po webapp
```
# Manage cluster component logs
Master
```
/var/log/kube-apiserver.log
/var/log/kube-scheduler.log
/var/log/kube-controller-manager.log 
```
```
journalctl -u kube-apiserver
journalctl -u kube-scheduler
journalctl -u kube-controller-manager
```
```
k logs kube-apiserver-master -nkube-system
k logs kube-scheduler-master -nkube-system
k logs kube-controller-manager-master -nkube-system
```
```
k logs kube-proxy-7njb4 -nkube-system
k logs weave-net-ljfxm weave -nkube-system
```
Worker
```
/var/log/kubelet.log
/var/log/kube-proxy.log
```
```
journalctl -u kubelet
journalctl -u kube-proxy
```
# Manage application logs
```
k logs -f webapp-1
```
