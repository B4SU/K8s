
### Node
A Pod always runs on a Node. A Node is a worker machine in Kubernetes and may be either a virtual or a physical machine, depending on the cluster. Each Node is managed by the Master. A Node can have multiple pods, and the Kubernetes master automatically handles scheduling the pods across the Nodes in the cluster. The Master's automatic scheduling takes into account the available resources on each Node.

Every Kubernetes Node runs at least:

Kubelet, a process responsible for communication between the Kubernetes Master and the Node; it manages the Pods and the containers running on a machine.
A container runtime (like Docker) responsible for pulling the container image from a registry, unpacking the container, and running the application.



### PODs
A Pod is a Kubernetes abstraction that represents a group of one or more application containers (such as Docker), and some shared resources for those containers. A Pod models an application-specific "logical host" and can contain different application containers which are relatively tightly coupled. Pods are the atomic unit on the Kubernetes platform. When we create a Deployment on Kubernetes, that Deployment creates Pods with containers inside them (as opposed to creating containers directly). Each Pod is tied to the Node where it is scheduled, and remains there until termination (according to restart policy) or deletion. In case of a Node failure, identical Pods are scheduled on other available Nodes in the cluster.



|    Commands                   | Purpose                                                 |
|-------------------------------|---------------------------------------------------------|
|kubectl get nodes              | List nodes                                              |
|kubectl get pods               | List pods                                               |
|kubectl get pods -o wide       | List all pods with more information (such as node name) |
|kubectl get pod -l env=QA      | List all pods with label env=QA                         |


```sh
# Create basic pod using image
kubectl run n1 --image nginx
```

```sh
# Create pod from yaml file
# POD defination file only allow to create a single pod
kubectl create -f pod-defination.yml

# See details about configured pod
kubectl describe pod mypod
```

```sh
# View manifest file of an existing image
kubectl run pod2 --image nginx --dry-run=client -o yaml
```

```sh
# Delete pod 
kubectl delete pod mypod
```




#### Replicaset

ReplicaSet ensures that a specified number of pod replicas are running at any given time.
