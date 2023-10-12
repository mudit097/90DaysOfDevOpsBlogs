---
title: "Day 55: Configuration Management with Ansible"
datePublished: Thu Oct 12 2023 14:57:49 GMT+0000 (Coordinated Universal Time)
cuid: clnnb0okj000g09l80dae4xpb
slug: day-55-configuration-management-with-ansible
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697122568231/9a6e6f7a-c44a-41fc-a386-76c81a967859.png
tags: blogging, aws, ansible, devops, iac

---

Welcome to our comprehensive guide on Configuration Management and Ansible! In this blog, we will delve into the world of Configuration Management and explore when to use it instead of Infrastructure as Code (IaC). We will also introduce you to common tools used in Configuration Management, with a special focus on Ansible. By the end of this journey, you’ll not only understand what Configuration Management is but also have the practical knowledge to perform key tasks like installing Ansible on an AWS EC2 instance (Master Node), setting up Ansible Host files, and configuring Ansible Child Nodes. So, let’s get started with the Table of Contents to help you navigate through this enlightening exploration.

# **What is Configuration Management?**

* Configuration management is a discipline that focuses on managing and controlling changes to a system’s configuration. It involves identifying and documenting the system’s components, their relationships, and their attributes.
    
* It ensures that changes to the system are properly planned, evaluated, approved, and implemented. Configuration management aims to maintain consistency, integrity, and traceability of the system’s configuration throughout its lifecycle.
    
* It facilitates efficient troubleshooting, maintenance, and version control of software, hardware, or any other complex system. Configuration management helps prevent unauthorized changes and ensures compliance with standards and regulations.
    

# **When do we use Configuration Management instead of IaC?**

* Configuration Management is typically used when dealing with established systems or environments that have already been set up manually or with traditional infrastructure management approaches.
    
* It is useful in scenarios where the primary goal is to manage and track changes to the configuration of these existing systems. In contrast, Infrastructure as Code (IaC) is employed when creating new infrastructure or when adopting a more agile and automated approach to provisioning and managing infrastructure resources.
    

# **Common Tools Used in Configuration Management**

1. **Ansible:** An automation tool that enables configuration management, application deployment, and orchestration.
    
2. **Puppet:** An open-source configuration management tool that helps automate the provisioning, configuration, and management of systems.
    
3. **Chef:** A configuration management tool used for infrastructure automation and management.
    
4. **Kubernetes:** An open-source container orchestration platform that helps manage and automate the deployment, scaling, and operation of containerized applications.
    
5. **SaltStack:** A configuration management and remote execution tool that aids in managing and controlling infrastructure.
    

# **Define Ansible**

* Ansible is an open-source automation tool that allows users to define and manage infrastructure as code. It follows a declarative language approach, making it easy to automate repetitive tasks, configuration management, and application deployment.
    
* Use cases for Ansible include provisioning and managing servers, deploying applications, configuring network devices, automating cloud infrastructure, and orchestrating complex workflows.
    
* It provides a simple and agentless architecture, making it highly scalable and efficient for managing large-scale environments. Ansible’s versatility and simplicity make it popular among DevOps teams for streamlining and automating various IT operations.
    

# **Task-1: Installation of Ansible on AWS EC2 (Master Node)**

* Create a new EC2 instance in AWS Console.
    

