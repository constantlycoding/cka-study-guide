Configure a volume for a Pod
```
k run random-number-generator --image=alpine --restart=Never -oyaml --dry-run --command -- /bin/sh -c "shuf -i 0-100 -n 1 >> /opt/number.out" > po-rng.yaml
vim po-rng.yaml
```
```
spec:
  containers:
  - volumeMounts:       # po.spec.containers.volumeMounts
    - name: data-volume
      mountPath: /opt
  volumes:              # po.spec.volumes
  - name: data-volume
    hostPath:
      path: /tmp
      type: Directory
```
```
k create -f po-rng.yaml
```
```
ssh node01
ls /tmp
```
