---
title: "Setting up an Application Load Balancer with AWS EC2"
datePublished: Mon Oct 02 2023 22:26:32 GMT+0000 (Coordinated Universal Time)
cuid: cln9gn7y2000509lg4oycc1gj
slug: setting-up-an-application-load-balancer-with-aws-ec2
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696285472913/82146139-1abc-4e11-96cd-9f1d206bd14a.png
tags: blogging, aws, devops, 90daysofdevops, trainwithshubham

---

In the previous blog, I automated EC2 instances using launch templates. In this blog let’s learn about Load balancing and Load balancers in AWS.

# **What is Load Balancing?**

Load balancing is a technique that distributes network or application traffic across several servers. This can improve performance, reliability, and availability.

Load balancers work by receiving requests from clients and then routing them to one of the servers in the pool. The load balancer uses a variety of factors to determine which server to send a request to, such as the server’s load, availability, and health.

In Amazon EC2, Elastic Load Balancing (ELB) is the load balancing service provided by AWS.

# **Elastic Load Balancing**

Elastic Load Balancing automatically distributes your incoming traffic across multiple targets, such as EC2 instances, containers, and IP addresses, in one or more Availability Zones.

It monitors the health of its registered targets, and routes traffic only to the healthy targets.

Elastic Load Balancing scales your load balancer capacity automatically in response to changes in incoming traffic.

How does Elastic Load Balancing work?

* Clients make requests to your application.
    
* The listeners in your load balancer receive requests matching the protocol and port that you configure.
    
* The receiving listener evaluates the incoming request against the rules you specify, and if applicable, routes the request to the appropriate target group. You can use an HTTPS listener to offload the work of TLS encryption and decryption to your load balancer.
    
* Healthy targets in one or more target groups receive traffic based on the load-balancing algorithm, and the routing rules you specify in the listener.
    

The benefits of load balancing:

* Improved performance: Load balancing can improve performance by distributing traffic across multiple servers. This can help to reduce latency and improve response times.
    
* Increased reliability: Load balancing can increase reliability by ensuring that no single server is overloaded. If one server goes down, the load balancer can redirect traffic to the remaining servers.
    
* Improved availability: Load balancing can improve availability by ensuring that your applications are always available. If one server goes down, the load balancer can redirect traffic to the remaining servers.
    

ELB can be created, accessed, and managed by using AWS Management Console, AWS Command Line Interface, AWS SDKs, and Query API.

Elastic Load Balancing supports the following types of load balancers:

* Application Load Balancers
    
* Network Load Balancers
    
* Gateway Load Balancers
    
* Classic Load Balancers
    

There is a key difference in how the load balancer types are configured:

* With Application Load Balancers, Network Load Balancers, and Gateway Load Balancers, you register targets in target groups, and route traffic to the target groups.
    
* With Classic Load Balancers, you register instances with the load balancer.
    

Cross-zone load balancing

The nodes for your load balancer distribute requests from clients to registered targets.

When cross-zone load balancing is enabled, each load balancer node distributes traffic across the registered targets in all enabled Availability Zones.

When cross-zone load balancing is disabled, each load balancer node distributes traffic only across the registered targets in its Availability Zone.

* With Application Load Balancers, cross-zone load balancing is always enabled at the load balancer level.
    
* At the target group level, cross-zone load balancing can be disabled.
    
* With Network Load Balancers and Gateway Load Balancers, cross-zone load balancing is disabled by default. After you create the load balancer, you can enable or disable cross-zone load balancing at any time.
    

> *When you create a Classic Load Balancer, the default for cross-zone load balancing depends on how you create the load balancer. With the API or CLI, cross-zone load balancing is disabled by default. With the AWS Management Console, the option to enable cross-zone load balancing is selected by default.*

Now let us understand the different types of ELB provided by AWS:

# **Application Load Balancer**

Here is the official documentation of the [Application Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/introduction.html).

ALB Functions at the application layer, the seventh layer of the Open Systems Interconnection (OSI) model.

It intelligently distributes incoming HTTP and HTTPS traffic to target instances, containers, or IP addresses based on the rules and configurations set by the user.

# **Network Load Balancer**

Here is the official documentation of the [Network Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/introduction.html).

NLB functions at the fourth layer of the Open Systems Interconnection (OSI) model. It can handle millions of requests per second.

NLB operates at the transport layer (Layer 4) of the OSI model and is designed to handle TCP, UDP, and TLS traffic.

It is highly scalable, offers low latency, and is suitable for applications that require high performance and extreme scalability.

# **Gateway Load Balancer**

Here is the official documentation of the [Gateway Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/gateway/introduction.html).

A Gateway Load Balancer operates at the third layer of the Open Systems Interconnection (OSI) model, the network layer.

It listens for all IP packets across all ports and forwards traffic to the target group that’s specified in the listener rule.

It maintains the stickiness of flows to a specific target appliance using a 5-tuple (for TCP/UDP flows) or 3-tuple (for non-TCP/UDP flows).

# **Classic Load Balancer**

Here is the official documentation of the [Classic Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/elb-getting-started.html).

*CLB* operates at both the application layer (Layer 7) and transport layer (Layer 4) of the OSI model and is ideal for applications that require basic load-balancing features.

CLB provides basic load-balancing capabilities for distributing incoming traffic across multiple Amazon EC2 instances.

