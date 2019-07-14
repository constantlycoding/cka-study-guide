# Understand Deployments and how to perform rolling updates and rollbacks
* Create deployment creates replicaset automatically, triggers rollout, creates new deployment version
```
k run nginx --image=nginx
```
```
k get deploy
k get deploy nginx -ojson | jq -r '.spec.strategy.type'
k get rs
```
Updates
* Update deployment creates new replicaset, brings down old replicaset
```
# Make change to deployment definition file
k apply -f nginx-deploy.yaml
```
```
k edit deploy nginx
```
```
k set image deploy nginx nginx=nginx:1.9.1
```
Status
```
k rollout status deploy nginx
k rollout history deploy nginx
k get rs
```
Rollback
* Rollback deployment brings down new replicaset, brings up old replicaset
```
k rollout undo deploy nginx
```
# Know various ways to configure applications
# Know how to scale applications
# Understand the primitives necessary to create a self-healing application
