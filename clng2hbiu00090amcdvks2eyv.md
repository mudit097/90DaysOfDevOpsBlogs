---
title: "Amazon ECS — Elastic Container Service"
datePublished: Sat Oct 07 2023 13:24:25 GMT+0000 (Coordinated Universal Time)
cuid: clng2hbiu00090amcdvks2eyv
slug: amazon-ecs-elastic-container-service
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696684732340/27a4cdcc-e92a-4e01-9572-d3544d74bfde.png
tags: aws, devops, aws-fargate, 90daysofdevops, trainwithshubham

---

This blog will discuss ECS — Elastic Container Service by AWS. Let’s jump into it.

# **ECS**

ECS or Amazon Elastic Container Service is a highly scalable container orchestration service provided by Amazon Web Services. It allows you to run and manage Docker containers on a cluster of EC2 instances or using AWS Fargate, a serverless compute engine for containers.

# **Amazon ECS Layers:**

![](https://miro.medium.com/v2/resize:fit:875/0*BiT1rF6NdLdJ4GTB.png align="left")

* Capacity — The infrastructure where your containers run
    
* Controller — Deploy and manage your applications that run on the containers
    
* Provisioning — The tools that you can use to interface with the scheduler to deploy and manage your applications and containers
    

# **ECS Application Lifecycle**

![](https://miro.medium.com/v2/resize:fit:875/0*8EhN7Qm7MsscfSNY.png align="left")

The application lifecycle in Amazon ECS (Elastic Container Service) involves the management of tasks and services throughout their lifecycle.

1. Task Definition Creation: The application lifecycle starts with creating a task definition. A task definition is a blueprint that defines how containers should run within ECS.
    
2. Task Scheduling: Once a task definition is created, tasks based on that definition can be scheduled on ECS container instances or as Fargate tasks.
    
3. Task Execution: When a task is scheduled to run, ECS provisions the necessary resources, such as EC2 instances or Fargate resources, to host the containers.
    
4. Task Monitoring: During task execution, you can monitor the health and resource utilization of tasks using Amazon CloudWatch.
    
5. Task Updates: If you need to update a running task, you can create a new task definition version with the desired changes and update the service to use the new version.
    
6. Scaling: ECS provides scaling capabilities to manage the number of tasks running in a service.
    
7. Service Management: Services in ECS provide higher-level abstractions for managing long-running tasks.
    
8. Task Termination: When a task is no longer needed or needs to be stopped, you can manually terminate the task or update the service to a desired count of zero.
    

# **Common use cases in Amazon ECS**

Fargate is suitable for the following workloads:

* Large workloads that need to be optimized for low overhead
    
* Small workloads that have the occasional burst
    
* Tiny workloads
    
* Batch workloads
    

EC2 is suitable for the following workloads:

* Workloads that require consistently high CPU core and memory usage
    
* Large workloads that need to be optimized for price
    
* Your applications need to access persistent storage
    
* You must directly manage your infrastructure
    

ECS also integrates with other AWS services, such as Elastic Load Balancing, Auto Scaling, and Amazon VPC, allowing you to build scalable and highly available applications. Additionally, ECS has support for Docker Compose and Kubernetes, making it easy to adopt existing container workflows.

# **Difference between EKS and ECS**

<table><tbody><tr><td colspan="1" rowspan="1"><p><strong>Feature</strong></p></td><td colspan="1" rowspan="1"><p><strong>EKS</strong></p></td><td colspan="1" rowspan="1"><p><strong>ECS</strong></p></td></tr><tr><td colspan="1" rowspan="1"><p>Architecture</p></td><td colspan="1" rowspan="1"><p>Distributed architecture. The Kubernetes control plane is distributed across multiple EC2 instances.</p></td><td colspan="1" rowspan="1"><p>Centralized architecture. There is a control plane that manages the scheduling of containers on EC2 instances.</p></td></tr><tr><td colspan="1" rowspan="1"><p>Managed Kubernetes</p></td><td colspan="1" rowspan="1"><p>Yes</p></td><td colspan="1" rowspan="1"><p>No</p></td></tr><tr><td colspan="1" rowspan="1"><p>Custom orchestration engine</p></td><td colspan="1" rowspan="1"><p>No</p></td><td colspan="1" rowspan="1"><p>Yes</p></td></tr><tr><td colspan="1" rowspan="1"><p>Autoscaling</p></td><td colspan="1" rowspan="1"><p>Supports autoscaling of pods and nodes (based on demand)</p></td><td colspan="1" rowspan="1"><p>Supports autoscaling of pods (configure scaling policies for your tasks and services)</p></td></tr><tr><td colspan="1" rowspan="1"><p>Deployment Flexibility</p></td><td colspan="1" rowspan="1"><p>More flexible with multi-region deployments, hybrid deployments, and custom configurations</p></td><td colspan="1" rowspan="1"><p>Flexible deployment options with EC2 or Fargate launch types</p></td></tr><tr><td colspan="1" rowspan="1"><p>Community Support</p></td><td colspan="1" rowspan="1"><p>Large and active Kubernetes community</p></td><td colspan="1" rowspan="1"><p>ECS has a growing community, but smaller than Kubernetes</p></td></tr><tr><td colspan="1" rowspan="1"><p>Container Compatibility</p></td><td colspan="1" rowspan="1"><p>Supports both Docker containers and other container runtimes compatible with Kubernetes</p></td><td colspan="1" rowspan="1"><p>Supports Docker containers</p></td></tr><tr><td colspan="1" rowspan="1"><p>Networking</p></td><td colspan="1" rowspan="1"><p>Kubernetes-native networking (Kubernetes Service Discovery, Ingress, etc.)</p></td><td colspan="1" rowspan="1"><p>Load Balancer integration, service discovery, network modes</p></td></tr><tr><td colspan="1" rowspan="1"><p>Monitoring and logging</p></td><td colspan="1" rowspan="1"><p>Supports built-in monitoring and logging</p></td><td colspan="1" rowspan="1"><p>Supports integration with CloudWatch</p></td></tr><tr><td colspan="1" rowspan="1"><p>Control plane</p></td><td colspan="1" rowspan="1"><p>Managed by AWS</p></td><td colspan="1" rowspan="1"><p>Managed by you</p></td></tr><tr><td colspan="1" rowspan="1"><p>Worker nodes</p></td><td colspan="1" rowspan="1"><p>Managed by AWS</p></td><td colspan="1" rowspan="1"><p>Managed by you</p></td></tr></tbody></table>

# **Task: Set up ECS (Elastic Container Service) by setting up Nginx on ECS.**

Let us do this task step by step.

# **Set up an ECS Cluster**

AWS Console &gt; Navigate to ECS &gt; On the left panel, click on Clusters

![](https://miro.medium.com/v2/resize:fit:875/1*njS-_OviQba_AIgN8Q3TNQ.png align="left")

Create Cluster &gt; Give Cluster name NginxCluster &gt; Let the Networking be default &gt; And by default Infrastructure AWS Fargate (Serverless) is selected

![](https://miro.medium.com/v2/resize:fit:875/1*r2vei4S8KQwMdC01tavWLw.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*5umNzp-HOcpS2lHQFn6ucQ.png align="left")

Click on Create.

![](https://miro.medium.com/v2/resize:fit:875/1*F-PqIIY5G0uWGSGCze_cFQ.png align="left")

# **Create a Task Definition**

In the left Panel of ECS &gt; Select Task Definitions

![](https://miro.medium.com/v2/resize:fit:875/1*4B8CwzVwyt5W4sqIHZpD8A.png align="left")

Click on Create new task definitions &gt; Create new task definition

![](https://miro.medium.com/v2/resize:fit:875/1*Fw6F2H7vxLyEVdP7XudjEQ.png align="left")

# **Configure task definition and containers**

Task definition family: nginx-task

Under Container details:

Name: nginx-container

Image URI: [public.ecr.aws/nginx/nginx:mainline-apline](http://public.ecr.aws/nginx/nginx:mainline-apline)

You can get this Image URL from [Amazon ECR Public Gallery](https://gallery.ecr.aws/).

Let other things be as it is and click on default.

# **Configure environment, storage, monitoring, and tags**

I am letting the app environment by default which is AWS Fargate.

Let other default things be as it is and click on Next.

# **Review and create**

Review the configuration and click on Create Task Definition.

![](https://miro.medium.com/v2/resize:fit:875/1*hAbXT3FvDl4goqlTZFicRg.png align="left")

# **Create a Service**

Go to ECS &gt; Select & open the Cluster you created.

Click on Create which is next to Services.

![](https://miro.medium.com/v2/resize:fit:875/1*_ZaWkh5mG7K2ar534s7rsg.png align="left")

Let the Environment section be the default.

In the Deployment Configuration section &gt; Select Service &gt; Give the Service Name &gt; Select the task definition you created.

![](https://miro.medium.com/v2/resize:fit:875/1*WSe21vJ-K4VSH0Wz50-J6Q.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*DMxCqeB2vO2lkDbmJl-rIA.png align="left")

In the Networking Tab &gt; Let the things be default except for SG &gt; Click on Create new SG.

Security group name: nginx-SG

Security group description: Security Group for Nginx Cluster

And configure the SG as below:

![](https://miro.medium.com/v2/resize:fit:875/1*3KrXNa61Nahw6AiUEuU9Zw.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*s6hdhR16p6x6ofCHBjryPA.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*I_KlULqOHcxPcKLUn8kG1A.png align="left")

Click on Create.

![](https://miro.medium.com/v2/resize:fit:875/1*BIGFS4w0nI_xpAH9RxZSSQ.png align="left")

Let’s test by accessing the Nginx container using the Public IPv4 of Fargate.

![](https://miro.medium.com/v2/resize:fit:875/1*t7firvTcmezqsRQE-AtW9Q.png align="left")

> *For the IP go to the Tasks tab in the ECS Cluster dashboard &gt; Select the Task number of your task required &gt; You can find the Public IPv4.*

![](https://miro.medium.com/v2/resize:fit:875/1*M9-eyvJKK6bcb_K3xCWy2A.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*ycWf_AQDvVjBO0zUtngmUw.png align="left")

This can be further done by exposing Nginx publicly, by setting up an Application Load Balancer (ALB). And then can be reached by the public IP address of your load balancer.

In this blog, I have explained ECS and set up an Nginx cluster in ECS. If you have any questions or want to share your experiences, please comment below. Don’t forget to read my blogs and connect with me on LinkedIn and let’s have a conversation.

To help me improve my blog and correct my mistakes, I am available on LinkedIn as [Mudit Mathur.](https://www.linkedin.com/in/mudit--mathur/) Do reach me and I am open to suggestions and corrections.

#Day48 #90daysofdevops