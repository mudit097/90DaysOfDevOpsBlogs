---
title: "Terraform and Docker"
datePublished: Sun Oct 15 2023 18:52:25 GMT+0000 (Coordinated Universal Time)
cuid: clnrtpxy8000409lhax1u6t13
slug: terraform-and-docker
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697395827231/646c87af-cedd-44b6-9482-4bce0de68941.png
tags: aws, devops, terraform, trainwithshubham, devops-devopsroadmap-continuousintegration-continuousdelivery-agile-automation-iac-infrastructureascode-docker-kubernetes-cloudcomputing-aws-azure-gcp-monitoring-logging-bestpractices-collaboration-softwaredevelopment-programming

---

Welcome to our blog, where we dive into the fascinating world of Terraform! In this space, we will explore Blocks and Resources in Terraform, offering insights and practical guidance to help you harness the full power of this infrastructure as code tool.

In our first task, we’ll guide you through creating a Terraform script with Blocks and Resources, including the essential Provider Block, as well as a Terraform Docker script.

Then, in our second task, we’ll focus on crafting a Resource Block for an Nginx Docker image, providing you with a hands-on approach to understanding Terraform’s capabilities. Join us as we embark on this Terraform journey, and let’s learn and grow together!

Terraform needs to be told which provider to use in the automation, hence we need to give the provider name with source and version. For Docker, we can use this block of code in your [main.tf](http://main.tf)

# **Blocks and Resources in Terraform**

* A block is a section within a configuration file that defines a specific object or behavior. Blocks are used to organize and configure resources, providers, variables, outputs, and other components of a Terraform configuration.
    
* A resource block is a specific type of block used to define and manage a resource within an infrastructure provider. It describes the desired state of a resource and instructs Terraform on how to create, update, or destroy that resource. A resource block typically includes properties such as the resource type, name, and configuration options specific to the provider.
    

Here’s an example of a resource block in a Terraform configuration file defining an Nginx image:

```plaintext
resource "docker_image" "my_nginx" {
            name = "nginx:latest"
            keep_locally = false
}
```

# **Task-01: Create a Terraform script with Blocks and Resources**

# **Provider Block**

The provider block configures the specified provider, in this case, docker. A provider is a plugin that Terraform uses to create and manage your resources.

```plaintext
provider "docker" {}
```

# **Create a Terraform Docker script with Blocks and Resources**

* Create a [`terra-docker.tf`](http://terra-docker.tf) and pass the docker provider.
    

```plaintext
  terraform {
    required_providers {
      docker = {
        source  = "kreuzwerker/docker"
        version = "~> 2.21.0"
       }
    }
  }
```

* Note: kreuzwerker/docker, is a shorthand Docker installation. [kreuzwerker docker registry](https://registry.terraform.io/providers/kreuzwerker/docker/latest/docs)
    

![](https://miro.medium.com/v2/resize:fit:875/0*yFqMTTv9EHSVakZe align="left")

# **Resource Block**

* Use resource blocks to define components of your infrastructure. A resource might be a physical or virtual component such as a Docker container, or it can be a logical resource such as a Heroku application.
    
* Resource blocks have two strings before the block: the resource type and the resource name. In this example, the first resource type is docker\_image and the name is Nginx.
    

# **Task-02: Create a Resource Block for an Nginx Docker image**

* Create a resource Block for an nginx docker image
    

```plaintext
  resource "docker_image" "my_nginx" {
              name = "nginx:latest"
              keep_locally = false
  }
```

* Create a resource Block for running a docker container for Nginx
    

```plaintext
  resource "docker_container" "my_nginx_container" {
        image = docker_image.my_nginx.name
        name = "nginx-container"   
        ports {
             internal = 80
             external = 80
      }
  }
```

![](https://miro.medium.com/v2/resize:fit:875/0*ndvxJisLxSYcOj7P align="left")

* Initializes a new or existing Terraform working directory by downloading the necessary provider plugins using `terraform init` command.
    

```plaintext
terraform init
```

![](https://miro.medium.com/v2/resize:fit:875/0*gVwWyWB7cI3Q-wd8 align="left")

* Now execute the `terraform plan` command which will create an execution plan by comparing the desired state in the configuration to the current state of the infrastructure.
    

```plaintext
terraform plan
```

![](https://miro.medium.com/v2/resize:fit:875/0*JMKTLtEriBZebexz align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*gJ_c14JgdpQLtr1y align="left")

* Execute the `terraform apply` command so all the configurations get [executed.It](http://executed.It) creates, modifies, or deletes resources as necessary to achieve the desired state, based on the execution plan generated by `terraform plan`.
    

```plaintext
  terraform apply
```

![](https://miro.medium.com/v2/resize:fit:875/0*Q_gl4yrN3_qj8Dhu align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*gzALw_o5WiMZ1ADK align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*A73Px3Vgvri7IxlD align="left")

* In case Docker is not installed use the below commands:
    

```plaintext
  sudo apt-get install docker.io -y

  sudo chown $USER /var/run/docker.sock

  docker --version
```

![](https://miro.medium.com/v2/resize:fit:875/0*Blc6fmsSsc-xPGfo align="left")

* Check docker container is created using the below command:
    

```plaintext
docker ps
```

![](https://miro.medium.com/v2/resize:fit:875/0*djOgCjnTrrHg2jx9 align="left")

* Browse public IP address, you can see the Nginx default page.
    

![](https://miro.medium.com/v2/resize:fit:875/1*n_PBaEP-6SWNw9KzhKPlIA.png align="left")

* Execute the `terraform destroy` so it will prompt for confirmation and then proceeds to delete the resources, reverting the infrastructure to its pre-Terraform state.
    

![](https://miro.medium.com/v2/resize:fit:875/0*0_xYcAB73pzy1UWF align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*Zew1UXkyCoJHuTEA align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*GOn9sKBf1UC_Szs1 align="left")

In Day 62 of my ’90 Days of DevOps’ journey, I delved into the exciting world of Terraform Blocks and Resources. I acquired knowledge about the crucial elements that make up Terraform scripts:

\- The **<mark>Provider Block</mark>**, which serves as the gateway to define the cloud or infrastructure provider for our resources. It’s the starting point that sets the stage for our infrastructure management.

\- The **<mark>Resource Block</mark>**, which I explored in depth. This component allows us to create, configure, and manage specific infrastructure resources. In this task, I put this knowledge to use by creating a Resource Block to provision an Nginx Docker image, covering key details like image name, ports, and other configurations.

I’m thrilled to share my learning journey with you, and I’m always open to questions, discussions, and insights related to DevOps, Infrastructure as Code (IAC), or infrastructure management. If you’d like to connect with me and explore these topics further, please find me on ([https://www.linkedin.com/in/mudit--mathur/](https://www.linkedin.com/in/mudit--mathur/)). Your feedback and contributions are invaluable as we all strive to enhance our DevOps and infrastructure skills.