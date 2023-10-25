---
title: "Building AWS Infrastructure Using Infrastructure as Code (IaC)"
datePublished: Wed Oct 25 2023 05:19:09 GMT+0000 (Coordinated Universal Time)
cuid: clo5b2ktp000m08mocegfd5jj
slug: building-aws-infrastructure-using-infrastructure-as-code-iac
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1698211089280/785259ee-2f34-4988-afd2-3eaaa47b380f.png
tags: aws, devops, terraform, 90daysofdevops, trainwithshubham

---

Welcome to the next leg of your Terraform adventure! In our prior lessons, you’ve gained a solid foundation in Terraform, including its configuration file, and the process of provisioning an EC2 instance with Terraform. Today, we’re going to dive deeper into Terraform’s capabilities, as we embark on a journey to create a multitude of resources. Get ready to build a VPC, Subnet, Internet Gateway, and even host a full-fledged website on an EC2 instance.

# **Project File Structure**

```plaintext
📁 terraform/terraform-aws 
    --📄 terraform.tf 
    --📄 provider.tf 
    --📄 vpc.tf
    --📄 subnet.tf 
    --📄 internetgateway.tf 
    --📄 routetable.tf 
    --📄 securitygroup.tf
    --📄 ec2.tf
    --📄 eip.tf
```

# **Step 1: Create a VPC (Virtual Private Cloud)**

