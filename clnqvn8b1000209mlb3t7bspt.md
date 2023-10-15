---
title: "Terraform Basics"
datePublished: Sun Oct 15 2023 02:58:32 GMT+0000 (Coordinated Universal Time)
cuid: clnqvn8b1000209mlb3t7bspt
slug: terraform-basics
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697338631486/b50eba34-a86e-4cdc-ab61-1282fbeb5190.png
tags: aws, devops, terraform, iac, 90daysofdevops

---

Welcome to the world of Infrastructure as Code (IaC), where we leverage the power of code to shape and manage our infrastructure. At the heart of this transformative approach lies Terraform, a versatile tool by HashiCorp.

Terraform empowers you to define, provision, and maintain your infrastructure using the HashiCorp Configuration Language (HCL).

In this exploration, we’ll delve into why Terraform is indispensable for modern infrastructure management and gain a grasp of essential terms and concepts, such as Providers, Resources, Modules, Outputs, State, and the building blocks of HCL.

# **What is Infrastructure as Code (IaC)?**

* Infrastructure as Code (IaC) is a software engineering practice that allows the provisioning, configuration, and management of infrastructure resources through machine-readable definition files.
    
* With Infrastructure as Code, infrastructure resources are defined using declarative or imperative code written in a domain-specific language (DSL) or a general-purpose programming language.
    
* There are several popular tools and frameworks available for implementing Infrastructure as Code out of which Terraform is one of the popular IaC tools.
    
* In Terraform we write the configuration file using HashiCorp Configuration Language (HCL).
    

# **What is Terraform?**

* Terraform is an open-source Infrastructure as Code (IaC) tool developed by HashiCorp. It enables the provisioning, configuration, and management of infrastructure resources across various cloud providers and platforms in a declarative and automated manner.
    
* With Terraform, infrastructure is defined using a declarative language called HashiCorp Configuration Language (HCL) or JSON. This language allows you to describe the desired state of your infrastructure, specifying resources, their configurations, dependencies, and relationships. The Terraform configuration files define the infrastructure as code, which can be version-controlled, shared, and collaboratively developed.
    

# **What is HCL?**

* HCL stands for HashiCorp Configuration Language. It is the language used in Terraform for defining infrastructure configurations and resources.
    
* HCL is a declarative language designed to be easy to read and write, allowing users to express their infrastructure requirements in a human-friendly and intuitive manner.
    
* HCL is specifically created for managing infrastructure as code and provides a structured and concise syntax for defining resources, their configurations, and their relationships.
    
* It enables users to describe the desired state of their infrastructure in a Terraform configuration file, which is typically named with the `.tf` extension.
    

# **Why do we use terraform?**

1. Automation and Efficiency: With Terraform, infrastructure provisioning and management tasks can be automated, reducing manual effort and human error.
    
2. Multi-Cloud and Hybrid Cloud Support: Terraform supports a wide range of cloud providers, including Amazon Web Services (AWS), Microsoft Azure, Google Cloud Platform (GCP), and others.
    
3. Infrastructure State Management: Terraform maintains a state file that tracks the current state of the infrastructure managed by Terraform.
    
4. Modularity and Reusability: Terraform supports modularization, allowing users to create reusable modules that encapsulate specific infrastructure configurations.
    
5. Dependency Management and Resource Relationships: Terraform handles dependencies between resources and manages their relationships. It automatically determines the correct order in which resources should be provisioned or modified based on their dependencies.
    
6. Community and Ecosystem: Terraform has a large and active community, contributing to its rich ecosystem. This includes a vast number of provider plugins for integrating with various services and technologies.
    

# **Important Terminologies in Terraform**

# **Provider**

* A provider is a plugin in Terraform that is responsible for interacting with a specific cloud provider or service.
    
* Providers are used to manage and provision resources within the target infrastructure. Examples of providers include AWS, Azure, Google Cloud, and more.
    
* Each provider has its own set of resources and configuration options.
    

```plaintext
provider "aws" {
  region = "ap-south-1"
}
```

# **Resource**

* A resource represents a specific infrastructure object that Terraform manages. Resources can be virtual machines, databases, networks, load balancers, or any other entity offered by the cloud provider.
    
* Each resource has a specific configuration block that defines its properties and settings.
    
* Terraform provisions, modify or destroys resources based on their definitions.
    

