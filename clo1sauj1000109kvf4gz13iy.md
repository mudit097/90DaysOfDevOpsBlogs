---
title: "Terraform Resources"
datePublished: Sun Oct 22 2023 18:10:23 GMT+0000 (Coordinated Universal Time)
cuid: clo1sauj1000109kvf4gz13iy
slug: terraform-resources
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697998136200/ad9c6370-04ca-4c90-a79c-a9fa91b76d70.png
tags: aws, devops, terraform, 90daysofdevops, trainwithshubham

---

In the realm of Terraform, the process of orchestrating cloud resources begins with understanding Terraform resources.

In this journey, we embark on three fundamental tasks:

**Task 1** involves creating a security group, **Task 2** is about crafting an EC2 instance, and Task 3 guides us in accessing our website for a personal blog.

Let’s explore these tasks and delve into the power of Terraform’s infrastructure as code.

# **Understanding Terraform Resources**

A resource in Terraform represents a component of your infrastructure, such as a physical server, a virtual machine, a DNS record, or an S3 bucket. Resources have attributes that define their properties and behaviors, such as the size and location of a virtual machine or the domain name of a DNS record.

When you define a resource in Terraform, you specify the type of resource, a unique name for the resource, and the attributes that define the resource. Terraform uses the resource block to define resources in your Terraform configuration.

A resource block typically includes the following elements:

* Resource Type: Specifies the type of resource being defined, such as “aws\_instance” for an Amazon EC2 instance.
    
* Resource name: Provides a unique name for the resource within your configuration.
    
* Resource configuration: Specifies the desired settings and attributes for the resource, such as the instance type, disk size, or access control rules.
    

# **Task 1: Create a security group**

* To allow traffic to the EC2 instance, you need to create a security group.
    
* In your [`main.tf`](http://main.tf) file configures the AWS Provider.
    

```plaintext
  terraform {
    required_providers {
      aws = {
        source  = "hashicorp/aws"
        version = "~> 4.0"
      }
    }
  }

  provider "aws" {
    region = "us-east-1"
  }
```

* Now add the following code in your [`main.tf`](http://main.tf) file to create a security group:
    

```plaintext
  resource "aws_security_group" "web_server" {
    name_prefix = "web-server-sg"
    ingress { 
       from_port   = 22 
       to_port     = 22 
       protocol    = "tcp" 
       cidr_blocks = ["0.0.0.0/0"] 
     } 

    ingress {
      from_port   = 80
      to_port     = 80
      protocol    = "tcp"
      cidr_blocks = ["0.0.0.0/0"]
    }

    ingress { 
       from_port   = 443 
       to_port     = 443 
       protocol    = "tcp" 
       cidr_blocks = ["0.0.0.0/0"] 
     } 

    egress { 
       from_port   = 0 
       to_port     = 0 
       protocol    = "-1" 
       cidr_blocks = ["0.0.0.0/0"] 
     }
  }
```

![](https://miro.medium.com/v2/resize:fit:875/0*X72op3HZBVRTvGHO align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*TwbJ7tIiqAUcJb18 align="left")

* Run the `terraform init` to initialize the Terraform project and.
    

![](https://miro.medium.com/v2/resize:fit:875/0*7uu9pJgwF2yPle9U align="left")

* Run the `terraform apply` to create the security group.
    

![](https://miro.medium.com/v2/resize:fit:875/0*4aJVxxQ6trfWIjVr align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*rxtJwHT_hBMur-tS align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*OyEB2tKPjhdIlSEY align="left")

* Check whether the security group is created or not.
    

![](https://miro.medium.com/v2/resize:fit:875/0*HRoQAw0W47TMsMlf align="left")

# **Task 2: Create an EC2 instance**

* Now you can create an EC2 instance with Terraform.
    
* Follow these steps:
    
* In your [main.tf](http://main.tf) file, add the following code to create an EC2 instance:
    

```plaintext
  resource "aws_instance" "web_server" {
    ami           = "ami-053b0d53c279acc90"
    instance_type = "t2.micro"
    key_name      = "Terraform-Key"
    tags = {
        Name = "TerraformTestServer1"
    }
    security_groups = [
      aws_security_group.web_server.name
    ]

   user_data = <<-EOF
    #!/bin/bash
    sudo apt-get update -y
    sudo apt-get install apache2 -y
    sudo systemctl start apache2
    sudo systemctl enable apache2
    sudo systemctl restart apache2
    sudo chmod 766 /var/www/html/index.html
    sudo echo "<html><body><h1>Welcome to my website!</h1></body></html>" >/var/www/html/index.html    
   EOF
  }
```

* Note: Replace the ami and key\_name values with your own. You can find a list of available AMIs in the AWS documentation.
    
* Run terraform apply to create the EC2 instance.
    

![](https://miro.medium.com/v2/resize:fit:875/0*Rm1yaxPoyawyWsRa align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*khFG_fl4QXFxjzHx align="left")

# **Task 3: Access your website**

* Now that your EC2 instance is up and running, you can access the website you just hosted on it. Follow these steps:
    

![](https://miro.medium.com/v2/resize:fit:875/0*Vb39wg9_anxinLdu align="left")

* Copy the public IPv4 address of the instance that is created using Terraform. Browse `http://<Public_IPv4_Addr>` of your instance. You can see the webpage.
    

![](https://miro.medium.com/v2/resize:fit:875/1*H48OiMjWnJ-B4oOe4_QU4Q.jpeg align="left")

In conclusion, we’ve embarked on an exciting journey into the world of Terraform resources, and I hope you’ve gained valuable insights throughout this blog. We’ve covered everything from creating security groups, launching EC2 instances, and finally, accessing your website.

With Terraform, the possibilities are endless, and your infrastructure as code adventure has only just begun. As you continue to explore this powerful tool, you’ll discover its flexibility and scalability for managing your cloud resources efficiently.

Now, as you move forward, remember to apply these principles to your own projects, customize them to suit your specific needs, and stay updated with the latest developments in the Terraform ecosystem. If you have any questions or need further assistance, don’t hesitate to reach out to the Terraform community or explore the official documentation.

If you’d like to connect with me and explore these topics further, please find me on ([https://www.linkedin.com/in/mudit--mathur/](https://www.linkedin.com/in/mudit--mathur/)). Your feedback and contributions are invaluable as we all strive to enhance our DevOps and infrastructure skills.

Thank you for joining us on this journey of Understanding Terraform Resources. We look forward to seeing you in future blogs and helping you on your path to infrastructure automation excellence. Happy Terraforming! Day 65.