* Create a [`terraform.tf`](http://terraform.tf) where you have to pass on AWS provider details.
    

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

* Add a [`provider.tf`](http://provider.tf) and add details about AWS Region that you are using.
    

```plaintext
  provider "aws" {
    region = "us-east-1"
  }
```

* Add the following code to create a VPC [`vpc.tf`](http://vpc.tf)
    

```plaintext
  resource "aws_vpc" "main" {
    cidr_block       = "10.0.0.0/16"
    tags = {
      Name = "main"
    }
  }
```

* Run the terraform init command to initialize the working directory and download the required providers.
    

![](https://miro.medium.com/v2/resize:fit:875/0*YY0-tzYc0QB3agS5 align="left")

* After that, run `terraform apply` to create the VPC in your AWS account.
    

![](https://miro.medium.com/v2/resize:fit:875/0*2OFBhnOLFQ7v9hTC align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*sPYP46ztkb8GdM_T align="left")

* Check whether the vpc is created in the AWS VPC.
    

![](https://miro.medium.com/v2/resize:fit:875/0*wDAIcKKpk5awVyJv align="left")

# **Step 2: Create a public subnet**

* Now create a public subnet named as [`subnet.tf`](http://subnet.tf) with CIDR block 10.0.1.0/24 in the VPC with ID aws\_[vpc.main.id](http://vpc.main.id/), and tags it with the name "public", you can take reference of vpc resource that has been created before.
    

```plaintext
  resource "aws_subnet" "public" {
    vpc_id     = aws_vpc.main.id
    cidr_block = "10.0.16.0/20"
    availability_zone = "us-east-1a"
    tags = {
      Name = "public"
    }
  }
```

* Run `terraform apply` to create a public subnet in your AWS account.
    

![](https://miro.medium.com/v2/resize:fit:875/0*M7cK_81VVvsY5chN align="left")

* Go to VPC console then go to Subnets. Check Public Subnet is created successfully.
    

![](https://miro.medium.com/v2/resize:fit:875/0*gfAmFy3nfKjpEucG align="left")

# **Step 3: Create a private subnet**

* Same as the public subnet, creates a private subnet with CIDR block 10.0.2.0/24 in the VPC with ID aws\_[vpc.main.id](http://vpc.main.id/), and tags it with the name “private”.
    

```plaintext
  resource "aws_subnet" "private" {
    vpc_id     = aws_vpc.main.id
    cidr_block = "10.0.32.0/20"
    availability_zone = "us-east-1a"
    tags = {
      Name = "private"
    }
  }
```

* Now execute the `terraform apply` the command to create a private subnet.
    

![](https://miro.medium.com/v2/resize:fit:875/0*VPLA3USrFcv4V4o9 align="left")

* A private Subnet is successfully created using Terraform, you can verify this in the VPC Tab of the Subnet console.
    

![](https://miro.medium.com/v2/resize:fit:875/0*sT83LFCFntIe4emi align="left")

# **Step 4: Create an Internet Gateway (IGW) and attach it to the VPC.**

* Create a [`internetgateway.tf`](http://internetgateway.tf) file write the following code which will creates an internet gateway in the VPC with ID aws\_[vpc.main.id](http://vpc.main.id/), and tags it with the name "igw".
    

```plaintext
  resource "aws_internet_gateway" "gw" {
    vpc_id = aws_vpc.main.id
    tags = {
      Name = "internet-getway"
    }
  }
```

* Execute the terraform apply command for the creation of Internet Gateway.
    

![](https://miro.medium.com/v2/resize:fit:875/0*P7Kn5K6CY-r7oI7K align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*oNf-ZGx4mWucCpgw align="left")

* Go to VPC then go to Internet gateways, and check whether a new Internet gateway is created with the name ‘internet-getway’.
    

![](https://miro.medium.com/v2/resize:fit:875/0*Buf_oDM13YNdrohQ align="left")

* VPC is attached to the internet gateway.
    

# **Step 5: Create a Route Table**

* Now create a route table named [`routetable.tf`](http://routetable.tf) for use with a public subnet specified by the subnet\_id attribute.
    

```plaintext
  resource "aws_route_table" "public" {
    vpc_id = aws_vpc.main.id

     route {
      cidr_block = "0.0.0.0/0"
      gateway_id = aws_internet_gateway.gw.id
    }
     tags = {
      Name = "public"
    }
  }

  resource "aws_route_table_association" "public_subnet_association" {
    subnet_id      = aws_subnet.public.id
    route_table_id = aws_route_table.public.id
  }
```

* In Route tables, a new route table is successfully created using `terraform apply`
    
* command, Now route table routes with an internet gateway.
    

![](https://miro.medium.com/v2/resize:fit:875/0*JT5TpU9Hf4zriwb9 align="left")

* The route table is associated with a public subnet using Terraform.
    

![](https://miro.medium.com/v2/resize:fit:875/0*8LnVTsVbJpxsVDHI align="left")

# **Step 6: Create a Security Group**

* To connect our EC2 instance, create a [`securitygroup.tf`](http://securitygroup.tf) file where use the aws\_security\_group block creates a new security group that allows inbound traffic on ports 22 (SSH) and 80 (HTTP) from any source (0.0.0.0/0).
    

```plaintext
resource "aws_security_group" "web_server" {
  name_prefix = "web-server-sg"
  vpc_id      =  aws_vpc.main.id


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

![](https://miro.medium.com/v2/resize:fit:875/0*V3lWI7nxXgGCsvuq align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*GGBLjMSrK5_he9z1 align="left")

* A security group is created with SSH(Port 22) and HTTP(Port 80) and HTTPS(Port 443) access.
    

![](https://miro.medium.com/v2/resize:fit:875/0*3Jpw5A18J0JY9cYv align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*1ADx1yhEKCGZyOiX align="left")

# **Step 7: Create an Elastic IP and associate it with the EC2 instance.**

* Create a file named [`elasticip.tf`](http://elasticip.tf) where the aws\_eip block creates a new Elastic IP address and associates it with the instance created in the first block by specifying the instance ID in the instance attribute.
    

```plaintext
  resource "aws_eip" "eip" {
    instance = aws_instance.web_server.id

    tags = {
      Name = "test-eip"
    }
  }
```

* Elastic IP is successfully created using `terraform apply` command.
    

![](https://miro.medium.com/v2/resize:fit:875/0*XyIBu_vfgKJ14ypj align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*dD-jziZ2vHoL8KNm align="left")

* Now we can check that our Elastic IP has been created.
    

![](https://miro.medium.com/v2/resize:fit:875/0*s1fGs6IWNYYyyTDY align="left")

# **Step 8: Create User data to install Apache**

* The user\_data attribute specifies the script to run when the instance is launched. This script updates the package manager, installs the Apache web server, creates a basic HTML file, and restarts Apache.
    

```plaintext
   user_data = <<-EOF
    #!/bin/bash
    sudo apt-get update -y
    sudo apt-get install apache2 -y
    sudo systemctl start apache2
    sudo systemctl enable apache2
    sudo systemctl restart apache2
    sudo chmod 766 /var/www/html/index.html
    sudo echo "<html><body><h1>Welcome to my website.</h1></body></html>" >/var/www/html/index.html    
   EOF
```

# **Step 9: Launch an EC2 instance in the public subnet**

* Create a new [ec2.tf](http://ec2.tf) file where add the details of our EC2 instance like AMI ID, instance type, key name, public subnet, security group and User Data to install Apache in our EC2 instance server.
    

```plaintext
  resource "aws_instance" "example" {
    ami           = "ami-053b0d53c279acc90"
    instance_type = "t2.micro"
    key_name      = "Terraform-Key"
    subnet_id     = aws_subnet.public.id

    associate_public_ip_address = true
    security_groups = [
      aws_security_group.web_server.id
    ]
     user_data = <<-EOF
       #!/bin/bash
       sudo apt-get update -y
       sudo apt-get install apache2 -y
       sudo systemctl start apache2
       sudo systemctl enable apache2
       sudo systemctl restart apache2
       sudo chmod 766 /var/www/html/index.html
       sudo echo "<html><body><h1>Welcome to my website.</h1></body></html>" >/var/www/html/index.html    
    EOF
    tags = {
      Name = "Terraform-Infra"
    }
  }
```

* Run `terraform apply` to create an EC2 instance in your AWS account named "Terraform-Infra".
    

![](https://miro.medium.com/v2/resize:fit:875/0*F53RdJO3Uzh7dxyZ align="left")

* A New instance is created (Terraform-Infra) using Terraform.
    

![](https://miro.medium.com/v2/resize:fit:875/0*ScAhow09H6b--e2g align="left")

* Using the Public IPv4 address, open the URL in a browser to verify that the website is hosted successfully.
    

![](https://miro.medium.com/v2/resize:fit:875/1*zwd79vf7akpnYBc0Fz7Juw.jpeg align="left")

In this blog post, we’ve laid out a structured project file for building a robust AWS environment. We’ve covered nine essential steps, from creating a Virtual Private Cloud (VPC) to launching an EC2 instance in a public subnet. Each step is a building block towards creating a secure and scalable cloud infrastructure.

We believe in continuous improvement, so if you come across any mistakes or have suggestions for enhancements, we’re open to your feedback. Your insights are invaluable in helping us refine our content and provide even more value to our readers.

If you have any questions or require further guidance, don’t hesitate to reach out. You can connect with me on LinkedIn at [https://www.linkedin.com/in/mudit--mathur/](https://www.linkedin.com/in/mudit--mathur/) [](https://www.linkedin.com/in/mudit--mathur/](https://www.linkedin.com/in/mudit--mathur/).). Your feedback and connections are highly appreciated as we continue our cloud journey together. Thank you for being a part of this community!