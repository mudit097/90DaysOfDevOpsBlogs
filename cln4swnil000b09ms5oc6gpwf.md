---
title: "Namespaces and Services in Kubernetes"
datePublished: Fri Sep 29 2023 16:10:57 GMT+0000 (Coordinated Universal Time)
cuid: cln4swnil000b09ms5oc6gpwf
slug: namespaces-and-services-in-kubernetes
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696003672594/65ee1ce2-4fed-4ee7-91b7-0bd573a7a82e.jpeg
tags: aws, kubernetes, devops, 90daysofdevops, trainwithshubham

---

# **Define Namespaces**

* A namespace is a way to partition and isolate resources within a cluster. It provides a virtual cluster within a physical cluster, allowing multiple teams or applications to coexist without interfering with each other.
    
* Namespaces can contain pods, services, deployments, and other Kubernetes objects, and each namespace has a unique name within the cluster.
    
* By default, all objects are created in the “default” namespace, but administrators can create additional namespaces and apply resource quotas, network policies, and access controls to them.
    
* Namespaces also facilitate resource management, monitoring, and troubleshooting, making it easier to organize, secure, and scale Kubernetes deployments.
    

# **Benefits of Having Namespace in Cluster**

1. **Resource Organization:** Namespaces provide a logical grouping mechanism to organize resources within a cluster.

2. **Resource Isolation:** Namespaces provide a way to isolate and segregate resources within a cluster. This isolation prevents resource conflicts and allows for better resource utilization and management.

3\. **Multi-tenancy:** Namespaces enable multi-tenancy within a Kubernetes cluster. Different teams or users can have their own dedicated namespaces, providing them with separate environments to deploy and manage their applications.

4\. **Access Control:** Namespaces provide a mechanism for access control and RBAC (Role-Based Access Control) within a cluster. By assigning appropriate roles and permissions at the namespace level, you can control who can create, view, or modify resources within a particular namespace.

5. **Resource Quotas:** Namespaces allow you to set resource quotas to limit the amount of CPU, memory, and storage that can be consumed within a namespace.

6\. **Namespace Scoping:** Some Kubernetes resources, such as services, secrets, and config maps, are scoped to a namespace. This means they are only accessible and visible within the same namespace where they are created.

# **Commonly Used Commands for Namespace**

1. To get all namespaces
    

```plaintext
 kubectl get namespaces
```

