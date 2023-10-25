---
title: "Meta-Arguments in Terraform"
datePublished: Wed Oct 25 2023 05:24:20 GMT+0000 (Coordinated Universal Time)
cuid: clo5b996b000z09mcbakt344p
slug: meta-arguments-in-terraform
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1698211402657/68a0c7da-2d41-463b-b630-96ef55263d8d.png
tags: aws, devops, terraform, 90daysofdevops, trainwithshubham

---

In the fascinating world of Infrastructure as Code (IaC) with Terraform, it’s crucial to understand the concept of Meta-Arguments. These Meta-Arguments, including “count” and “for\_each,” play a pivotal role in shaping the way you define and manage your infrastructure. In this blog, we’ll delve into the core of Meta-Arguments, exploring their applications and practical use cases.

We’ll not only discuss the essentials but also provide a hands-on demonstration in Task 1, where we create IaC using “count” and “for\_each.” So, join us on this journey as we unravel the power and versatility of Meta-Arguments in Terraform, enabling you to optimize your infrastructure provisioning like never before. Let’s dive in!

# **What are Meta-Arguments in Terraform**

* meta-arguments are special arguments used to modify the behavior of resources or blocks. They provide additional functionality beyond the standard resource configuration.
    
* Meta-arguments allow you to customize resource behavior, define dependencies between resources, control resource lifecycle, and associate providers with resources or blocks.
    
* When you define a resource block in Terraform, by default, this specifies one resource that will be created. To manage several of the same resources, you can use either count or for\_each, which removes the need to write a separate block of code for each one.
    
* Using these options reduces overhead and makes your code neater. count is what is known as a ‘meta-argument’ defined by the Terraform language. Meta-arguments help achieve certain requirements within the resource block.
    

# **count**

The count meta-argument accepts a whole number and creates the number of instances of the resource specified.

When each instance is created, it has its own distinct infrastructure object associated with it, so each can be managed separately. When the configuration is applied, each object can be created, destroyed, or updated as appropriate.

# **for\_each**

Like the count argument, the for\_each meta-argument creates multiple instances of a module or resource block. However, instead of specifying the number of resources, the for\_each meta-argument accepts a map or a set of strings.

This is useful when multiple resources are required that have different values. Consider our active directory groups example, with each group requiring a different owner.

# **Use cases of meta arguments**

1. Dynamic resource creation: Use “count” to create a variable number of instances based on conditions.
    
2. Managing dependencies: “depends\_on” ensures resources are created or modified in the correct order.
    
3. Fine-grained lifecycle management: “lifecycle” controls resource behavior during updates or replacements.
    
4. Multi-cloud provider support: “provider” associates different providers with specific resources, enabling multi-cloud management.
    
5. Custom provisioning and configuration: “provisioner” executes scripts or commands during resource creation or destruction, allowing custom actions.
    

# **Task- 1: Create the above IaC and use “count” and “for\_each”.**

# **Meta Argument: count**

