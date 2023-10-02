---
title: "AWS EC2 Automation"
datePublished: Mon Oct 02 2023 06:09:51 GMT+0000 (Coordinated Universal Time)
cuid: cln8hr6sg000d0amlcaa7htiy
slug: aws-ec2-automation
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696226863210/c3c4e5de-101b-4125-93b4-4c2d0b42815e.png
tags: blogging, aws, devops, 90daysofdevops, trainwithshubham

---

In the previous blog, we learned about User Data and IAM. Let’s learn how to automate EC2 using Launch Templates and Auto Scaling Groups.

# **EC2**

EC2 stands for Elastic Compute Cloud. It is a web service provided by Amazon Web Services (AWS).

EC2 provides scalable computing capacity, allowing users to quickly provision and configure virtual machines called instances.

With EC2, users can choose the type of instance they need, such as the amount of CPU, memory, storage, and networking capacity. Instances can be launched from pre-configured Amazon Machine Images (AMIs) that contain various operating systems and software configurations, or users can create their own custom AMIs.

EC2 provides a flexible and scalable infrastructure for running applications in the cloud, allowing users to pay only for the resources they consume and easily scale their computing capacity up or down as needed.

The below image depicts the lifecycle of an Instance:

![](https://miro.medium.com/v2/resize:fit:623/0*aRa5NXSkVkW8Xltj.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*oL_r54qMdt2BVnj3axnmEQ.png align="left")

Instances can be launched using the launch instance wizard or using a launch template.

# **Launch Templates in EC2**

A launch template is a feature provided by Amazon EC2 that allows you to create reusable configurations for launching instances.

You can create a *launch template* that contains the configuration information to launch an instance. You can use launch templates to store launch parameters so that you do not have to specify them every time you launch an instance.

Launch templates support versioning, which means you can create multiple versions of a template to track changes over time. If you do not specify a version, the default version is used. You can set any version of the launch template as the default version — by default, it’s the first version of the launch template.

# **Instance Types**

When you launch an instance, the *instance type* that you specify determines the hardware of the host computer used for your instance.

Instance types are named based on their family, generation, additional capabilities, and size.

* The first position of the instance type name indicates the instance family, for example `c`.
    
* The second position indicates the instance generation, for example `5`.
    
* The remaining letters before the period indicate additional capabilities, such as instance store volumes.
    
* After the period (`.`) is the instance size, which is either a number followed by size, such as `9xlarge`, or `metal` for bare metal instances.
    

The different types of Instances provided by AWS are:

# **General Purpose**

These instances provide a balance of CPU, memory, and network resources. They are suitable for a wide range of workloads, including web servers, small databases, development environments, and other applications that require a balance of compute power and memory.

Examples: t3, m5

# **Compute Optimised**

These instances are designed for compute-intensive workloads that require high CPU performance. They offer a high ratio of vCPUs to memory and are ideal for applications like scientific modeling, batch processing, gaming servers, and highly scalable front-end fleets.

Examples: c5

# **Memory Optimised**

Memory-optimized instances are designed for memory-intensive workloads such as in-memory databases, real-time analytics, and high-performance computing. They offer a large amount of RAM relative to CPU resources, allowing efficient processing of data-intensive applications.

Examples: r5

# **Storage Optimised**

Storage-optimized instances are designed for workloads that require high storage capacity and high sequential read/write performance. They are suitable for big data processing, data warehousing, and other applications that require fast and large-scale data access.

Examples: i3, d2.

# **GPU Instances**

GPU instances are equipped with powerful graphics processing units (GPUs) that accelerate applications requiring parallel processing and high-performance computing. They are used for machine learning, deep learning, video rendering, and other GPU-intensive workloads.

Examples: p3, g4.

# **FPGA Instances**

FPGA (Field Programmable Gate Array) instances are specialized instances that provide programmable hardware acceleration. They are suitable for applications that require custom hardware acceleration and can be programmed to perform specific tasks efficiently.

Examples: f1

# **Instance Sizes**

![](https://miro.medium.com/v2/resize:fit:875/1*1PJAuuOLy86H5iAbM3Bm3g.png align="left")

# **AMI**

AMI stands for Amazon Machine Image. It is a pre-configured template that contains the necessary information to launch an instance in Amazon EC2. An AMI serves as the building block for creating virtual servers in the cloud.

AMIs are available as Amazon-provided AMIs, AWS Marketplace AMIs, and Custom AMIs.

An AMI includes Root Volume, Instance Configuration, Permissions, Block Device Mappings, and Launch Permissions.

# **Tasks: Create a launch template with Ubuntu AMI and t2.micro instance type with Jenkins and Docker setup (You can use the Day 39 User data script for installing the required tools).**

Select Launch Templates on the left side of your screen under Instances.

![](https://miro.medium.com/v2/resize:fit:875/1*PkwKZ_SmuVeZjn0rakI8FA.png align="left")

Click on Create Launch Template.

![](https://miro.medium.com/v2/resize:fit:875/1*s1QEWz1_mv5kwpg4qP-Z0Q.png align="left")

*Application and OS Images (Amazon Machine Image): Ubuntu*

*Instance Type: t2.micro*

*Advanced Details: Use the following script-*

```plaintext
#!/bin/bash
sudo apt-get update -y
sudo apt install openjdk-11-jre -y
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins -y
sudo systemctl enable jenkins
sudo systemctl start jenkins
sudo apt-get update
sudo apt-get install docker.io -y
sudo systemctl start docker
```

Click on Create Launch Template.

In the Launch Templates Dashboard, select the template you created and click on Actions. Select Launch Instance from the template.

![](https://miro.medium.com/v2/resize:fit:875/1*SczQoi6iiWU6roAdmFX3ZA.png align="left")

Since we need 3 instances from the template we created, In Summary &gt; Number of Instances &gt; Type 3.

![](https://miro.medium.com/v2/resize:fit:875/1*2OIeChsnj5MXDrE1u0-7XQ.png align="left")

Select the KeyPair and click on Launch Instances.

We can see that 3 instances are running.

![](https://miro.medium.com/v2/resize:fit:875/1*nBwb2j2x-3d7bTSMH5Ignw.png align="left")

Let’s create ASG(Auto Scaling Group) and make the process more automated depending on the usage.

On the left side of your screen, you can find Auto Scaling Groups.

![](https://miro.medium.com/v2/resize:fit:875/1*Wr7Fj8GJ_GFnFh_Eiz0rCg.png align="left")

Click on Create Auto Scaling Group.

Step 1: Choose the launch template or configuration

> *Auto Scaling group name: JenDockScaling*
> 
> *Launch template: DockerJenkinsTemplate*
> 
> *Version: 2*

![](https://miro.medium.com/v2/resize:fit:875/1*zTZWdWNaiasJ4_h18c4jeg.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*fcXZGz26-L9eoSQJtI7qLw.png align="left")

Click Next.

Step 2: Choose instance launch options

![](https://miro.medium.com/v2/resize:fit:875/1*7ZOYrZcdJHJcWvtLaT5l0w.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*teTry2UDz_8OdM9gfavdlw.png align="left")

Select the availability zones and click on Next.

Step 3: Configure advanced options

*Load balancing: Attach to a new load balancer*

![](https://miro.medium.com/v2/resize:fit:875/1*k302tQpVzTEbUDhu23hgYw.png align="left")

*Attach to a new load balancer:*

![](https://miro.medium.com/v2/resize:fit:875/1*ez8tjFaqTQkq6koULXfVJA.png align="left")

*Load balancer type: Application Load Balancer*

![](https://miro.medium.com/v2/resize:fit:875/1*R1PLe42X2u-BvV0prGRQRQ.png align="left")

*Load balancer name: JenDockScaling-1*

![](https://miro.medium.com/v2/resize:fit:875/1*3qGekfgTPScRQcP4qEoLgA.png align="left")

*Load balancer scheme: Internal*

![](https://miro.medium.com/v2/resize:fit:875/1*SoBJSkfx1gF7L8uWPIUoqw.png align="left")

Let the other options be the default, and click on Next.

Step 4*:* Configure group size and scaling policies

![](https://miro.medium.com/v2/resize:fit:875/1*DLVnHMA_nAYxInwK-voxJg.png align="left")

*Desired capacity: 3*

*Minimum capacity: 1*

*Maximum capacity: 5*

Click on Next.

Step 5: Add notifications

![](https://miro.medium.com/v2/resize:fit:875/1*aKE1IKO6JI5uBu6O7AjycA.png align="left")

Step 6: Add Tags

![](https://miro.medium.com/v2/resize:fit:875/1*VxkXGnj9uQFZ6-papxUSqA.png align="left")

Click on Next.

Once you reach the Review section, click on Create AutoScaling Groups.

![](https://miro.medium.com/v2/resize:fit:875/1*rabrfyC2FkC9_eH8i38MJA.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*zKRp_5xwIIyhOeiTwpl--A.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*wonwhgemt5VFUR_RicdQHQ.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*v2HnKfmbDaAZX7VVv2p5VA.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*aWXMgmwOThUjhgPu_K_12Q.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*d7_zfJzOfEH1W_Gonpt8pg.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*IKIvkedoWLViMexT46NAFQ.png align="left")

click on Create AutoScaling Group.

![](https://miro.medium.com/v2/resize:fit:875/1*18Nfgai5pVMCbRX1AGAhaw.png align="left")

When the utilization increases or decreases, the instances are scaled up or down automatically, based on the criteria you have given.

In this blog, I have discussed how to automate EC2 instance creation using Launch Templates and Auto Scaling Groups. If you have any questions or would like to share your experiences, please leave a comment below. Don’t forget to read my blogs and connect with me on LinkedIn and let’s have a conversation.

To help me improve my blog and correct my mistakes, I am available on LinkedIn as [Mudit Mathur.](https://www.linkedin.com/in/mudit--mathur/) Do reach me and I am open to suggestions and corrections.

#Day40 #90daysofdevops