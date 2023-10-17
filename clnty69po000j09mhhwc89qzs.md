---
title: "Terraform Variables"
datePublished: Tue Oct 17 2023 06:32:38 GMT+0000 (Coordinated Universal Time)
cuid: clnty69po000j09mhhwc89qzs
slug: terraform-variables
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697524246951/bf079b0d-0d85-46a5-ba61-0a8ab17ddfa5.png
tags: aws, devops, terraform, iac, trainwithshubham

---

In this blog, we’re about to embark on a journey through the intricate landscape of Terraform, a potent tool in the world of Infrastructure as Code (IAC). Our focus today is on two fundamental pillars of Terraform: variables and data types. These are the building blocks that allow us to create dynamic, flexible, and highly configurable infrastructure configurations.

**Chapter 1: What is Terraform Variable**

Let’s start with the basics:

**Task-01: Create a local file using Terraform**

We’ll begin by demystifying Terraform variables, which serve as the backbone for parameterization in your infrastructure code. In this task, we will roll up our sleeves and put this newfound knowledge to practical use by creating a local file using Terraform.

But that’s not all — there’s a command that plays a pivotal role in the Terraform variable ecosystem:

**terraform refresh**

In this section, we’ll explore the ‘terraform refresh’ command, shining a light on its significance in ensuring your variables are correctly loaded and utilized within your configurations.

**Chapter 2: Data Types in Terraform**

Now that you have a solid foundation in Terraform variables, let’s venture into the world of data types:

**Map**

We’ll dissect the Map data type, a powerhouse when it comes to handling key-value associations. You’ll see how it simplifies the management of structured data, making your configurations more organized and efficient.

**List**

The List data type becomes your ally in managing collections of values. We’ll provide real-world examples to showcase how it enhances the reusability of your configurations.

**Object**

The Object data type is a key player in creating readable and organized configurations. We’ll delve into how it enables you to define intricate structures within your Terraform code.

**Set**

Lastly, we’ll unveil the Set data type, which simplifies the handling of unique, non-repetitive values. This is your go-to tool for data that needs to be distinct and well-organized.

By the end of this blog, you’ll have a solid grasp of Terraform’s variables and data types, equipping you with the skills to create infrastructure configurations that are not just efficient but also adaptable and dynamic. So, let’s dive into this exploration of Terraform’s core building blocks!

# **What is Terraform Variable**

* Variables are placeholders for values that can be used within Terraform configurations. They allow for flexibility and customization by enabling users to pass values from external sources or prompt user input. Variables can be defined in Terraform configuration files or external input files.
    
* To define a variable in Terraform, you can use the “variable” block in your configuration file or create a separate “.tfvars” file. Here’s an example of defining a variable in a configuration file:
    

```plaintext
  variable "region" {
    description = "The AWS region"
    type        = string
    default     = "us-east-1"
  }
```

* In this example, we define a variable named “region” with a description, type, and default value. The variable is of type string and has a default value of “us-east-1”. You can reference this variable later in your configuration by using the syntax “${var.region}”.
    
