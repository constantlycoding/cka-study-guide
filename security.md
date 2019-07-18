# Know how to configure authentication and authorization
# Understand Kubernetes security primitives
# Know to configure network policies.
# Create and manage TLS certificates for cluster components
CA

| Keys               |
|:------------------ |
| ca-key.pem, ca.pem |

Servers

| Component      | Node   | Keys                               | hosts |
|:-------------- |:------ |:---------------------------------- |:----- |
| kube-apiserver | master | apiserver-key.pem, apiserver.pem   | hostname, Host_IP, advertise_IP, kubernetes, kubernetes.default, kubernetes.default.svc, kubernetes.default.svc.cluster, kubernetes.default.svc.cluster.local   |
| etcd           | master | etcdserver-key.pem, etcdserver.pem |       |
| kubelet        | worker | kubelet-key.pem, kubelet.pem       |       |

Clients

| Component       | Node   | Keys                                             | CN                             | O              | Server           |
|:--------------- |:------ |:------------------------------------------------ |:------------------------------ |:-------------- |:--------------- |
| kubectl         | remote | admin-key.pem, admin.pem                         | admin                          | system:masters | kube-apiserver |
| kube-scheduler  | master | scheduler-key.pem, scheduler.pem                 | system:kube-scheduler          |                | kube-apiserver |
| kube-controller | master | controller-key.pem, controller.pem               | system:kube-controller-manager |                | kube-apiserver |
| kube-apiserver  | master | apiserver-etcd-key.pem, apiserver-etcd.pem       |                                |                | etcd             |
| kube-apiserver  | master | apiserver-kubelet-key.pem, apiserver-kubelet.pem |                                |                | kubelet   |
| kube-proxy      | worker | proxy-key.pem, proxy.pem                         |                                |                | kube-apiserver |
| kubelet         | worker | kubelet-apiserver-key.pem, kubelet-apiserver.pem | system:node:<nodeName>         | system:nodes   | kube-apiserver |

# Work with images securely
# Define security contexts
# Secure persistent key value store
