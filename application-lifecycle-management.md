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
Command and Arguments on applications
* Docker `CMD` will be replaced by command line parameters
* Docker `ENTRYPOINT` will be prepended to command line parameters
* Docker `CMD` will be appended to `ENTRYPOINT`
* Docker default `CMD` will be replaced by command line parameters
* Docker `ENTRYPOINT` can be replaced with `--entrypoint` option
* Pod definition `args` overwrites DockerFile `CMD`
* Pod definition `command` overwrites DockerFile `ENTRYPOINT`
```
k get po ubuntu-sleeper -ojson | jq -r '.spec.containers[0].command'
k get po ubuntu-sleeper -ojson | jq -r '.spec.containers[0].args'
```
Environment Variables
```
k get po ubuntu-sleeper -ojson | jq -r '.spec.containers[0].env'
```
```
env
- name: APP_COLOUR
  value: PINK
```
```
env
- name: APP_COLOUR
  valueFrom:
    configMapKeyRef:
```
```
env
- name: APP_COLOUR
  valueFrom:
    secretMapKeyRef:
```
ConfigMaps
```
k create cm app-config --from-literal=APP_COLOUR=BLUE
k create cm app-config --from-literal=APP_COLOUR=BLUE --from-literal=APP_MOD=prod
k create cm app-config --from-file=app.config
```
```
envFrom
- configMapRef:
    name: app-config
```
```
env
- name: APP_COLOUR
  valueFrom:
    configMapKeyRef:
      name: app-config
      key: APP_COLOUR
```
```
volumes
- name: app-volume
  configMap:
      name: app-config
```
Secrets
```
k create secret generic app-secret --from-literal=DB_HOST=mysql
k create secret generic app-secret --from-literal=DB_HOST=mysql --from-literal=DB_USER=root
k create secret generic app-secret --from-file=app.secret
```
```
envFrom
- secretRef:
    name: app-secret
```
```
env
- name: DB_HOST
  valueFrom:
    secretKeyRef:
      name: app-secret
      key: DB_HOST
```
```
volumes
- name: app-volume
  secret:
      secretName: app-secret
```
Encode
```
echo -n 'mysql' | base64
```
Decode
```
echo -n 'bXIzcWw=' | base64 --decode
```
# Know how to scale applications
# Understand the primitives necessary to create a self-healing application
