# Kubernetes

### **Overview**

Kubernetes is a portable, extensible, open-source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation. It has a large, rapidly growing ecosystem. Kubernetes services, support, and tools are widely available.

Kubernetes Components
A Kubernetes cluster consists of the components that represent the control plane and a set of machines called nodes.

The Kubernetes API
The Kubernetes API lets you query and manipulate the state of objects in Kubernetes. The core of Kubernetes' control plane is the API server and the HTTP API that it exposes. Users, the different parts of your cluster, and external components all communicate with one another through the API server.

Working with Kubernetes Objects
Kubernetes objects are persistent entities in the Kubernetes system. Kubernetes uses these entities to represent the state of your cluster. Learn about the Kubernetes object model and how to work with these objects.

---


### **Architecture**

Kubernetes environment consists of a control plane (master), a distributed storage system for keeping the cluster state consistent (etcd), and a number of cluster nodes (Kubelets).

<br/>

![alt text][logo]

[logo]: https://platform9.com/wp-content/uploads/2019/05/kubernetes-constructs-concepts-architecture.jpg "K"



#### **Control Plane**

The control plane is made up of three major components: kube-apiserver, kube-controller-manager and kube-scheduler. All these can run on a single master node, or can be replicated across multiple master nodes for high availability. Control plane components make global decisions about the cluster (for example, scheduling), as well as detecting and responding to cluster events (for example, starting up a new pod when a deployment's replicas field is unsatisfied).

<br/>

___
##### **API Server (kube-apiserver)**
The API server is the front end for the Kubernetes control plane, it acts as the gateway to the cluster, hence it must be accessible by clients from outside the cluster. Clients authenticate via the API Server, and also use it as a proxy/tunnel to nodes and pods (and services). It also provides api to support for lifecycle orchestration (scaling, updates, and so on) for different types of applications.
kube-apiserver is designed to scale horizontally, it scales by deploying more instances.

<br/>

##### **Controller Manager (kube-controller-manager)**
Control Plane component that runs controller processes.
Logically, each controller is a separate process, but to reduce complexity, they are all compiled into a single binary and run in a single process.

Some types of these controllers are:
- Node controller: Responsible for noticing and responding when nodes go down.
- Job controller: Watches for Job objects that represent one-off tasks, then creates Pods to run those tasks to completion.
- Endpoints controller: Populates the Endpoints object (that is, joins Services & Pods).
- Service Account & Token controllers: Create default accounts and API access tokens for new namespaces.

The Controller Manager is a daemon that runs the core control loops, watches the state of the cluster, and makes changes to drive status toward the desired state.

<br/>

##### **Cloud Controller Manager (cloud-controller-manager)**

The Cloud Controller Manager integrates into each public cloud for optimal support of availability zones, VM instances, storage services, and network services for DNS, routing and load balancing. The cloud-controller-manager only runs controllers that are specific to the cloud provider. The cloud-controller-manager combines several logically independent control loops into a single binary that you run as a single process

<br/>

##### **Scheduler (kube-scheduler)**
Control plane component that watches for newly created Pods with no assigned node, and selects a node for them to run on.
Factors taken into account for scheduling decisions include: individual and collective resource requirements, hardware/software/policy constraints, affinity and anti-affinity specifications, data locality, inter-workload interference, and deadlines.

<br/>

##### **etcd**
Consistent and highly-available key value store used as Kubernetes' backing store for all cluster data.

___

#### **Cluster Nodes**
Cluster nodes are machines that run containers and are managed by the master nodes.

**Node Components**
- kubelet :
  An agent that runs on each node in the cluster. It makes sure that containers are running in a Pod.
  The kubelet takes a set of PodSpecs that are provided through various mechanisms and ensures that the containers described in those PodSpecs are running and healthy. The kubelet doesn't manage containers which were not created by Kubernetes.

- kube-proxy :
  kube-proxy is a network proxy that runs on each node in your cluster, implementing part of the Kubernetes Service concept. kube-proxy maintains network rules on nodes. These network rules allow network communication to Pods from network sessions inside or outside of the cluster.

  <br/>

**Container runtime**
The container runtime is the software that is responsible for running containers.

Kubernetes supports several container runtimes: Docker, containerd, CRI-O, and any implementation of the Kubernetes CRI (Container Runtime Interface).


<br/>

Additional information
https://kubernetes.io/docs/concepts/overview/components/#addons


---
