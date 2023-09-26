---
title: "Kubernetes,Kubernetes Architecture"
datePublished: Tue Sep 26 2023 21:35:49 GMT+0000 (Coordinated Universal Time)
cuid: cln0u6vkp000108la6spe2ymq
slug: kuberneteskubernetes-architecture
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1695763033853/8740748e-469f-42c7-8fef-97f1793ddc8d.jpeg
tags: kubernetes, devops, devops-articles, 90daysofdevops, trainwithshubham

---

In this blog, I am going to discuss Kubernetes, Kubernetes Architecture, Kubernetes components, and its configuration.

# **Kubernetes**

Kubernetes is an open-source container orchestration platform that automates the deployment, scaling, and management of containerized applications.

Before I deep dive into this, here is the link to official Kubernetes documentation which supports and helps in troubleshooting almost all issues that arise: [**Kubernetes Documentation**](https://kubernetes.io/docs/home/).

# **Kubernetes Architecture**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1682438116016/4615f658-1561-40c1-99bb-fd623e109eaa.png?auto=compress,format&format=webp&auto=compress,format&format=webp align="left")

The Kubernetes Architecture consists of two nodes: Control Plane/Master Node and the Worker Node. The Master Node and the Worker Node together make the Kubernetes Cluster. Kubernetes is a distributed system.

In one Kubernetes Cluster, there can be only ***One*** control plane (Master Node), and one or more than one Worker Node.

***The control plane*** is responsible for managing and maintaining the overall state of the Kubernetes cluster.

***Worker nodes*** are the hosts that run the pods and the containers that make up the applications deployed in the Kubernetes cluster.

# **Kubernetes Components**

The components of Kubernetes can be classified as Control plan Components and Worker Node components.

## Control Plane Components ( Master Node)

The components of the Control Plane are API Server, etcd, kube-scheduler, and the kube-controller manager.

### API Server

The API server acts as the primary management point for the Kubernetes cluster. It is the front end of the Kubernetes Control Plane.

API Server can scale horizontally, which means for scaling it uses the deployment of instances.

It provides a REST API that enables users to interact with the cluster and manage its resources. It acts as the primary interface for users and external systems to interact with the cluster and perform actions such as creating or updating deployments, scaling applications, or monitoring the state of the cluster.

### etcd

etcd is a distributed key-value store that stores the configuration data for the Kubernetes cluster.

It stores information about the state of the cluster, such as the current status of the nodes and the configuration of the deployed applications.

etcd can scale horizontally. etcd ctl is a CLI tool to interact with etcd server.

### kube-scheduler

The kube-scheduler is responsible for scheduling pods on the worker nodes.

When a user creates a new pod or scales up an existing deployment, the kube-scheduler is responsible for selecting a suitable node for the pod to run on. It takes into account factors such as CPU RAM, resources required, data locality, and other policies to determine the best node to run a given pod.

Its primary role is to ensure that each pod is scheduled to run on an appropriate node that can satisfy its resource requirements and other constraints.

### kube-controller-manager

The kube-controller-manager is responsible for managing the controllers that maintain the desired state of the cluster.

It includes controllers such as the node controller, which manages the nodes in the cluster, and the replication controller, which manages the replication of pods. Cron jobs, deployment controller, persistent volume protection, etc. are all a part of kube-controller-manager.

## Worker Node Components

The components of the Worker Node are kubelet, kube-proxy, and Container Runtime.

### kubelet

The kubelet is responsible for managing the pods on the node.

It ensures that the containers in the pod are running and healthy, and communicates with the API server to receive instructions for managing the pods.

One needs to install the kubelet manually on worker nodes.

### kube-proxy

The kube-proxy is responsible for managing the network connectivity between the pods and other services in the cluster.

It performs load balancing and sets up network routes to enable communication between the pods.

It runs on each node, using IP Table rules so any services from outside can connect to the pods.

### Container Runtime

The container runtime, such as Docker, is responsible for running the containers that make up the pods.

When a pod is scheduled on a worker node, the Kubernetes kubelet communicates with the container runtime to start the containers that make up the pod. The container runtime is responsible for creating the containers and setting up their networking and storage resources, as well as monitoring their health and resource usage.

# Tasks

## Task 1: What is Kubernetes? Write in your own words. Why do we call it k8s?

Kubernetes is an open-source container orchestration platform developed by Google. It provides a way to automate the deployment, scaling, and management of containerized applications.

***What is Kubernetes according to me?*** Kubernetes is the container orchestration platform that is helping developers, and engineers over the world by making their jobs easy for maintaining and deploying containerized applications. Kubernetes also helps in scaling and is highly available. In Kubernetes, we define everything as a Manifest file, that is declarative files.

For example, in the IPL which we saw till last year on OTT (HotStar), the high user demand was all handled by Kubernetes.

***Why do we call it K8s?*** The number 8 represents the eight letters between the "K" and the "s" in "Kubernetes."

## Task 2: What are the benefits of using k8s?

* **Portability:** Kubernetes is a portable platform that can be used on-premises or in the cloud.
    
* **Scalability:** Kubernetes is a scalable platform that can be scaled horizontally to meet the needs of your applications.
    
* **Flexibility:** Kubernetes is a flexible platform that can be used to deploy a wide range of applications.
    
* **Efficiency:** Kubernetes is an efficient platform that uses resources effectively.
    
* **Security:** Kubernetes provides a secure platform for running applications.
    

## Task 3: Explain the architecture of Kubernetes.

Kubernetes architecture is based on the client-server model. The control plane is the server component, and it is responsible for managing the cluster. The nodes are the client components, and they are responsible for running the applications.

The control plane consists of the following components:

* **API server:** The API server is the main interface for interacting with Kubernetes. It exposes a RESTful API that can be used to create, update, and delete resources.
    
* **Scheduler:** The scheduler is responsible for assigning pods to nodes. It takes into account factors such as resource availability, node affinity, and pod anti-affinity when making scheduling decisions.
    
* **Controller manager:** The controller manager is responsible for running controllers. Controllers are responsible for managing the state of the cluster. For example, the replication controller ensures that a specified number of replicas of a pod are running.
    
* **Etcd:** Etcd is a key-value store that is used to store cluster data. This data includes things like the current state of the cluster, the configuration of the cluster, and the logs of the cluster.
    

The nodes in a Kubernetes cluster are responsible for running the applications. Each node has the following components:

* **Kubelet:** The kubelet is responsible for running pods on a node. It ensures that pods have the resources they need and that they are running correctly.
    
* **Kube-proxy:** The kube-proxy is responsible for routing traffic to pods. It uses the service definition to determine how to route traffic to pods.
    
* **Container runtime:** The container runtime is responsible for running containers. The most popular container runtime is Docker.
    

## Task 4: What is Control Plane?

The control plane is the part of the system that manages the cluster. It consists of the following components: API server, Scheduler, Controller Manager, etcd.

The control plane is responsible for keeping the cluster in a consistent state. It does this by monitoring the state of the cluster and taking corrective action when necessary. For example, if a pod fails, the controller manager will restart it. If a node goes down, the scheduler will assign the pods that were running on that node to other nodes.

## Task 5: Write the difference between kubectl and kubelet.

<table><tbody><tr><td colspan="1" rowspan="1"><p><strong>Feature</strong></p></td><td colspan="1" rowspan="1"><p><strong>kubectl</strong></p></td><td colspan="1" rowspan="1"><p><strong>kubelet</strong></p></td></tr><tr><td colspan="1" rowspan="1"><p>Type</p></td><td colspan="1" rowspan="1"><p>Command-line tool</p></td><td colspan="1" rowspan="1"><p>Daemon</p></td></tr><tr><td colspan="1" rowspan="1"><p>Location</p></td><td colspan="1" rowspan="1"><p>Local machine</p></td><td colspan="1" rowspan="1"><p>Node in cluster</p></td></tr><tr><td colspan="1" rowspan="1"><p>Communication</p></td><td colspan="1" rowspan="1"><p>With Kubernetes API server</p></td><td colspan="1" rowspan="1"><p>With Kubernetes API server</p></td></tr><tr><td colspan="1" rowspan="1"><p>Purpose</p></td><td colspan="1" rowspan="1"><p>To interact with the Kubernetes cluster</p></td><td colspan="1" rowspan="1"><p>To manage containers on the node</p></td></tr></tbody></table>

## Task 6: Explain the role of the API server.

The API server is a core component of the control plane in Kubernetes.

It acts as the primary interface for communication between various Kubernetes components and external entities. The API server exposes the Kubernetes API, which allows users, administrators, and other components to interact with the cluster.

Here are some of the key responsibilities of the API server:

* The API server is responsible for managing the overall state and configuration of the Kubernetes cluster.
    
* The API server handles user authentication and authorization.
    
* The API server acts as an endpoint for clients and other Kubernetes components to interact with the cluster. This allows users to create, update, and delete Kubernetes resources, as well as retrieve information about the cluster's state.
    
* The API server performs validation and admission control for incoming API requests.
    
* The API server interacts with the etcd key-value store, which serves as the cluster's data store.
    
* The API server manages the lifecycle of resources and provides a control loop for various controllers running within the control plane.
    

---

In this blog, I have discussed Kubernetes and its architecture. If you have any questions or would like to share your experiences, feel free to leave a comment below. Don't forget to read my blogs and connect with me on LinkedIn and let's have a conversation.

To help me improve my blog and correct my mistakes, I am available on LinkedIn as [**Mudit Mathur**](https://www.linkedin.com/in/mudit--mathur/). Do reach me and I am open to suggestions and corrections.

#Day30 #90daysofdevops