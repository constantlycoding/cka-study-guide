Specify a memory request and a memory limit
```
k run mem-demo --image=polinux/stress --restart=Never --requests=memory=100Mi --limits=memory=200Mi --command -- stress --vm 1 --vm-bytes 150M --vm-hang 1
```
Exceed a Container’s memory limit
```
k run mem-demo --image=polinux/stress --restart=Never --requests=memory=50Mi --limits=memory=100Mi --command -- stress --vm 1 --vm-bytes 250M --vm-hang 1
```
Specify a memory request that is too big for your Nodes
```
k run mem-demo --image=polinux/stress --restart=Never --requests=memory=1000Gi --limits=memory=1000Gi --command -- stress --vm 1 --vm-bytes 150M --vm-hang 1
```
Check
```
k get po mem-demo -ojson | jq -r '.status'
```
