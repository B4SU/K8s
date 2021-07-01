# Kubernetes


K8s Cluster: Master & Slave

Can orchestrate container of any type

#### Overview

Kubernetes is a portable, extensible, open-source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation. It has a large, rapidly growing ecosystem. Kubernetes services, support, and tools are widely available.

Kubernetes Components
A Kubernetes cluster consists of the components that represent the control plane and a set of machines called nodes.

The Kubernetes API
The Kubernetes API lets you query and manipulate the state of objects in Kubernetes. The core of Kubernetes' control plane is the API server and the HTTP API that it exposes. Users, the different parts of your cluster, and external components all communicate with one another through the API server.

Working with Kubernetes Objects
Kubernetes objects are persistent entities in the Kubernetes system. Kubernetes uses these entities to represent the state of your cluster. Learn about the Kubernetes object model and how to work with these objects.




#### Architecture

Kubernetes environment consists of a control plane (master), a distributed storage system for keeping the cluster state consistent (etcd), and a number of cluster nodes (Kubelets).

![alt text][logo]

[logo]: https://platform9.com/wp-content/uploads/2019/05/kubernetes-constructs-concepts-architecture.jpg "K"

The control plane is made up of three major components: kube-apiserver, kube-controller-manager and kube-scheduler. All these can run on a single master node, or can be replicated across multiple master nodes for high availability. Control panel components make global decisions about the cluster (for example, scheduling), as well as detecting and responding to cluster events (for example, starting up a new pod when a deployment's replicas field is unsatisfied).
