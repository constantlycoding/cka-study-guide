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

# Configure Default, Minimum and Maximum Memory/CPU Requests and Limits for a Namespace
```
apiVersion: v1
kind: LimitRange
metadata:
  name: mem-limit-range
spec:
  limits:
  - default:
      memory: 512Mi
      cpu: 1
    defaultRequest:
      memory: 256Mi
      cpu: 0.5
    max:
      memory: 1Gi
      cpu: 800m
    min:
      memory: 500Mi
      cpu: 200m
    type: Container
```
# Configure Memory, CPU and Pod Quotas for a Namespace
```
k create quota my-quota --hard=cpu=1,memory=1G,pods=2
```
# Access Clusters Using the Kubernetes API
