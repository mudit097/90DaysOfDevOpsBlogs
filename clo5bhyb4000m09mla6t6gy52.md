---
title: "Terraform Interview Q&A"
datePublished: Wed Oct 25 2023 05:31:06 GMT+0000 (Coordinated Universal Time)
cuid: clo5bhyb4000m09mla6t6gy52
slug: terraform-interview-qa
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1698211583734/61334e11-cd5d-4daa-93bb-b911a2d47641.png
tags: interview, aws, devops, terraform, trainwithshubham

---

## **Top Terraform Interview Questions**

### 1️⃣What is Terraform and how it is different from other IaaC tools?

Terraform is an infrastructure-as-code (IaaC) tool used to provision and manage cloud resources. Unlike other IaaC tools, Terraform is cloud-agnostic, supporting multiple providers, and uses a declarative configuration language. It enables infrastructure automation, collaboration, and version control across different cloud platforms.

### **2️⃣Define Terraform init?**

Terraform initialises the code with the command [**terraform init**](https://k21academy.com/terraform-iac/terraform-workflow-and-its-use-case/). This command is used to set up the working directory for Terraform configuration files. It is safe to run this command multiple times.

You can use the init command for:

1. Installing Plugins
    
2. Installation of a Child Module
    
3. Initialization of the backend
    

### 3️⃣**What are Terraform providers?**

Terraform providers are plugins that allow Terraform to interact with different infrastructure services, such as Azure,AWS , Google Cloud and Kubernetes. Providers define a set of resources and their corresponding operations that Terraform can manage.

### 4️⃣**What is a Terraform module?**

A Terraform module is a reusable and self-contained code defining a set of infrastructure resources. Modules such as web servers, databases, or networking resources can create complex infrastructure configurations and be shared and reused across different projects or environments.

### 5️⃣**Explain the purpose of Terraform in DevOps.**

Terraform is a tool commonly used in DevOps to manage infrastructure as code. It utilizes the HashiCorp Configuration Language (HCL), similar to JSON, to provide a streamlined and easily understandable syntax for defining infrastructure settings across various cloud and on-premises environments. This simplifies the process of setting up and maintaining infrastructure for DevOps teams.

### 6️⃣**How does Terraform work?**

Terraform creates an implementation plan, defines what it will do to achieve the desired state, and then executes it to build the infrastructure described. Terraform is capable of determining what changed and generating incremental execution plans that are practical as the configuration changes**.**

### 7️⃣**Name some major features of Terraform?**

* Execution Plan
    
* Change Automation
    
* Resource Graph
    
* Infrastructure as code
    

### 8️⃣ **How to check the installed version of Terraform?**

We can use `terraform -version` of the command to identify the version which we are running.

### 9️⃣**Describe the working of Terraform core?**

The terraform core examines configuration monitoring and generates configuration-based analysis and evaluation. It keeps track of and compares versions (current and previous) before displaying the results via the terminal.

**Terraform core mainly takes two inputs:**

* Terraform Configuration – It keeps track of the infrastructure detail
    
* Terraform state – It keeps track of the infrastructure status.
    

### 1️⃣0️⃣**What do you understand about Terraform backend?**

Terraform, a backend refers to the storage and retrieval mechanism for Terraform state files. The Terraform state file is a critical component that keeps track of the current state of the infrastructure that Terraform manages. It contains information about the resources Terraform has created, their current state, and the relationships between them.

### 1️⃣1️⃣What exactly is Sentinel? Can you provide few examples that we can use for Sentinel policies?

* Sentinel is a policy-as-code framework developed by HashiCorp. It integrates with various HashiCorp tools, including Terraform, to enforce governance and security policies.
    
* Sentinel enables the creation of custom policies to control infrastructure provisioning and deployment. Examples of Sentinel policies include enforcing tagging conventions, validating resource configurations, restricting access to certain regions, enforcing encryption requirements, and ensuring compliance with regulatory standards.
    
* Sentinel provides fine-grained control over infrastructure deployments by evaluating policy rules before changes are applied.
    

### 1️⃣2️⃣ You have a Terraform configuration file that defines an infrastructure deployment. However, there are multiple instances of the same resource that need to be created. How would you modify the configuration file to achieve this?

To create multiple instances of the same resource in Terraform, you can use resource "count" or resource "for\_each" depending on your specific requirements. By setting the count or for\_each argument with an appropriate value, you can dynamically create and manage multiple instances of the resource within your configuration file.

### 1️⃣3️⃣ You want to know from which paths Terraform is loading providers referenced in your Terraform configuration (\*.tf files). You need to enable debug messages to find this out. Which of the following would achieve this?

To enable debug messages in Terraform and identify the paths from which providers are loaded, you can set the `TF_LOG` environment variable to `DEBUG` before running Terraform commands. This will display detailed debug logs, including information about provider loading, allowing you to determine the paths referenced in your Terraform configuration.

A. <mark>Set the environment variable TF_LOG=TRACE</mark>

B. Set verbose logging for each provider in your Terraform configuration

C. Set the environment variable TF\_VAR\_log=TRACE

D. Set the environment variable TF\_LOG\_PATH

### 1️⃣4️⃣ Below command will destroy everything that is being created in the infrastructure. Tell us how would you save any particular resource while destroying the complete infrastructure.

```plaintext
terraform destroy
```

### 1️⃣5️⃣Which module is used to store .tfstate file in S3?

The "terraform\_backend\_s3" module is commonly used to store the .tfstate file in an S3 bucket. It provides a convenient way to configure the backend in Terraform, allowing for state storage, locking, and versioning in an S3 bucket.

### 1️⃣6️⃣How do you manage sensitive data in Terraform, such as API keys or passwords?

Sensitive data in Terraform, like API keys or passwords, should be stored securely outside the code. Common practices include using environment variables, secret management systems like HashiCorp Vault, or integration with cloud provider-specific services like AWS Secrets Manager or Azure Key Vault.

### 1️⃣7️⃣You are working on a Terraform project that needs to provision an S3 bucket, and a user with read and write access to the bucket. What resources would you use to accomplish this, and how would you configure them?

To provision an S3 bucket and a user with read and write access, you would use the "aws\_s3\_bucket" resource to create the bucket and the "aws\_iam\_user" resource to create the user. For access control, you would configure an appropriate "aws\_iam\_policy" with the necessary permissions and attach it to the user.

### 1️⃣8️⃣Who maintains Terraform providers?

Terraform providers are maintained by various organizations, including both cloud service providers (such as AWS, Azure, and Google Cloud) and independent contributors. Each provider has its own maintainers responsible for developing, updating, and supporting the provider's integration with Terraform.

### 1️⃣9️⃣How can we export data from one module to another?

To export data from one module to another in Terraform, you can use output variables. Define output variables in the module where the data is generated, and reference those outputs as input variables in the module where the data needs to be consumed.

# **Intermediate Terraform Interview Questions**

### 1️⃣**What are the most useful Terraform commands?**

Common commands:

* **terraform init**: Prepare your working directory for other commands
    
* **terraform plan**: Show changes required by the current configuration
    
* **terraform apply**: Create or update infrastructure
    
* **terraform destroy**: Destroy previously-created infrastructure
    

### 2️⃣**How does Terraform help in discovering plugins?**

Terraform interprets configuration files in the operational directory with the authority “Terraform init.” Then, Terraform determines the necessary plugins and searches for installed plugins in various locations.

### 3️⃣**Can I add policies to the open-source or pro version of Terraform enterprise?**

**Terraform** Policies cannot be added to Terraform Enterprise’s open-source description. The same is true for the Enterprise Pro edition. Terraform Enterprise’s best version could only contact the watch policies.

### 4️⃣**What do you mean by Terraform cloud?**

Terraform Cloud is an application that enables teams to use Terraform collaboratively. It manages Terraform runs in a consistent and reliable environment, and includes features such as easy access to shared state and secret data, access controls for approving infrastructure changes, a private registry for sharing Terraform modules, detailed policy controls for governing the contents of Terraform configurations, and more.

### 5️⃣**Define null resource in Terraform.**

The null resource follows the standard resource lifecycle but takes no additional actions. The trigger argument allows for the specification of a subjective set of values that, if misrepresented, will cause the reserve to be replaced.

### **6️⃣What does the following command do?**

* **Terraform -version** – to check the installed version of terraform
    
* **Terraform fmt**– it is used to rewrite configuration files in canonical styles and format
    
* **Terraform providers** – it gives information of providers working in the current configuration.
    

### 7️⃣**Mention some of the version control tools supported by Terraform.**

Version control tools supported by Terraform are:

* GitHub
    
* GitLab CE
    
* GitLab EE
    
* Bucket Cloud
    

## **Advanced Terraform Interview Questions**

### 1️⃣**How would you recover from a failed application in Terraform?**

You can save your configuration in version control and commit it before making any changes, and then use the features of your version control system to revert to an earlier configuration if necessary. You must always recommit the previous version code for it to be the new version in the version control system.

### 2️⃣**What is a Remote Backend in Terraform?**

Terraform remote backend is used to store Terraform’s state and can also run operations in Terraform Cloud. Multiple terraform commands such as init, plan, apply, destroy (terraform version &gt;= v0.11.12), get, output, providers, state (sub-commands: list, mv, pull, push, rm, show), taint, untaint, validate, and many more are available via remote backend.

### 3️⃣**How to prevent Error Duplicate Resource**

It can be done in three ways depending on the situation and the requirement

1) By deleting the resource, Terraform code will no longer manage it.  
2) By removing resources from APIs  
3) Importing action will also aid in resource elimination.

