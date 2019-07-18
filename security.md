# Know how to configure authentication and authorization
# Understand Kubernetes security primitives
# Know to configure network policies.
# Create and manage TLS certificates for cluster components
CA

| Keys               |
|:------------------ |
| ca-key.pem, ca.pem |

Servers

| Component      | Node   | Keys                               |
|:-------------- |:------ |:---------------------------------- |
| kube-apiserver | master | apiserver-key.pem, apiserver.pem   |
| etcd           | master | etcdserver-key.pem, etcdserver.pem |
| kubelet        | worker | kubelet-key.pem, kubelet.pem       |

Clients

| Component       | Node   |  Keys                                            | Server         |
|:--------------- |:------ |:------------------------------------------------ |:-------------- |
| kubectl         | remote | admin-key.pem, admin.pem                         | kube-apiserver |
| kube-scheduler  | master | scheduler-key.pem, scheduler.pem                 | kube-apiserver |
| kube-controller | master | controller-key.pem, controller.pem               | kube-apiserver |
| kube-apiserver  | master | apiserver-etcd-key.pem, apiserver-etcd.pem       | etcd           |
| kube-apiserver  | master | apiserver-kubelet-key.pem, apiserver-kubelet.pem | kubelet        |
| kube-proxy      | worker | proxy-key.pem, proxy.pem                         | kube-apiserver |
| kubelet         | worker | kubelet-apiserver-key.pem, kubelet-apiserver.pem | kube-apiserver |

# Work with images securely
# Define security contexts
# Secure persistent key value store
