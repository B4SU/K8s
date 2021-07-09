
### Node
A Pod always runs on a Node. A Node is a worker machine in Kubernetes and may be either a virtual or a physical machine, depending on the cluster. Each Node is managed by the Master. A Node can have multiple pods, and the Kubernetes master automatically handles scheduling the pods across the Nodes in the cluster. The Master's automatic scheduling takes into account the available resources on each Node.

Every Kubernetes Node runs at least:

Kubelet, a process responsible for communication between the Kubernetes Master and the Node; it manages the Pods and the containers running on a machine.
A container runtime (like Docker) responsible for pulling the container image from a registry, unpacking the container, and running the application.


```sh
kubeadm init --apiserver-advertise-address $(hostname -i) --pod-network-cidr 10.5.0.0/16

#1.  Initialize cluster networking
kubectl apply -f https://raw.githubusercontent.com/cloudnativelabs/kube-router/master/daemonset/kubeadm-kuberouter.yaml

#2.  Weave network
kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"

```

---
<br/>

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

```sh
kubectl create -f rs-defination.yml     # Create pods using replicaset defination file
kubectl describe rs <replicaset-name>   # Get details about the replicaset
```
```sh
kubectl get replicaset                  # List replicaset
kubectl get pods                        # List pods

# List pods with custom columns
kubectl get pods -o=custom-columns=PodName:.metadata.name,Containers:.spec.containers[*].name,Image:.spec.containers[*].image
```

---
<br/>

### Services
Services are the Kubernetes way of configuring a proxy to forward traffic to a set of pods.
A Service in Kubernetes is an abstraction which defines a logical set of Pods and a policy by which to access them. Services enable a loose coupling between dependent Pods. The set of Pods targeted by a Service is usually determined by a LabelSelector.

Although each Pod has a unique IP address, those IPs are not exposed outside the cluster without a Service. Services allow your applications to receive traffic. Services can be exposed in different ways by specifying a type in the ServiceSpec:

- ClusterIP (default) - Exposes the Service on an internal IP in the cluster. This type makes the Service only reachable from within the cluster.
- NodePort - Exposes the Service on the same port of each selected Node in the cluster using NAT. Makes a Service accessible from outside the cluster using <NodeIP>:<NodePort>. Superset of ClusterIP.
- LoadBalancer - Creates an external load balancer in the current cloud (if supported) and assigns a fixed, external IP to the Service. Superset of NodePort.
- ExternalName - Maps the Service to the contents of the externalName field (e.g. `foo.bar.example.com`), by returning a CNAME record with its value. No proxying of any kind is set up. This type requires v1.7 or higher of kube-dns, or CoreDNS version 0.0.8 or higher.


#### NodePort
```yaml
# Manifest file svc1.yml

apiVersion: v1
kind: Service
metadata:
  name: mysvc
spec:
  type: NodePort
  ports:
    - targetPort: 80    # POD port
      port: 80          # Service port
      nodePort: 30001   # Node port
  selector:
    type: WebServer
```

```sh
# Create service  object of type nodeport
kubectl create -f svc1.yml
```


#### LoadBalancer
```yaml
# Manifest file svc2.yml
apiVersion: v1
kind: Service
metadata:
  name: mysvc
spec:
  type: LoadBalancer
  ports:
    - targetPort: 80    # POD port
      port: 80          # Service port
  selector:
    type: WebServer

```

```sh
# Create service  object of type nodeport
kubectl create -f svc2.yml
```

---
<br/>


### Deployments


```sh
# Create service using deployment.yml
kubectl create -f deployment.yml


# RollingUpdate of version
kubectl set image deploy kubeserve app=leaddevops/kubeserve:v2


# Check rollout history
kubectl rollout history deployment kubeserve

# Rollback to previous version
kubectl rollback undo deployment kubeserve

# Rollback to particular version
kubectl rollback undo deployment kubeserve --to-revision=1

```

---
<br/>


### Dashboard

```sh
#
kubectl create -f dashboard.yml
```


---
<br/>
