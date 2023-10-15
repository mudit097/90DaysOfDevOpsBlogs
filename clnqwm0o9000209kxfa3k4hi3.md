---
title: "Terraform Commands"
datePublished: Sun Oct 15 2023 03:25:35 GMT+0000 (Coordinated Universal Time)
cuid: clnqwm0o9000209kxfa3k4hi3
slug: terraform-commands
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697340218881/a657d197-538d-42f9-a956-b0f0b4a6348d.png
tags: aws, devops, terraform, 90daysofdevops, trainwithshubham

---

In today’s fast-evolving world of IT and cloud computing, Infrastructure as Code (IAC) is transforming the way organizations manage their infrastructure.

This comprehensive guide will help you master IAC, beginning with fundamental Terraform commands. We’ll then explore Terraform’s competitors, such as Ansible, AWS CloudFormation, Puppet, Chef, Kubernetes, and Packer.

By the end of this journey, you’ll have a solid understanding of these tools, enabling you to make informed choices for your infrastructure needs. So, let’s dive into the world of IAC and take your infrastructure management to the next level.

# **Basic Terraform commands**

1. terraform init
    

The `terraform init` command initializes a working directory containing Terraform configuration files. This is the first command that should be run after writing a new Terraform configuration or cloning an existing one from version control.

2\. terraform init -upgrade

The `-upgrade` option for the `terraform init` command is used to upgrade modules and plugins. This can be useful if you want Terraform to ignore the dependency lock file and consider installing newer versions.

3\. terraform plan

The `terraform plan` command creates an execution plan, which lets you preview the changes that Terraform plans to make to your infrastructure. By default, when Terraform creates a plan it reads the current state of any already-existing remote objects to make sure that the Terraform state is up-to-date

4\. terraform apply

The `terraform apply` command is used to deploy your infrastructure according to the configuration files or a pre-determined execution plan. It can perform changes to the real infrastructure environment or the desired state of the configuration

5\. terraform validate

The `terraform validate` command checks the syntax and internal consistency of Terraform configuration files in a directory. It does not access any remote services or state files.

6\. terraform fmt

The `terraform fmt` command is used to rewrite Terraform configuration files to a canonical format and style which it easier to maintain & read.

7\. terraform destroy

The `terraform destroy` command to delete the resources created using the apply command. The destroy command is an essential part of the Terraform workflow, allowing users to clean up resources that are no longer needed.

8\. terraform refresh

The `terraform refresh` command is used to reconcile the Terraform state with the actual infrastructure resources. It updates the state file with the current state of the resources without making any changes to the infrastructure.

# **Terraform’s main competitors**

# **Ansible**

Ansible is an open-source automation tool that supports infrastructure provisioning and configuration management. Ansible uses YAML-based playbooks for managing infrastructure. Ansible is known for its agentless architecture and its ability to automate tasks across multiple platforms.

# **AWS CloudFormation**

AWS CloudFormation is a native infrastructure provisioning tool provided by Amazon Web Services (AWS). It allows users to define infrastructure resources and their dependencies using YAML or JSON templates. CloudFormation integrates seamlessly with other AWS services and provides a declarative approach to infrastructure provisioning within the AWS ecosystem.

# **Puppet**

Puppet is a popular open-source Infrastructure provisioning tool. It uses declarative language to define system configurations and automate the deployment and management of software and infrastructure. Puppet supports various operating systems and provides a centralized management platform.

# **Chef**

Chef is an open-source tool that follows a model-driven approach to Configuration Management. It uses a domain-specific language (DSL) called Chef Infra to define system configurations and automate the provisioning and management of infrastructure. Chef offers flexibility and supports multiple platforms and cloud providers.

# **Kubernetes**

Kubernetes Infrastructure as Code (IaC) refers to the practice of using declarative configuration files to define and manage Kubernetes infrastructure. With Kubernetes IaC, infrastructure resources such as pods, services, deployments, and ingress rules are defined in YAML or JSON files.

# **Packer**

Packer Infrastructure as Code (IaC) involves using declarative configuration files to define and automate the creation of machine images across multiple platforms. Packer allows you to define image templates using JSON or HCL configuration files.

In this comprehensive guide, we’ve journeyed through the dynamic world of Infrastructure as Code (IAC), starting with Terraform’s foundational principles. From mastering Terraform’s basics to understanding its competitors, including Ansible, AWS CloudFormation, Puppet, Chef, Kubernetes, and Packer, you’ve gained essential insights into modern infrastructure management.

As you embark on your own IAC adventures, remember that the power of these tools lies in their flexibility. They empower you to mold your infrastructure to suit your needs and adapt to the ever-changing IT landscape. Whether you’re streamlining resource provisioning with Terraform, automating configuration management with Ansible, or orchestrating containers with Kubernetes, your infrastructure can now be more efficient and agile than ever before.

If you have questions, seek further guidance, or simply wish to discuss DevOps, IAC, or infrastructure management in general, please connect with me on [https://www.linkedin.com/in/mudit--mathur/](https://www.linkedin.com/in/mudit--mathur/)). Your feedback and insights are invaluable as we all strive to enhance our DevOps and infrastructure skills.

Best of luck on your “90 Days of DevOps” journey, and may your infrastructure endeavors be both transformative and rewarding.

Day 61