![](https://miro.medium.com/v2/resize:fit:875/1*oQd1Vy9C_dSBlwG-pBdSCQ.png align="left")

2\. To get all system-related pods running in namespace “kube-system”.

```plaintext
 kubectl get pods -n=kube-system
```

![](https://miro.medium.com/v2/resize:fit:875/1*OBatbA_xkGxFncw8DdxwLw.png align="left")

3\. If you didn’t mention any namespace, the pod will be stored in the default namespace

```plaintext
 kubectl get namespaces -n=default
```

![](https://miro.medium.com/v2/resize:fit:875/1*IU7k7KC-Q5M_fV7QIszIAA.png align="left")

4\. To create a new namespace

```plaintext
 kubectl create namepspace <name>
```

# **Services in k8s**

* A Service is an abstraction that defines a logical set of Pods and a policy by which to access them. It provides a stable IP address and DNS name for a set of Pods, allowing them to be accessed by other parts of the application or by external users.
    
* Services can be configured to provide load balancing, service discovery, and proxying to backends running on different ports or nodes within a cluster. They can also be used to provide access to external resources or to expose applications running inside the cluster to external users.
    
* Services are an essential component of Kubernetes networking and are widely used in microservices architectures.
    

# **Benefits of Having Services**

Services are used in Kubernetes for several reasons:

1.**Load balancing:** Services provide a single, stable IP address and DNS name for a set of Pods, distributing traffic among them and ensuring that requests are handled by healthy instances.

2.**Service discovery:** Services allow other parts of the application to discover and communicate with Pods, even if their IP addresses change due to scaling or failure.

3.**Port mapping:** Services enable backends running on different ports or nodes to be accessed through a single, well-known port or endpoint, simplifying configuration and management.

4.**External access:** Services can be used to expose applications running inside the cluster to external users or to provide access to external resources, such as databases or APIs.

# **Types of Service in K8s**

In Kubernetes, different types of services enable connectivity and load balancing to pods and applications:

1. **ClusterIP:** Exposes the service on a cluster-internal IP, allowing communication within the cluster.

2\. **NodePort:** Exposes the service on a static port on each node’s IP, enabling external access to the service.

3\. **LoadBalancer:** Automatically provisions an external load balancer (e.g., cloud provider’s load balancer) to distribute traffic to the service.

4\. **ExternalName:** Maps the service to an external DNS name, allowing direct access to external services without a cluster IP.

Read **Task 2** to know more about the types of services in K8s.

# **Task 1:**

1. Create a Namespace for your Deployment
    

Use the command `kubectl create namespace <namespace-name>` to create a Namespace

```plaintext
 kubectl create namespace my-django-app

 # List out all the name space
 kubectl get namespace
```

![](https://miro.medium.com/v2/resize:fit:875/1*bpM0Yz5cxVWp01AsynJbZg.png align="left")

2\. Update the deployment.yml file to include the Namespace

```plaintext
 apiVersion: apps/v1
 kind: Deployment
 metadata:
   name: my-django-app-deployment
   namespace: my-django-app
 spec:
   replicas: 2
   selector:
     matchLabels:
       app: django-app
   template:
     metadata:
       labels:
         app: django-app
     spec:
       containers:
       - name: django-app-deployment
         image: mudit097/django-todo:latest
         ports:
         - containerPort: 8000
```

![](https://miro.medium.com/v2/resize:fit:875/1*pv_yUHyXniLZshNvfbsqdQ.png align="left")

3\. Apply the updated deployment using the command: `kubectl apply -f deployment.yml`

```plaintext
 kubectl apply -f deployment.yml
```

![](https://miro.medium.com/v2/resize:fit:875/1*lYDbs7-fqXbr3rYMuYcQaA.png align="left")

4\. Verify that the Namespace has been created by checking the status of the Namespaces in your cluster.

```plaintext
 kubectl get pods -n=my-django-app
```

![](https://miro.medium.com/v2/resize:fit:875/1*hMRTWTQPtStkW_lq_KRoPA.png align="left")

5\. We can scale the pod by modifying the number of the replicas in the deployment

```plaintext
 kubectl scale deployment my-django-app-deployment --replicas=10 -n=my-django-app
```

![](https://miro.medium.com/v2/resize:fit:875/1*_GkYONAGiONDjIafEwh6Zw.png align="left")

# **Task 2:**

# **Cluster IP**

* ClusterIP is a type of Kubernetes Service that provides a stable IP address and DNS name for a set of Pods within a cluster. When a ClusterIP Service is created, Kubernetes assigns a virtual IP address to the Service, which can be used by other parts of the application to access the Pods.
    
* The ClusterIP is accessible only from within the cluster and is not exposed to the external network. It enables seamless communication between different services and pods within the cluster without the need for exposing them to the outside world.
    
* To use a ClusterIP Service, other parts of the application can simply use the Service’s DNS name, along with the assigned port number, to access the Pods. Kubernetes ensures that traffic sent to the Service’s IP address is distributed among the available Pods, based on the configured load-balancing algorithm.
    
* ClusterIP is commonly used for internal microservice-to-microservice communication and internal service discovery within the Kubernetes cluster.
    

# **NodePort**

* NodePort is a type of Kubernetes Service that exposes a specific port on each node in the cluster and routes traffic to a Service. When a NodePort Service is created, Kubernetes automatically assigns a random port in the range of 30000–32767 to the Service.
    
* NodePort is typically used to expose a Service externally, either to the Internet or to other services outside the cluster. For example, a web application Service could be exposed using a NodePort, allowing users to access the application using the IP address of any node in the cluster, along with the assigned port number.
    
* To use a NodePort Service, the client must connect to the IP address of a node in the cluster, along with the assigned port number. Kubernetes ensures that traffic sent to this port is routed to the appropriate Pod, based on the configured load-balancing algorithm.
    

# **Load Balancing**

* Load balancing in Kubernetes is the process of distributing network traffic across multiple Pods to ensure that requests are handled efficiently and reliably. It is achieved through the use of a Kubernetes Service, which provides a stable IP address and DNS name for a set of Pods.
    
* Load balancing in Kubernetes is essential for ensuring the high availability and scalability of applications, particularly in microservices architectures where many small, independently deployable services may be running on different nodes in the cluster.
    
* By distributing traffic across multiple instances, load balancing helps to prevent overload and ensures that requests are processed quickly and reliably. It also allows for seamless scaling of applications by adding or removing Pods without affecting the overall performance of the application.
    
* Kubernetes supports several load-balancing algorithms, including round-robin, least connections, and IP Hash, which can be configured to suit the specific needs of the application.
    

# **Networking**

* Networking in Kubernetes is the process of connecting Pods and Services within a cluster to enable communication between them. Kubernetes provides a flexible and extensible networking model that allows developers to build complex applications with ease.
    
* To enable communication between Pods and Services, Kubernetes uses a network overlay, such as Calico, Flannel, or Weave Net, which provides virtual network interfaces and routing rules to connect Pods and Services across nodes in the cluster.
    
* Kubernetes networking uses a flat, shared network space, with each Pod assigned a unique IP address within the cluster. Pods can communicate with each other directly using these IP addresses, without the need for port mapping or NAT.
    

In this blog, we delved into the world of Kubernetes namespaces, shedding light on their significance within a cluster. We also explored the various benefits of incorporating namespaces into your Kubernetes environment, as well as some commonly used commands for managing them effectively.

Moving forward, we shifted our focus to Kubernetes services, a fundamental component for facilitating communication between different parts of your application. We discussed the advantages of implementing services within your cluster and outlined the different types of services available, including Cluster IP, NodePort, and Load Balancing.

In Task 1 and Task 2, we encountered practical scenarios where namespaces and services can be invaluable tools for managing and organizing your Kubernetes resources efficiently.

As you continue to explore Kubernetes, keep in mind that namespaces and services play pivotal roles in ensuring the scalability, security, and reliability of your applications. Whether you’re a seasoned Kubernetes pro or just starting your DevOps journey, these concepts are essential for mastering container orchestration.

If you have any questions or would like to share your experiences, please don’t hesitate to leave a comment below. Stay tuned for more insightful blogs, and feel free to connect with me on LinkedIn for further discussions. I’m always open to feedback and eager to hear your suggestions for improving my content. You can find me on LinkedIn as [Mudit Mathur](https://www.linkedin.com/in/mudit--mathur/). Reach out anytime; I’d love to hear from you!

#Day33 #90daysofdevops