* Create a [`main.tf`](http://main.tf) and pass the details of AWS providers and aws instance details. Using the count meta argument you can name the instances as per the number of counts you have passed on.
    

```plaintext
  terraform {
    required_providers {
       aws = {
          source = "hashicorp/aws"
          version = "~> 4.16"
      }
   }
   required_version = ">= 1.2.0"
  } 

  provider "aws" {
     region = "us-east-1"
  }

  resource "aws_instance" "server" {
       count = 2
       ami = "ami-053b0d53c279acc90"
       instance_type = "t2.micro"
       tags = {
          Name = "Server ${count.index}"
      }
  }
```

* Run `terraform init` to initialize the Terraform project.
    

![](https://miro.medium.com/v2/resize:fit:875/0*R8sShHt74QHBxH-N align="left")

* Execute the `terraform plan` command.
    

![](https://miro.medium.com/v2/resize:fit:875/0*27LTHU1qFTntlsnI align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*gOlufmr9kHhVUl6d align="left")

* Execute the `terraform apply` to create 2 new EC2 instances.
    

![](https://miro.medium.com/v2/resize:fit:875/0*I2fCVj68wqxiGRxc align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*esmDqSD7GKbLMQX- align="left")

* You can verify, 2 new EC2 instances were successfully created and named as per the count argument.
    

![](https://miro.medium.com/v2/resize:fit:875/0*gZc5YYFL6ZT6Q9zR align="left")

# **Meta argument: for\_each**

* Create a [`main.tf`](http://main.tf) and pass the details of AWS providers and aws instance details. Using the for\_each meta argument you can name the instances as per iteration of the locals ami ids.
    

```plaintext
  terraform {
    required_providers {
       aws = {
          source = "hashicorp/aws"
          version = "~> 4.16"
      }
   }
   required_version = ">= 1.2.0"
  } 

  provider "aws" {
     region = "us-east-1"
  }

  locals {
      ami_ids = toset([
          "ami-022e1a32d3f742bd8",
          "ami-053b0d53c279acc90",
       ])
  }

  resource "aws_instance" "server" {
     for_each = local.ami_ids
        ami = each.value
        instance_type = "t2.micro"  
     tags = {
        Name = "Server ${each.key}"
     }
  }
```

* Execute the `terraform apply` to create 2 new EC2 instances.
    

![](https://miro.medium.com/v2/resize:fit:875/0*v6PBCfs8J1J_k3cd align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*nyFTq3vSCtUmifk_ align="left")

* 2 new instances were successfully created and named after ami id as we are using for\_each.
    

![](https://miro.medium.com/v2/resize:fit:875/0*jwmEWlrJRrHBMpCj align="left")

# **Meta argument: multiple key-value iterations.**

* Create a [`main.tf`](http://main.tf) and pass the details of AWS providers and aws instance details. Using the for\_each meta argument you can name the instances as per iteration of the locals ami ids but here we are passing both key: value pairs.
    

```plaintext

  terraform {
    required_providers {
       aws = {
          source = "hashicorp/aws"
          version = "~> 4.16"
      }
   }
   required_version = ">= 1.2.0"
  } 

  provider "aws" {
     region = "us-east-1"
  }

  # Multiple key value iteration
  locals {
    ami_ids = {
      "amazonlinux" :"ami-022e1a32d3f742bd8",
      "ubuntu": "ami-053b0d53c279acc90",
     }
  }

  resource "aws_instance" "server" {
     for_each = local.ami_ids
        ami = each.value
        instance_type = "t2.micro"  
     tags = {
        Name = "Server ${each.key}"
     }
  }
```

* Execute the `terraform apply` to create 2 new instances.
    

![](https://miro.medium.com/v2/resize:fit:875/0*EZAyPZAmmRQwfPrL align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*5I6R-hbJsAp46yzi align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*wJs6FzF7LSN-KzsX align="left")

* Two new instances were successfully created by taking the name using key values of ami ids.
    

![](https://miro.medium.com/v2/resize:fit:875/0*B_WvBIWfvr-0yzUm align="left")

As we reach the conclusion of this exploration into Meta-Arguments in Terraform, we hope you’ve gained valuable insights into how these powerful tools can transform your Infrastructure as Code projects. The understanding of “count” and “for\_each” and their real-world applications opens up a world of possibilities for managing your infrastructure efficiently.

Your feedback is incredibly important to us, and we’re always eager to hear your thoughts and experiences. Please connect with me on LinkedIn ([https://www.linkedin.com/in/mudit--mathur/](https://www.linkedin.com/in/mudit--mathur/)) to share your insights, suggestions, or to stay updated on future discussions in the world of Terraform and IaC.

Thank you for joining us on this journey, and we look forward to sharing more valuable knowledge with you in the future. Keep exploring, keep learning, and keep optimizing your infrastructure. Until next time!