### 4️⃣**Differentiate between Terraform and Ansible.**

| **Terraform** | **Ansible** |
| --- | --- |
| Terraform is a tool for provisioning. | Ansible is a tool for managing configurations. |
| It uses a declarative Infrastructure as Code methodology. | It takes a procedural method. |
| It’s ideal for orchestrating cloud services and building cloud infrastructure from the ground up. | It is mostly used to configure servers with the appropriate software and to update resources that have previously been configured. |
| By default, Terraform does not allow bare metal provisioning. | The provisioning of bare metal servers is supported by Ansible. |
| In terms of packing and templating, it does not provide better support. | It includes complete packaging and templating support. |
| It is strongly influenced by lifecycle or state management. | It doesn’t have any kind of lifecycle management. It does not store the state. |

### 5️⃣**What is Terraform Directory?**

Terraform Directory, which Terraform uses to manage cached provider plugins and modules, as well as to record which workspace is currently active and the last known backend configuration in case state needs to be migrated on the next run.

### 6️⃣**Does Terraform support multi-provider deployments?**

Terraform is a powerful tool in multi-provider deployments because it is not tied to a specific infrastructure or cloud provider. You can manage all resources with the same set of configuration files, sharing variables and defining dependencies across providers.

### 7️⃣**What are Provisioners in Terraform?**