Here is the link which gives the product differentiation and pricing of the [different ELBs provided by AWS.](https://aws.amazon.com/elasticloadbalancing/features/#Product_comparisons)

# **Tasks**

# **Task 1: Launch 2 EC2 instances with an Ubuntu AMI and use User Data to install the Apache Web Server. Modify the index.html file to include your name so that when your Apache server is hosted, it will display your name also do it for 2nd instance which provides for “ TrainWithShubham Community is Super Awesome :) “.**

Create two EC2 instances with the following details:

> *Name: Apache-Server*
> 
> *Application and OS Images (Amazon Machine Image): Ubuntu AMI*
> 
> *Instance type: t2.micro*
> 
> *Key pair (login): Select the key pair you want.*
> 
> *Network Settings: Check the boxes “Allow HTTPS traffic from the Internet” & “Allow HTTP traffic from the Internet”*
> 
> *Advanced details:*
> 
> *Scroll down to the User data box and type these commands:*

```plaintext
#!/bin/bash
sudo apt-get update -y
sudo apt-get install apache2 -y
sudo systemctl start apache2
sudo systemctl enable apache2
```

> *Number of instances: 2*

Click on Launch Instance. Once the instances are created rename them with numbers so you can easily identify the servers.

![](https://miro.medium.com/v2/resize:fit:875/1*Q2lezpRq8iA8EYRlkXATSw.png align="left")

To modify the index.html file, we need to modify its content in the directory /var/www/html.

Let’s connect to Apache-Server-1.

![](https://miro.medium.com/v2/resize:fit:875/1*NczuNDoa5iUxlk7DmbK_QA.png align="left")

The directory /var/www/html exists. Let’s modify the index.html file.

Give the index.html file root user privilege.

```plaintext
sudo chmod +x index.html
```

These are the contents I have used in the index.html file:

```plaintext
<!DOCTYPE html>
<html>
<head>
<title>My New Page for Apache Web Server</title>
</head>
<body>
<h1>Author - Mudit Mathur</h1>
</body>
</html>
```

Copy the Public IP of the instance and paste it into the browser. You should be able to see the author’s name.

![](https://miro.medium.com/v2/resize:fit:875/1*efIhNIVAaU0HzDiKuJpctA.png align="left")

Let us do the same thing for the other server with some more additions.

```plaintext
<!DOCTYPE html>
<html>
<head>
<title>My New Page for Apache Web Server</title>
</head>
<body>
<h1>Author - Mudit Mathur</h1>
<h2> TrainWithShubham Community is Super Awesome :) <h2>
<h3> I am happy to use the Apache Web Server <h3>
</body>
</html>
>
```

![](https://miro.medium.com/v2/resize:fit:875/1*_jez7FEc9LM1-E8LkmqKuQ.png align="left")

Connect to the Web server using the instance’s Public IP.

![](https://miro.medium.com/v2/resize:fit:875/1*Te5IDga5CccU95j2l3-gCA.png align="left")

And yay! We have successfully installed the Apache Web server and edited the index.html file.

# **Task 2: Create an Application Load Balancer (ALB) in EC2 using the AWS Management Console. Add EC2 instances that you launch in task-1 to the ALB as target groups. Verify that the ALB is working properly by checking the health status of the target instances and testing the load-balancing capabilities.**

On the left side of the EC2 page, if you scroll down you can see Load Balancers, select it.

![](https://miro.medium.com/v2/resize:fit:875/1*LDqaty14ICohMedmyaebmQ.png align="left")

Click on Create Load balancer. The following page opens up.

![](https://miro.medium.com/v2/resize:fit:875/1*tX1uQyLNzfao7rbFM7HYeQ.png align="left")

Select Application Load Balancer and click on Create.

Basic configuration:

> *Load balancer name: PHP-lb*
> 
> *Scheme: Internet Facing (access to public)*
> 
> *Network mapping: Select at least two Availability Zones and one subnet per zone.*
> 
> *Security Group: default will be selected and select the other security groups you require.*

Before going ahead, let’s create Target Groups. Select Target Groups which is below the Load balancer on your left-hand side.

![](https://miro.medium.com/v2/resize:fit:274/0*AjeRi4YzmdI-odbg align="left")

Click on Create Target groups.

Step 1: Specify group details

> *Basic configuration: Instances*
> 
> *Target group name: ALB-apache*

![](https://miro.medium.com/v2/resize:fit:521/0*-6I01wed_9qRu81F align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*cSXR78VtWN89LE8eA-OAhQ.png align="left")

> *And click on Next*

Step 2: Register targets

> *Available Instances: Select the instances which you need*

![](https://miro.medium.com/v2/resize:fit:875/1*MKWxNTP-nwQnrwOHe8CKaw.png align="left")

*Click on Create Target groups.*

![](https://miro.medium.com/v2/resize:fit:875/1*Y381VStG4dU4FahdulH1MQ.png align="left")

Now go back to the ALB page.

![](https://miro.medium.com/v2/resize:fit:875/1*EKtiAT0WZGmJQQc-QAJ9oA.png align="left")

Select the target group you just created.

And click on Create Load Balancer.

Once the ALB is in an active state, copy the DNS of the load balancer and access it from your website.

![](https://miro.medium.com/v2/resize:fit:875/0*RETDh6ESk1mLmSjK align="left")

As per the load, we can observe that sometimes Server 1 comes up and other times Server 2 comes up.

![](https://miro.medium.com/v2/resize:fit:875/1*Vv_RGG_xxcSKp1yrOX3IRA.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*pWSHvf6QpWr19l7un2NIXw.png align="left")

And we have created an ALB, and created the load!

In this blog, I have discussed how to create an AWS Application Load Balancer and use it to balance the load between two web servers. If you have any questions or would like to share your experiences, please leave a comment below. Don’t forget to read my blogs and connect with me on LinkedIn and let’s have a conversation.

To help me improve my blog and correct my mistakes, I am available on LinkedIn as [Mudit Mathur.](https://www.linkedin.com/in/mudit--mathur/) Do reach me and I am open to suggestions and corrections.

#Day41 #90daysofdevops