```plaintext
  resource "aws_instance" "my_instance"{
      count = 5
      ami="<ami-id>"
      instance_type = "t2.micro"
      tags={
           Name = "terra-instance-server"
     }
  }
```

# **Module**

* A module is a reusable unit of infrastructure configuration. It encapsulates a set of resources and configurations that can be used to create and manage infrastructure components.
    
* Modules promote modularity, code reuse, and maintainability by abstracting complex configurations into manageable units.
    
* Modules can be used across different projects or shared within a team, making infrastructure configurations more maintainable and scalable.
    

```plaintext
module "dev-app" {
  source = "./modules/my-app"
  my_environment = "dev"
  ami = "<ami-id>"
  instance_type = "t2.micro"
  instance_name = "demo"
  bucket_name = "demo-bucket-my-app"
  dynamo_table_name = "demo-table-my-app"
}
```

# **Output**

* Outputs are values that are derived from the Terraform configuration and can be used to provide information about the infrastructure to external systems or users.
    
* Outputs are typically used to expose important details such as IP addresses, URLs, or resource identifiers for reference or consumption by other components.
    
* They are useful for sharing important information with other parts of your infrastructure or with users who need to access or interact with the provisioned resources.
    

```plaintext
  output "my_ec2_ip"{
    value = aws.instance.my_instance[*].public_ip
  }
```

# **State**

* The state in Terraform represents the current state of the infrastructure being managed. It is a record of the resources and their configurations defined in the Terraform configuration files.
    
* The state file contains metadata about resources, their attributes, dependencies, and relationships.
    
* Terraform uses this state file to understand the existing infrastructure, track changes, and plan and execute updates in a controlled manner.
    

```plaintext
provider "aws" {
  region = "ap-south-1"
}

resource "aws_s3_bucket" "my_bucket" {
  bucket = "cf-s3-..."
  acl    = "private"
}

resource "aws_s3_bucket_public_access_block" "example" {
  bucket = aws_s3_bucket.my_bucket.id
}

resource "aws_s3_bucket_logging" "example" {
  bucket = aws_s3_bucket.my_bucket.id

  target_bucket = aws_s3_bucket.my_bucket.id
  target_prefix = "logs/"
}

resource "aws_s3_bucket_notification" "example" {
  bucket = aws_s3_bucket.my_bucket.id

  lambda_function {
    lambda_function_arn = aws_lambda_function.my_lambda_function.arn
    events              = ["s3:ObjectCreated:*"]
    filter_prefix       = "uploads/"
    filter_suffix       = ".jpg"
  }
}
```

# **Backend**

* The backend in Terraform defines where Terraform state files are stored. This can be a local file system, remote storage services like Amazon S3 or Azure Blob Storage, or a version control system like Git.
    
* The backend configuration determines how the state is accessed and shared among team members.
    

```plaintext
  terraform {
    backend "remote" {
      organization = "example_corp"

      workspaces {
        name = "my-app-prod"
      }
    }
  }
```

# **Components of HCL**

# **Blocks**

* HCL organizes configurations into blocks, which are enclosed within curly braces `{}`.
    
* Blocks define different aspects of the configuration, such as the provider, resource, variable, or output. Each block has a specific purpose and contains configuration settings specific to that block type.
    

# **Arguments**

* Within blocks, you define arguments to set the configuration values for resources or other block types.
    
* Arguments are specified using the `key = value` syntax, where the key represents the configuration setting name and the value represents the desired value for that setting.
    
* Here’s an example of an `aws_instance` block with parameters and arguments:
    

```plaintext
resource "aws_instance" "example" {
  instance_type = "t2.micro"              # Set the instance type to t2.micro
  ami           = "ami-12345678"          # Updated the AMI ID (replace with the desired AMI)
  key_name      = "my-key-pair"          # Added a key_name for SSH access (replace with your key pair)
  subnet_id     = "subnet-12345678"       # Added a specific subnet ID (replace with your subnet)
}
```

# **Variables**

* Variables in HCL are used to parameterize configurations and provide flexibility. They allow you to define placeholders for values that can be assigned from external sources or passed as input to your configuration.
    
* Variables are defined using the `variable` block and can have a default value or be defined as required.
    

```plaintext
variable "region" {
  type    = string
  default = "ap-south-1"
}
```

# **Expressions and Interpolation**

* HCL supports expressions and interpolation, allowing you to dynamically generate or reference values within the configuration.
    
