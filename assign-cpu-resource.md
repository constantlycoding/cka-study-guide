Specify a CPU request and a CPU limit
```
k run cpu-demo --image=vish/stress --restart=Never --requests=cpu=0.5 --limits=cpu=1 -- -cpu 2
```
Specify a CPU request that is too big for your Nodes
```
k run cpu-demo --image=vish/stress --restart=Never --requests=cpu=100 --limits=cpu=100 --command -- -cpu 2
```
Check
```
k get po cpu-demo -ojson | jq -r '.status'
```
