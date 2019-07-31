# Assign Memory/CPU Resources to Containers and Pods
```
k run nginx --image=nginx --restart=Never --requests='cpu=100m,memory=256Mi' --limits='cpu=200m,memory=512Mi'
```
# Configure a Pod to Use a Volume for Storage
```
apiVersion: v1
kind: Pod
metadata:
  name: redis
spec:
  containers:
  - name: redis
    image: redis
    volumeMounts:            # po.spec.containers.volumeMounts
    - name: redis-storage
      mountPath: /data/redis
  volumes:                   # po.spec.volumes
  - name: redis-storage
    emptyDir: {}
```
# Configure a Pod to Use a PersistentVolume for Storage
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
kind: Pod
apiVersion: v1
metadata:
  name: task-pv-pod
spec:
  volumes:                        # po.spec.volumes
    - name: task-pv-storage
      persistentVolumeClaim:
        claimName: task-pv-claim
  containers:
    - name: task-pv-container
      image: nginx
      ports:
        - containerPort: 80
          name: "http-server"
      volumeMounts:               # po.spec.containers.volumeMounts
        - mountPath: "/usr/share/nginx/html"
          name: task-pv-storage
```
# Configure a Security Context for a Pod or Container
# Configure Service Accounts for Pods
```
k create sa myuser
k run nginx --image=nginx --restart=Never --serviceaccount=myuser
```
# Pull an Image from a Private Registry
# Assign Pods to Nodes
# Configure Pod Initialization
# Configure a Pod to Use a ConfigMap