* Expressions can be used to perform calculations, concatenate strings, or define conditional logic. Interpolation is used to reference values of variables or attributes of resources within other parts of the configuration.
    

```plaintext
  resource "aws_instance" "example" {
    instance_type = var.instance_type
    ami           = data.aws_ami.ubuntu.id
  }
```

# **Blocks Within Blocks**

* HCL allows the nesting of blocks within other blocks to define hierarchical relationships and configurations. This enables you to express more complex infrastructures and relationships between resources.
    

```plaintext
provider "aws" {
  region = "ap-south-1"
}

resource "aws_vpc" "main" {
  cidr_block = "10.0.0.0/16"

  tags = {
    Name = "main-vpc"
  }

  subnet {
    cidr_block        = "10.0.1.0/24"
    availability_zone = "ap-south-1a"
  }
}
```

# **Comments**

* HCL allows you to include comments within the configuration files to provide explanations, document decisions, or add any relevant information.
    
* Single-line comments start with `'#'` and multi-line comments are enclosed within `/* */`.
    

```plaintext
  # This is a single-line comment

  /*
  This is a multi-line comment.
  It can span multiple lines.
  */
```

# **Task 1: Install Terraform on your system**

Create an EC2 instance and SSH into it.

![](https://miro.medium.com/v2/resize:fit:875/0*dgO4nkN5tQ1hdHgu align="left")

Visit the official Terraform website to get the installation step. [Install Terraform](https://developer.hashicorp.com/terraform/downloads)

![](https://miro.medium.com/v2/resize:fit:875/1*IlmI7ZJwxI7Ag_EwcdjrBg.png align="left")

For our EC2 Linux machine installation follow the below command:

```plaintext
 sudo apt-get update

 wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg

 echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list

 sudo apt update && sudo apt install terraform
```

![](https://miro.medium.com/v2/resize:fit:875/0*r1iWyJSSypvV_O9g align="left")

Verify that Terraform is installed correctly by running the following command:

```plaintext
 terraform --version
```

![](https://miro.medium.com/v2/resize:fit:875/0*0_X-8EGhTYVIHNp8 align="left")

# **Task 2:**

# **What is the State file in Terraform? What’s the importance of it?**

* The state file in Terraform is a JSON file that stores the current state of the managed infrastructure. It contains metadata about provisioned resources, their attributes, dependencies, and relationships.
    
* The state file serves as a single source of truth for Terraform, enabling it to understand the existing infrastructure and track changes over time. It plays a crucial role in planning, applying, and destroying infrastructure.
    
* The state file ensures idempotent operations, facilitates collaboration among team members, manages resource dependencies, and enables reproducibility.
    
* It helps Terraform generate execution plans, validate configurations, and maintain the desired infrastructure state.
    
* Proper management and version control of the state file is essential for maintaining consistency and ensuring accurate infrastructure management.
    

# **What is Desired and Current State?**

* In Terraform, the “Desired State” refers to the configuration and settings specified in the Terraform code that describes the desired end state of the infrastructure. It represents the state you want your infrastructure to be in, such as the resources to create, modify, or delete their properties, and their relationships.
    
* The “Current State” refers to the actual state of the infrastructure as tracked by Terraform. It is recorded in the state file and includes information about the provisioned resources, their attributes, and their dependencies. The current state reflects the real-world state of the infrastructure at any given point in time.
    

In this blog, we’ve delved into the realm of Infrastructure as Code (IaC) and explored the power of Terraform, accompanied by the HashiCorp Configuration Language (HCL). From understanding Terraform’s significance to mastering fundamental Terraform terms like Provider, Resource, Module, Output, State, Backend, and HCL’s core components including Blocks, Arguments, Variables, Expressions, and Interpolation, you’ve embarked on a journey to revolutionize infrastructure management. We’ve even equipped you with the skills to install Terraform on your system.

As we demystified the critical State file and its integral role in tracking and evolving infrastructure, you’ve grasped the essence of Desired and Current State, the bedrock of maintaining infrastructure as code.

Moreover, your feedback is invaluable to us. We encourage you to connect with me on LinkedIn at Mudit Mathur ([https://www.linkedin.com/in/mudit--mathur/](https://www.linkedin.com/in/mudit--mathur/)) to share your thoughts, questions, or engage in further discussions. Your input plays a pivotal role in shaping our content. Join the conversation and follow my journey at #90daysofdevops to stay connected and stay informed. day60