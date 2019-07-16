# Understand persistent volumes and know how to create them
```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv1
spec:
  capacity:
    storage: 5Gi
  accessModes:
  - ReadWriteOnce
  hostPath:
    path: /tmp
```
```
k get pv
```
# Understand access modes for volumes
| Mode          | Abbrev | Mounted as     |
| ------------- | -------| -------------- |
| ReadWriteOnce | RWO    | RW single node |
| ReadOnlyMany  | ROX    | RO many nodes  |
| ReadWriteMany | RWX    | RW many nodes  |
# Understand persistent volume claims primitive
```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: myclaim
spec:
  accessModes:
  - ReadWriteOnce
  resources:
    requests:
      storage: 8Gi
```
```
k get pvc
```
# Understand Kubernetes storage objects
# Know how to confifigure applications with persistent storage
```
kubectl create -f https://k8s.io/examples/pods/storage/redis.yaml --dry-run -oyaml > po-vol.yaml
```
