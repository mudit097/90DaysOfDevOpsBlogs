---
title: "Terraform Modules"
datePublished: Wed Oct 25 2023 05:25:45 GMT+0000 (Coordinated Universal Time)
cuid: clo5bb31t000c09l85oqs23pq
slug: terraform-modules
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1698211489437/f5a4366f-27f3-412d-9b02-761a457d932f.png
tags: aws, devops, terraform, 90daysofdevops, trainwithshubham

---

In the dynamic world of infrastructure automation, Terraform has emerged as a game-changer. Central to harnessing its power are Terraform modules. In this blog series, we’ll dive deep into the fascinating realm of Terraform Modules.

We’ll begin by unraveling the core concepts, exploring different module types, and understanding the distinction between Root Modules and Child Modules. Plus, we’ll address a common query: Are Modules and Namespaces the same, or are they different? We’ll provide insights to justify both sides of the argument.

Additionally, we’ll walk you through the file structure for modules and demonstrate how to create a robust AWS infrastructure using Terraform Modules. Join us on this journey to discover how Terraform Modules can elevate your infrastructure provisioning to new heights.

# **What are Terraform Modules**

* Terraform modules are reusable and self-contained collections of Terraform configurations that encapsulate a set of resources and their configurations. A module consists of a collection of .tf and/or .tf.json files kept together in a directory
    
* Modules can be created for specific infrastructure patterns, application components, or entire stacks. They promote code reuse, consistency, and maintainability by encapsulating common infrastructure patterns and configurations.
    
* Modules can also be called multiple times, either within the same configuration or in separate configurations, allowing resource configurations to be packaged and accelerating development by reducing duplication and promoting reusability.
    

# **Different modules of Terraform**

Terraform offers different types of modules to enhance infrastructure management:

1. Provider Modules: Encapsulate cloud provider configurations (e.g., AWS, Azure).
    
2. Resource Modules: Represent specific resources or infrastructure patterns (e.g., EC2 instance, VPC).
    
3. Application Modules: Focus on deploying and managing application components (e.g., ECS, Lambda).
    
4. Composite Modules: Combine lower-level modules into cohesive solutions (e.g., application + network modules).
    
5. Utility Modules: Provide generic functionalities or reusable components (e.g., monitoring, security groups).
    

# **Difference between Root Module and Child Module**

* The Root Module in Terraform is the main entry point of a Terraform configuration. It is typically represented by the top-level directory containing the main Terraform files.
    
* The Root Module defines the infrastructure components, providers, and variables used in the configuration. It may also include references to Child Modules.
    
* Child Modules are self-contained modules that encapsulate specific sets of resources and configurations. They can be referenced and used within the Root Module.
    
* Child Modules promote code reuse, modularity, and separation of concerns. They enable the organization and reusability of infrastructure code by encapsulating specific functionality or infrastructure patterns, making it easier to manage and maintain complex configurations.
    

# **Modules and Namespaces are the same? Justify your answer for both Yes/No**

* No, modules and namespaces are not the same.
    
* Modules in Terraform refer to self-contained units of infrastructure code that encapsulate resources and configurations. They promote code reuse, modularity, and organization of infrastructure code. Modules allow for abstraction, reusability, and easier management of complex configurations.
    
* While Namespaces provide a way to group and organize related entities, such as classes, functions, or variables, within a codebase. It helps prevent naming conflicts by providing a unique scope for entities within the namespace. Namespace enables logical separation and isolation of code components, improving code organization and readability.
    
* On a short note, we can say that modules focus on packaging and reusing code or resources, while namespaces primarily address code organization, isolation, and avoiding naming conflicts within a codebase.
    

# **Below is the file structure for modules:**

```plaintext
📁 terraform-project 
    --📄 terraform.tf 
    --📄 provider.tf 
    --📄 main.tf

📁 terraform-project/modules/my-app 
    --📄 variables.tf 
    --📄 ec2.tf 
    --📄 s3.tf 
    --📄 dynamo.tf
```

