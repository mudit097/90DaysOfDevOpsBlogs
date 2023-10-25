---
title: "Terraform with AWS"
datePublished: Sun Oct 22 2023 18:07:00 GMT+0000 (Coordinated Universal Time)
cuid: clo1s6htf00010akxehhpajb1
slug: terraform-with-aws
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697997895307/fd62470a-a8dc-4908-af7f-c9e2a1c73c7d.png
tags: aws, devops, terraform, 90daysofdevops, trainwithshubham

---

Welcome to our blog on leveraging the combined strength of Terraform and AWS! Dive into the world of Infrastructure as Code (IaC) as we explore how Terraform simplifies the provisioning and management of AWS resources. Discover step-by-step guides, and best practices empowering you to build and manage scalable infrastructure in the AWS cloud.

# **Prerequisites**

# **Step -1: AWS CLI installed**

The AWS Command Line Interface (AWS CLI) is a unified tool to manage your AWS services. With AWS CLI configured we can interact with AWS services directly from your command line. We can use various AWS CLI commands to manage and configure your AWS resources.

```plaintext
sudo apt-get update

sudo apt install awscli -y

aws --version
```

![](https://miro.medium.com/v2/resize:fit:875/0*aSO--bC0TqPqpXAG align="left")

# **Step -2: AWS IAM User**

IAM (Identity Access Management) AWS Identity and Access Management (IAM) is a web service that helps you securely control access to AWS resources. Use IAM to grant a user to provide admin privileges and get the Access Key for that.

To connect your AWS account and Terraform, you need the access keys and secret access keys exported to your machine which we already got from AWS IAM User.

```plaintext
export AWS_ACCESS_KEY_ID=<access key>
export AWS_SECRET_ACCESS_KEY=<secret access key>
```

![](https://miro.medium.com/v2/resize:fit:875/0*v9g_BFTjCAqqYfqf align="left")

# **Step -3: Install AWS Providers**

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

Add the region where you want your instances to be

```plaintext
provider "aws" {
  region = "us-east-1"
}
```

# **Task-01**

* Create a terraform file named [`main.tf`](http://main.tf) provision an AWS EC2 instance using terraform aws provider.
    

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

![](https://miro.medium.com/v2/resize:fit:875/0*C1NY1xHqdRGN9aKk align="left")

* Create a [`providers.tf`](http://providers.tf) and put the selected AWS Region that you want to create an EC2 instance.
    

```plaintext
  provider "aws" {
    region = "us-east-1"
  }
```

![](https://miro.medium.com/v2/resize:fit:875/0*zwi3KSdfgZ2bMLKG align="left")

* In the [`aws.tf`](http://aws.tf) provide all the details like AMI ID, instance type and instance name and the number of EC2 count that has to be created.
    

```plaintext
  resource "aws_instance" "aws_ec2_test" {
          count = 1
          ami = "ami-053b0d53c279acc90"
          instance_type = "t2.micro"
          tags = {
             Name = "TerraformTestServerInstance"
    }
  }
```

![](https://miro.medium.com/v2/resize:fit:875/0*EKtkaHSqX_-tszph align="left")

* Now the first step is to initialize the working directory with the necessary plugins and modules by executing `terraform init`
    

![](https://miro.medium.com/v2/resize:fit:875/0*Q0kFf6adnYMqQrkV align="left")

* Once you initialize all the plugins required for AWS, now execute the `terraform plan` which will create an execution plan by analyzing the changes required to achieve the desired state of your infrastructure.
    

![](https://miro.medium.com/v2/resize:fit:875/0*ewiz72OFWrZzFsmE align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*IwRms2NEhMooeas4 align="left")

* Finally, use the command `terraform apply` it will apply the changes to create or update resources as needed
    

![](https://miro.medium.com/v2/resize:fit:875/0*QYVA72TbqryHGtRg align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*tGGkIvZFJMC_Udo7 align="left")

* You can check, a new EC2 instance is created using Terraform as we provided a count as 1.
    

![](https://miro.medium.com/v2/resize:fit:875/0*BhzQZuWxjG9S27bf align="left")

* Once you are done with the newly created instance we can use `terraform destroy` command which will delete the complete infrastructure.
    

![](https://miro.medium.com/v2/resize:fit:875/0*LzcLShFheZzHeg-r align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*V7Csyc38zfHsaNfO align="left")

* Now from EC2 Instance, we can verify that the newly created EC2 instance is in the terminated state.
    

![](https://miro.medium.com/v2/resize:fit:875/0*S7IODn-mxiHCTsTj align="left")

In this blog, we have learned the essential prerequisites for AWS infrastructure provisioning, including AWS CLI installation, IAM User setup, and AWS Providers installation.

We’ve also embarked on our AWS infrastructure automation journey with Task-01. This blog has set the stage for further learning and exploration in the realm of DevOps, Infrastructure as Code (IAC), and infrastructure management.

Your engagement and feedback are highly encouraged to enhance our collective DevOps and infrastructure skills.

Connect with me on LinkedIn [https://www.linkedin.com/in/mudit--mathur/](https://www.linkedin.com/in/mudit--mathur/)) to continue the conversation and learning. Day 64