![](https://miro.medium.com/v2/resize:fit:875/1*-h9hnSlCaRQSj713M0TUvg.png align="left")

* Now connect the EC2 instance using SSH.
    

![](https://miro.medium.com/v2/resize:fit:875/1*0J77xhE01gXd4ILl60NGLw.png align="left")

* Once you SSH the instance, install Ansible.
    

```plaintext
  # Add ansible repository to your instance
  sudo apt-add-repository ppa:ansible/ansible

  # Update the package
  sudo apt update

  # Install the Ansible
  sudo apt install ansible
```

![](https://miro.medium.com/v2/resize:fit:875/1*TEdL1WlL2ZIblzZuslP4Iw.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*QEZKEjqrWoiddQ1ifq8LSA.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*YejekWDMTyVdnecGvtsIdg.png align="left")

* As installation completes, to verify Ansible is installed successfully, we can check the Ansible by using the following command.
    

```plaintext
  ansible --version
```

![](https://miro.medium.com/v2/resize:fit:875/1*myLFxSNSQOtb5zbO4v4WUA.png align="left")

# **Task-2: Ansible Host File**

* The Ansible host file is a text file that contains a list of hosts or servers that Ansible can connect to and manage. The host’s file is located at /etc/ansible/hosts on the Ansible control node, It defines the inventory of systems on which Ansible can perform automation tasks.
    
* To edit the hosts file, you can use any text editor of your choice.
    

```plaintext
  sudo vim /etc/ansible/hosts
```

![](https://miro.medium.com/v2/resize:fit:875/1*B9WYcLvc6wTuVy5bbY7USw.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*EN9HSEAh8zukMOPWrdXR-Q.png align="left")

* After you have added the hosts to the file, you can verify the inventory of hosts that Ansible can manage using the `ansible-inventory --list` command.
    

```plaintext
  ansible-inventory --list
```

![](https://miro.medium.com/v2/resize:fit:875/1*zEdbalqVFRblGw9Vh5etnQ.png align="left")

# **Task-3: Configuring Ansible Child Node**

* We need to create 1 master node and 3 server nodes
    

![](https://miro.medium.com/v2/resize:fit:875/0*CTNn-5uB_v236gvV.png align="left")

we have launched 1 master node , we need 3 server nodes

select the instance &gt; actions &gt; image and templates &gt; launch more like these

![](https://miro.medium.com/v2/resize:fit:875/1*m84Is73jg9vkVUkOWv9Fiw.png align="left")

Launch 3 instances with the same configurations ,

And launch instance

![](https://miro.medium.com/v2/resize:fit:875/1*2-5zFs49a9svPtGZQU679A.png align="left")

Change the name of the 3 — instances ,

![](https://miro.medium.com/v2/resize:fit:875/1*KvNeTpfN6QGeBpgWyo7Y4w.png align="left")

Now, Setup 3 more EC2 instances having the same Private keys as the Ansible Master Node.

Add the newly created public IPv4 host address in the ansible master /etc/ansible/hosts file.

```plaintext
  sudo vim /etc/ansible/hosts
```

```plaintext
  [my-servers]
  server1 ansible_host=<Server1_IPv4_Addr>
  server2 ansible_host=<Server2_IPv4_Addr>
  server3 ansible_host=<Server3_IPv4_Addr>
```

![](https://miro.medium.com/v2/resize:fit:875/1*BmQtLz37mJxDPQi7LDzg4Q.png align="left")

Go to the master server ,

use command

**ssh-keygen** to generate id\_rsa.pub

![](https://miro.medium.com/v2/resize:fit:875/1*_DJYQ_aCoKWVNIw1-1G-Lw.png align="left")

Copy the key from id\_rsa.pub

![](https://miro.medium.com/v2/resize:fit:875/1*ROTtNiKaOk7YWADypCttWg.png align="left")

Now go to the ansible *server*2 instance ,

Go to .ssh &gt; authorized\_keys

```plaintext
ubuntu@ip-172-31-41-31:~ $ cd .ssh
ubuntu@ip-172-31-41-31:~/.ssh$ ls
authorized_keys
ubuntu@ip-172-31-41-31:~/.ssh vim authorized_keys
```

And paste the public key here ,

![](https://miro.medium.com/v2/resize:fit:875/1*XpFJbtQGak1T_3naxL0PuQ.png align="left")

Save and exit.

Do the same for ansible\_server\_2 ,ansible\_server\_3

![](https://miro.medium.com/v2/resize:fit:875/1*TPPw0KHOX86DDZxTNljq0g.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*k0en_Y__Hxoq5zx3cN-1Zw.png align="left")

Upload keygen from local to Ec2 instance

```plaintext
  sudo scp -i "<pem_key>" <pem_key> ubuntu@ec2-<ipaddr>.compute-1.amazonaws.com:/home/ubuntu/.ssh/
```

![](https://miro.medium.com/v2/resize:fit:875/1*W5dy9nGKGc2i5cuTjxTQuQ.png align="left")

As the file is uploaded into the .ssh folder, change the file permission rwx to the user only.

```plaintext
  chmod 700 flask-server.pem
```

![](https://miro.medium.com/v2/resize:fit:875/1*xKAnYTYsAFk9XMxhBhSnug.png align="left")

As file permission is modified, add the private key and Python file to the host file

```plaintext
  [all:vars]
  ansible_ssh_private_key_file=/home/ubuntu/.ssh/flask-server.pem
  ansible_python_interpreter=/usr/bin/python3
  ansible_user=ubuntu
```

![](https://miro.medium.com/v2/resize:fit:875/1*hTR5TGMvP0gdadUMcZ_IJw.png align="left")

We can see all the server’s details in the inventory list where we are providing the host address, python directory and private key to be used.

```plaintext
  ansible-inventory --list
```

![](https://miro.medium.com/v2/resize:fit:875/1*v4sYF2vf8pTbxco_6_psjA.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*tD_Z5G6Bc2m6SJxjpEtgCQ.png align="left")

Provide an ad-hoc command to check free RAM for all the servers.

```plaintext
  ansible all -a "free -h" -u ubuntu
```

![](https://miro.medium.com/v2/resize:fit:875/1*FOwN5FZ-NXabVN7hLbXDFg.png align="left")

Try a ping module command using ansible to all the child nodes.

```plaintext
  ansible all -m ping -u ubuntu
```

![](https://miro.medium.com/v2/resize:fit:875/1*Ar4vTEIt-DH0fNsrwkIU1w.png align="left")

If you are getting an error related to authentication as you’re using a custom SSH key to connect to the remote servers, you can provide it at execution time with the `--private-key` option

To know more about Ansible please refer to the video [Ansible Video](https://youtu.be/SGB7EdiP39E?t=1020)

```plaintext
  ansible all -m ping -i /etc/ansible/hosts --private-key=~/.ssh/flask-server.pem
```

![](https://miro.medium.com/v2/resize:fit:875/1*VKnjBbLdSSNEIg0KMD4PQQ.png align="left")

Note: Still If you are getting any error related to the key, then copy the id\_[rsa.pub](http://rsa.pub/) key of the Ansible master and paste it to each server.

![](https://miro.medium.com/v2/resize:fit:875/1*ROTtNiKaOk7YWADypCttWg.png align="left")

Child Servers

![](https://miro.medium.com/v2/resize:fit:875/1*XpFJbtQGak1T_3naxL0PuQ.png align="left")

In this blog, we dove into Configuration Management, a crucial aspect of DevOps. We discussed the core concept and when to opt for Configuration Management over Infrastructure as Code (IaC).

We introduced Ansible, a versatile tool in this space, and walked through practical tasks to set it up on AWS.

Your feedback is highly valued on my [LinkedIn Mudit Mathur](https://www.linkedin.com/in/mudit--mathur/), as it helps me continually improve. Stay tuned for more DevOps insights, and let’s keep the conversation going. #Day55 #90daysofdevops