![](https://miro.medium.com/v2/resize:fit:875/0*D8GuxeZFvkE5-EeE align="left")

# **Create an AWS infrastructure using Terraform Module**

* Create a [`variable.tf`](http://variable.tf) file and mentioned all the variables here only and provide the type of variable as "string"
    

```plaintext
  variable "ami" {
         type = string
  }

  variable "instance_type"{
      type = string
  }

  variable "instance_name"{
      type = string
  }

  variable "bucket_name"{
      type = string
  }

  variable "dynamo_table_name"{
      type = string
  }

  variable "my_environment"{
     type = string
  }
```

* Create a file [`ec2.tf`](http://ec2.tf) and inside it provides all details related to instances like the number of ec2 to be created, AMI Id, instance type and name of the instance using variables.
    

```plaintext
  resource "aws_instance" "my_instance"{
      count = 2
      ami = var.ami
      instance_type = var.instance_type
      tags = {
           Name = "${var.my_environment}-${var.instance_name}"
     }
  }
```

* Create a [`s3.tf`](http://s3.tf) file and add details related to the s3 bucket name.
    

```plaintext
  resource "aws_s3_bucket" "my_bucket"{
       bucket = "${var.my_environment}-${var.bucket_name}"
  }
```

* Create a [`dynamo.tf`](http://dynamo.tf) file and add details related to dynamodb like name, billing mode, hash key and attribute using variables.
    

```plaintext
  resource "aws_dynamodb_table" "my_table"{
       name = "${var.my_environment}-${var.dynamo_table_name}"
       billing_mode = "PAY_PER_REQUEST"
       hash_key = "UserID"
       attribute{
           name = "UserID"
           type = "S"
       }
  }
```

* In the terraform-project or main directory of the project add [`terraform.tf`](http://terraform.tf) for add details of AWS provider.
    

```plaintext
  terraform {
    required_providers {
      aws = {
        source  = "hashicorp/aws"
        version = "~> 4.0"
      }
    }
  }
```

[`provider.tf`](http://provider.tf)

```plaintext
  provider "aws"{
     region = "us-east-1"
  }
```

* Now create a [`main.tf`](http://main.tf) file and here add all the values of variables that make our project modular.
    

```plaintext
  module "dev-app"{
     source = "./modules/my-app"
     my_environment = "dev"
     ami = "ami-053b0d53c279acc90"
     instance_type = "t2.micro"
     instance_name = "Server"
     bucket_name = "day70-bucket-my-app1"
     dynamo_table_name = "day70-table-my-app1"
  }

  module "prd-app"{
     source = "./modules/my-app"
     my_environment = "prd"
     ami = "ami-053b0d53c279acc90"
     instance_type = "t2.micro"
     instance_name = "Server"
     bucket_name = "day70-bucket-my-app1"
     dynamo_table_name = "day70-table-my-app1"
  }
```

* To get the ip address of the newly created ec2 instances we can create [`output.tf`](http://output.tf) and add the following code.
    

```plaintext
  output "my_ec2_ip"{
    value = aws.instance.my_instance[*].public_ip
  }
```

* Once all the file setup is done, now execute the `terraform init` command.
    

![](https://miro.medium.com/v2/resize:fit:875/0*IsTRtvsSOIgGTYcO align="left")

* Once all the prerequisite plugins is satisfied, execute the terraform plan commands to check as our infrastructure met the conditions that we are provided.
    

![](https://miro.medium.com/v2/resize:fit:875/0*MPHqWRomo7rphu4P align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*-hRP2U6DUQgi2gI7 align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*ouvloe3Geomwgh6H align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*CvJkemYFfVBpveHY align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*FHkMcDNQQYPWBo9y align="left")

* Once `terraform plan` is successfully executed, now execute the `terraform apply` command to create our complete infrastructure.
    

![](https://miro.medium.com/v2/resize:fit:875/0*njKJJ9aFxNvQUhmU align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*CtyLjAXT63WeAQ_p align="left")

* As the process is successfully completed, we can see 4 new EC2 instances out of which 2 for the prd environment and 2 for the dev environment.
    

![](https://miro.medium.com/v2/resize:fit:875/0*sTnBzJ54bvIMEWFX align="left")

* 2 new s3 bucket is also created for both prd and dev environment.
    

![](https://miro.medium.com/v2/resize:fit:875/0*60ksly5HzgRaMGOd align="left")

* Same like s3 bucket, with 2 new Dynamodb tables is created for both prd and dev environments.
    

![](https://miro.medium.com/v2/resize:fit:875/0*ZhYblS6adbDR9Kwi align="left")

* Using `terraform state list` command you can list out all the states of your infrastructure.
    

![](https://miro.medium.com/v2/resize:fit:875/0*H_0MqfjUe02xeUpa align="left")

* To view the state of a particular module we can use
    

```plaintext
   terraform state show <module-name>
```

![](https://miro.medium.com/v2/resize:fit:875/0*oTU-VxTlYQ2EJCYB align="left")

* To destroy the particular state of a particular module we can use
    

```plaintext
terraform destroy -target <mod>
```

![](https://miro.medium.com/v2/resize:fit:875/0*nErrD8Y9KSLrpmRz align="left")

As we wrap up our journey through the world of Terraform Modules, we hope you’ve gained a deeper understanding of this powerful tool and how it can revolutionize your infrastructure management. The concepts, differences, and practical applications explored in this series will equip you with the knowledge needed to optimize your infrastructure provisioning process.

We value your feedback and encourage you to share your thoughts and experiences. Connect with me on LinkedIn [here](https://www.linkedin.com/in/mudit--mathur/) to provide your insights, ask questions, or stay updated on future discussions in the world of Terraform and infrastructure automation.

Thank you for joining us on this enlightening expedition, and we look forward to sharing more valuable insights with you in the future. Keep exploring, keep learning, and keep automating your infrastructure. Until next time!