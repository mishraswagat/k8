kubectl get node --> lists all nodes
kubectl get ns --> lists all namespace
kubectl get all --> get all pods
kubectl get pods -n kube-system --> show pods from specific namespace

What is pod ? 
Pod in the smallest unit in k8s, we cant run a container in k8s, we need a wrapper and wrapper called as pod.
The pod can have 1 or more container but ideally it should be 1 pod for 1 container.

What is namespace ?
Namespace is a logical separation of k8s services. (pod is a service)
All the k8s own system pods are under kube-system namespace, if we don't define any namespace it will show us the default namespace.

How to define namespace ?
kubectl get pods -n kube-system

