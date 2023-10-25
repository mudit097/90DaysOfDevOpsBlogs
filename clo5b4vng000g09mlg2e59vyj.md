---
title: "AWS S3 Bucket Creation and Management"
datePublished: Wed Oct 25 2023 05:20:56 GMT+0000 (Coordinated Universal Time)
cuid: clo5b4vng000g09mlg2e59vyj
slug: aws-s3-bucket-creation-and-management
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1698211198893/82276d23-ec17-48b4-b8d3-a480e65d109c.png
tags: aws, devops, terraform, 90daysofdevops, trainwithshubham

---

In this blog, we dive into the world of AWS S3 buckets, uncovering essential steps to harness their power and flexibility. From creating an S3 bucket using Terraform to configuring public read access, crafting fine-tuned policies for IAM users, and enabling versioning, we’ll guide you through every crucial detail you need to know. Whether you’re a cloud novice or a seasoned pro, this comprehensive guide will equip you with the knowledge to leverage AWS S3 buckets effectively.

# **AWS S3 Bucket**

AWS S3 (Simple Storage Service) Bucket is a scalable and durable object storage service. It allows you to store and retrieve any amount of data from anywhere on the web. S3 provides high availability, security, and flexibility, making it suitable for storing files, hosting static websites, and enabling data backup and archival solutions in the AWS cloud.

![](https://miro.medium.com/v2/resize:fit:875/0*o13G2qKCjXlwRuD_ align="left")

# **Step 1: Create an S3 bucket using Terraform.**

* Create a [`terraform.tf`](http://terraform.tf) and [`provider.tf`](http://provider.tf) to add details regarding AWS configuration and AWS Region.
    

```plaintext
# terraform.tf

terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.0"
    }
  }
}

# provider.tf

provider "aws" {
  region = "us-east-1"
}
```

* Create a [`s3.tf`](http://s3.tf) file and inside aws\_s3\_bucket resource creates a new S3 bucket, my\_bucket is a unique identifier.
    

```plaintext
  resource "aws_s3_bucket" "my_bucket" {
    bucket = "task1-day67-devops"
  }
```

* Run the terraform init command to initialize the working directory and download the required providers.
    

![](https://miro.medium.com/v2/resize:fit:875/0*Qzl2cxuw5uUXN1OJ align="left")

* Execute terraform plan, it will create an execution plan by analyzing the changes required to achieve the desired state of your infrastructure.
    

![](https://miro.medium.com/v2/resize:fit:875/0*s16CCs7rdhYMfejm align="left")

* Finally, execute terraform apply, it will apply the changes to create or update resources as needed.
    

![](https://miro.medium.com/v2/resize:fit:875/0*Vdj1-H-KigZRHY7f align="left")

* S3 bucket successfully created.
    

![](https://miro.medium.com/v2/resize:fit:875/0*-OZTs8JdF3d0n_Ns align="left")

# **Step 2: Configure the bucket to allow public read access.**

* As the S3 bucket is created which is Private only, to allow public read access to the S3 bucket, the code creates an ACL (access control list) resource using the “aws\_s3\_bucket\_acl” resource type.
    
* Now create a file [`access.tf`](http://access.tf)`,`the resource is associated with the S3 bucket resource "aws\_s3\_bucket.my\_bucket" using the "bucket" parameter. The "acl" parameter is set to "public-read", which allows public read access to the bucket.
    

```plaintext
  resource "aws_s3_bucket_acl" "bucket_acl" {
    bucket = aws_s3_bucket.my_bucket.id
    acl    = "public-read"
  }

  resource "aws_s3_bucket_public_access_block" "pem_access" {
    bucket = aws_s3_bucket.my_bucket.id

    block_public_acls       = false
    block_public_policy     = false
    ignore_public_acls      = false
    restrict_public_buckets = false
  }
```

* Now change the object Ownership by enabling “ACL enable” in the S3 Bucket “Edit Object Ownership”.
    

![](https://miro.medium.com/v2/resize:fit:875/0*92urJ0A4x9sEmfPR align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*XfdBX_xnK4gNVnI5 align="left")

* Run terraform apply
    

![](https://miro.medium.com/v2/resize:fit:875/0*tm14qhYIziLN-1kZ align="left")

* Now the S3 Bucket is publicly accessible.
    

![](https://miro.medium.com/v2/resize:fit:875/0*WmISAOiZseCTEPet align="left")

# **Step 3: Create an S3 bucket policy that allows read-only access to a specific IAM user or role.**

* To provide read-only access to a specific IAM user or role, the code creates an S3 bucket policy resource using the “aws\_s3\_bucket\_policy” resource type. The resource is associated with the S3 bucket resource “aws\_s3\_bucket.my\_bucket” using the “bucket” parameter.
    
* Create a file [`iam.tf`](http://iam.tf) and inside "aws\_iam\_policy\_document" provide the details of the IAM user ARN. Inside the action provide the details like "s3:GetObject" and "s3:ListBucket". And in the resources add the bucket details including the IAM User arn.
    

```plaintext
resource "aws_s3_bucket_policy" "bucket_policy" {
  bucket = aws_s3_bucket.my_bucket.id
  policy = data.aws_iam_policy_document.allow_read_only_access.json
}


data "aws_iam_policy_document" "allow_read_only_access" {
  statement {
    principals {
      type        = "AWS"
      identifiers = ["arn:aws:iam::563024908183:user/Doraemon"]
    }

    actions = [
      "s3:GetObject",
      "s3:ListBucket",
    ]

    resources = [
      aws_s3_bucket.my_bucket.arn,
      "${aws_s3_bucket.my_bucket.arn}/*",
    ]
  }
}
```

* Run terraform apply
    

![](https://miro.medium.com/v2/resize:fit:875/0*wTWUe7VMgQLRWymy align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*t-aMAb5U-gtsVpvU align="left")

* S3 bucket policy is created that allows read-only access to a specific IAM user.
    

![](https://miro.medium.com/v2/resize:fit:875/0*rXttTFUlWx0DK7-1 align="left")

# **Step 4: Enable versioning on the S3 bucket.**

* S3 bucket versioning is a feature in AWS S3 that enables the preservation and tracking of multiple versions of an object. It provides an added layer of data protection, allowing you to recover and restore previous versions of objects stored in an S3 bucket.
    
* In the [`s3.tf`](http://s3.tf) file adds the versioning block is included, with enabled set to true.
    

```plaintext
  resource "aws_s3_bucket" "my_bucket" {
    bucket = "task1_day67_devops"
    versioning {
      enabled = true
    }
  }
```

* Now use the command `terraform apply` and makes the bucket versioning enabled.
    

![](https://miro.medium.com/v2/resize:fit:875/0*7kRv9ISWsUooWjAA align="left")

* Now we can verify in the S3 Bucket that Bucket Versioning has been enabled.
    

![](https://miro.medium.com/v2/resize:fit:875/0*i2S6GoOCZCBIBkCn align="left")

In this guide, we’ve walked through the steps to create and configure an AWS S3 bucket using Terraform. By following these steps, you can set up an S3 bucket, grant public read access, and establish a bucket policy for controlled access to a specific IAM user or role. Enabling versioning on your S3 bucket ensures data integrity and management.

We hope you found this tutorial helpful in harnessing the power of AWS S3 for your storage needs. If you have any questions, suggestions, or feedback, please feel free to reach out. I’m always open to connecting with fellow tech enthusiasts and professionals on LinkedIn. Don’t hesitate to connect with me on **\[LinkedIn\]** ([https://www.linkedin.com/in/mudit--mathur/](https://www.linkedin.com/in/mudit--mathur/)) and share your thoughts.