Provisioners are used to execute scripts on a local or remote machine as part of resource creation or destruction. Provisioners can be used to bootstrap a resource, cleanup before destroy, run configuration management, etc.

### 8️⃣**Define Resource Graph in Terraform.**

A resource graph is a graphical representation of the available resources. It enables the modification and creation of independent resources at the same time. Terraform creates a plan for the graph’s configuration to generate plans and refresh the state. It efficiently and effectively creates a structure to help us understand the disadvantages.

### 9️⃣**What are the various levels of Sentinel enforcement?**

Sentinel has three levels of enforcement: advisory, soft mandatory, and hard mandatory.

* **Advisory** – Logged in but permitted to pass. When a user initiates a plan that violates the policy, an advisory is issued.
    
* **Soft Mandatory** – Unless an override is specified, the policy must be followed. Overrides are only available to administrators.
    
* **Hard Mandatory** – The policy must be implemented regardless. Unless and until this policy is removed, it cannot be overridden. Terraform’s default enforcement level is this.
    

### 1️⃣0️⃣**How can you define dependencies in Terraform?**

You can use depends\_on to declare the dependency explicitly. You can also specify multiple resources in the depends-on argument, and Terraform will create the target resource after all of them have been created.

### 1️⃣1️⃣**What is the external data block in Terraform?**

The external data source allows an external program to act as a data source by exposing arbitrary data for use elsewhere in the Terraform configuration by implementing a specific protocol (defined below).

### 1️⃣2️⃣**Which value of the TF\_LOG variable provides the MOST verbose logging?**

**TRACE** is the most verbose option, and it is the default if TF\_LOG is not set to a log-level name. When logging is enabled, you can set TF\_LOG\_PATH to force the log to always be appended to a specific file.

### 1️⃣3️⃣**What is the benefit of Terraform State? What is the benefit of using modules in Terraform?**

**Terraform state** is primarily used to store bindings between remote system items and resource instances specified in your configuration. When Terraform generates a remote object in response to a configuration change, it saves the remote object’s identification to a specific resource instance and may update or remove that object in response to future configuration changes.

### 1️⃣4️⃣**Some other important terraform commands**

* ***terraform init:*** To prepare the working directory for use with Terraform, the `terraform init` command performs Backend Initialization, Child Module Installation, and Plugin Installation.
    
* ***terraform apply:*** The `terraform apply` command executes the actions proposed in a Terraform plan
    
* ***terraform apply –auto-approve:*** Skips interactive approval of plan before applying.
    
* ***terraform destroy:*** The `terraform destroy` command is a convenient way to destroy all remote objects managed by a particular Terraform configuration.
    
* ***terraform fmt:*** The `terraform fmt` command is used to rewrite Terraform configuration files to a canonical format and style
    
* ***terraform show:*** The `terraform show` command is used to provide human-readable output from a state or plan file.
    

As we conclude this interview-focused journey through Terraform, we hope you've found these questions and answers invaluable in your quest to become a Terraform expert. Remember, practice and preparation are the keys to success in any interview, and mastering Terraform is no different.

We're always open to feedback and would love to hear about your interview experiences and any additional questions you'd like to see covered. Connect with me on LinkedIn [here](https://www.linkedin.com/in/mudit--mathur/) to share your insights, questions, or to stay updated on future discussions in the world of Terraform.

Thank you for joining us on this enlightening expedition. We look forward to sharing more valuable insights and resources with you in the future. Keep exploring, keep learning, and keep excelling in the world of Terraform. Until next time!