* We can create a [variable.tf](http://variable.tf) file which will hold all the variables. These variables can be accessed by the var object in [main.tf](http://main.tf)
    

# **Task-01**

# **Create a local file using Terraform**

* Create a [variable.tf](http://variable.tf), and add details regarding file creation by providing the new file complete path.
    

```plaintext
  variable "filename" {
      default = "/home/ubuntu/terraform/terraform-variables/demo-var.txt"
  }

  variable "content" {
     default = "This is coming from a variable which was updated"
  }
```

![](https://miro.medium.com/v2/resize:fit:875/0*NVWrVhMHbElDL1Yd align="left")

* Create a [main.tf](http://main.tf) file where we will access the variables that have defined before.
    

```plaintext
  resource "local_file" "devops" {
  filename = var.filename
  content = var.content
  }
```

![](https://miro.medium.com/v2/resize:fit:875/0*Zpebko7SIdKYvbK0 align="left")

* Initializes a new terraform working directory.
    

```plaintext
  terraform init
```

![](https://miro.medium.com/v2/resize:fit:875/0*OL1DNhubdevNyV3a align="left")

* Generates an execution plan by using `terraform plan` command that shows what actions Terraform will take to reach the desired state specified in the configuration file.
    

![](https://miro.medium.com/v2/resize:fit:875/0*TKG7cknUpWsCfb14 align="left")

* Once `terraform apply` command runs, Terraform will create a file called demo-var.txt in the local directory with the content specified in the content variable that we had mentioned before.
    

![](https://miro.medium.com/v2/resize:fit:875/0*JL6hOZncVL7GoF5k align="left")

* Check whether the file is created in a specified folder using `ls` command.
    

![](https://miro.medium.com/v2/resize:fit:875/0*YcBtkWcmtQMH0C9Z align="left")

# **terraform refresh**

* The “`terraform refresh`" command in Terraform compares the current state of the infrastructure with the state defined in the Terraform configuration files. It updates the Terraform state file to reflect any changes made outside of Terraform, ensuring accurate tracking of resource status and attributes.
    
* In short, we can say this command is used to refresh the state of your configuration file and reloads the variables.
    

![](https://miro.medium.com/v2/resize:fit:875/0*uTnZVsVSmisPJvKt align="left")

# **Task-02**

* Use terraform to demonstrate usage of List, Set and Object datatypes
    
* Put proper screenshots of the outputs
    
* Use `terraform refresh`
    
* To refresh the state of your configuration file, reloads the variables
    

# **Data Types in Terraform**

# **Map**

A “map” variable is a data type used to store key-value pairs identified by a string label. It allows you to define a collection of values associated with unique keys, providing a flexible way to configure and manage resources in your infrastructure-as-code deployments.

* Inside [variable.tf](http://variable.tf) create a variable type map and put content inside it.
    

```plaintext
  variable "filename" {
      default = "/home/ubuntu/terraform/terraform-variables/terra-dt/demo-map1.txt"
  }

  variable "content" {
     default = "This is coming from a variable which was updated"
  }

  variable "file_contents" {
    type = map
    default = {
        "statement1" = "this is cool stmt1"
        "statement2" = "this is cooler stmt2"
    }
  }
```

![](https://miro.medium.com/v2/resize:fit:875/0*P5YhuW1BS0Gu0hZ- align="left")

* In this example, we use the file\_contents variable to set the content parameter of local\_file resource.
    
* Now from the [main.tf](http://main.tf) access the variables that have been created before inside [variable.tf](http://variable.tf)
    

```plaintext
  resource "local_file" "devops" {
      filename = var.filename
      content = var.file_contents["statement1"]
  }

  resource "local_file" "devops_var" {
      filename = "/home/ubuntu/terraform/terraform-variables/terra-dt/demo-map2.txt"
      content = var.file_contents["statement2"]
  }
```

![](https://miro.medium.com/v2/resize:fit:875/0*QeuncftIn9MTOBYZ align="left")

* Now initialize the terraform in the current directory using `terraform init` command.
    

![](https://miro.medium.com/v2/resize:fit:875/0*kBJtIGPlR2DLBK4P align="left")

* Once terraform is initialized and all dependencies are done, execute the `terraform plan`.
    

![](https://miro.medium.com/v2/resize:fit:875/0*RDrLxa9iAIlCAwzV align="left")

* As the terraform plan satisfies all the steps, execute the `terraform apply` command.
    

![](https://miro.medium.com/v2/resize:fit:875/0*zUk1oNRjzstVdybw align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*usXbsp_PZqGsgG7D align="left")

* We can verify the file content in the directory.
    

![](https://miro.medium.com/v2/resize:fit:875/0*a9edq5rHYbDEh8Bx align="left")

# **List:**

A list is a data type used to store ordered collections of values of the same type. It allows you to define and manage sequences of values, providing a convenient way to handle multiple elements within a single variable in your infrastructure-as-code deployments.

Here’s an example:

```plaintext
variable "file_list"{
    type = list
    default = ["/home/ubuntu/terraform/terraform-variables/terra-dt/file1.txt","/home/ubuntu/terraform/terraform-variables/terra-dt/file2.txt"]
}
```

![](https://miro.medium.com/v2/resize:fit:875/0*cGRT3mvUIQDAFLHA align="left")

* In this example, we define a variable named “file\_list” as a list of strings with a default value that contains the file path. This variable can be used in your Terraform configuration to reference the file paths defined in the list.
    

```plaintext
  resource "local_file" "devops" {
      filename = var.file_list[0]
      content = var.file_contents["statement1"]
  }

  resource "local_file" "devops_var" {
      filename = var.file_list[1]
      content = var.file_contents["statement2"]
  }
```

![](https://miro.medium.com/v2/resize:fit:875/0*TRO08mVdphmm5149 align="left")

* In this example, we use the file\_list variable to set the filename parameter of a local\_file resource. We reference the first element of the list using the square bracket notation and var.file\_list\[0\] syntax.
    
* Execute the `terraform plan` command.
    

![](https://miro.medium.com/v2/resize:fit:875/0*36bDjufD2I6R6gbz align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*nft-cEr6pvjQlU1s align="left")

* Execute the `terraform apply` the command.
    

![](https://miro.medium.com/v2/resize:fit:875/0*H3qbIottjrT354Pa align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*to1Hh5iEvEnw8CEX align="left")

* Once `terraform apply` is completed, check whether 2 files are created with different content.
    

![](https://miro.medium.com/v2/resize:fit:875/0*zdb91A-ctRx5g0t3 align="left")

# **Object**

* An object is a structural type that is used to store structured data with named attributes and each has its type.
    
* Objects are typically used to group related attributes together and provide a structured way to organize and manage data within a configuration. Object data types in Terraform are represented using maps, which are key-value pairs.
    

Here’s an example:

```plaintext
variable "example_object" {
  type = map(object({
    name  = string
    age   = number
    email = string
  }))
  default = {
    user1 = {
      name  = "John Doe"
      age   = 30
      email = "john.doe@example.com"
    }
    user2 = {
      name  = "Jane Smith"
      age   = 25
      email = "jane.smith@example.com"
    }
  }
}
```

# **Set:**

A set is an unordered collection of unique values of the same type. To define a set variable, use the set type and specify the type of elements in the set.

Here’s an example:

```plaintext
variable "security_groups" {
  type    = set
  default = ["sg-0692hl0ccdac0f320", "sg-04fg5ca004127f39e"]
}

variable "set" {
  type = set(string)
  default = ["foo","bar",]
}

output "set" {
  value = var.set
}

output "set_first_element" {
  value = var.set[0]
}
```

In this example, we define a variable named “security\_groups” as a set of strings with a default value.

As we conclude our exploration of Terraform variables and data types, we hope you've found this blog to be an enlightening journey into the world of infrastructure as code. The knowledge and skills you've gained will undoubtedly empower you to streamline your infrastructure management with Terraform.

Remember, Terraform is a versatile tool with boundless possibilities, and your mastery of its fundamentals is just the beginning. Stay curious, keep experimenting, and, most importantly, continue building, automating, and optimizing your infrastructure.

We encourage you to share your newfound insights and experiences with the Terraform community, fostering a collaborative and innovative spirit in this ever-evolving field. Together, we can shape the future of infrastructure as code.

Thank you for joining us on this adventure, and we look forward to guiding you through more Terraform insights in the future. Until then, happy coding and may your infrastructure be forever stable and scalable!