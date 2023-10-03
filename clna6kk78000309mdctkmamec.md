---
title: "S3 Programmatic access with AWS-CLI"
datePublished: Tue Oct 03 2023 10:32:18 GMT+0000 (Coordinated Universal Time)
cuid: clna6kk78000309mdctkmamec
slug: s3-programmatic-access-with-aws-cli
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696329029222/f33ed520-496e-466c-bc33-a833728ea8b1.png
tags: blogging, aws, devops, 90daysofdevops, trainwithshubham

---

In the previous blog, I discussed IAM Programmatic access with AWS CLI. In this blog, I will explain S3, and how to access it with AWS CLI.

# **S3**

Amazon S3 (Simple Storage Service) is a scalable object storage service that Amazon Web Services (AWS) provides.

It allows you to store and retrieve large amounts of data in a secure and highly available manner.

S3 is commonly used for various purposes, including backup and restore, data archiving, content distribution, and hosting static websites.

Here’s the link to the official documentation of [S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html#S3Features).

# **Features of Amazon S3**

Below are a few features of Amazon S3:

# **Storage classes**

S3 offers different storage classes to optimize cost and performance based on your data access patterns. The available classes include Standard, Intelligent-Tiering, Standard-IA (Infrequent Access), One Zone-IA, Glacier, and Glacier Deep Archive.

# **Storage management**

Amazon S3 has storage management features that you can use to manage costs, meet regulatory requirements, reduce latency, and save multiple distinct copies of your data for compliance requirements.

* Lifecycle management — You can use lifecycle management to automatically move your data to different storage classes as it ages. This can help you save money on storage costs.
    
* Object lock — You can use object lock to prevent your data from being deleted or overwritten for a specified period. This can help you meet regulatory requirements.
    
* Access control — You can use access control to control who can access your data. This can help you protect your data from unauthorized access.
    
* Replication — You can replicate your data to multiple regions to improve availability and reduce latency.
    
* Data backup — You can use Amazon S3 to back up your data to the cloud. This can help you protect your data from data loss.
    

# **Access management and security**

S3 offers various mechanisms to control access to your buckets and objects. Access Control Lists (ACLs) and Bucket Policies can define granular permissions for different users and applications.

By default, S3 buckets and the objects in them are private.

# **Data Processing**

To transform data and trigger workflows to automate a variety of other processing activities at scale, you can use the features like S3 Object Lambda and Event Notifications.

# **Storage logging and monitoring**

Amazon S3 provides logging and monitoring tools that you can use to monitor and control how your Amazon S3 resources are being used.

# **Analytics and insights**

Amazon S3 offers features to help you gain visibility into your storage usage, which empowers you to better understand, analyze, and optimize your storage at scale.

# **Strong consistency**

Amazon S3 provides strong read-after-write consistency for PUT and DELETE requests of objects in your Amazon S3 bucket in all AWS Regions.

# **Concepts in S3**

[Buckets](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html#BasicsBucket): S3 organizes data into containers called buckets. Each bucket has a globally unique name and serves as a logical container for objects.

[Objects](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html#BasicsObjects): Objects are the fundamental entities stored in S3. They consist of the data you want to store and associated metadata.

[Keys](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html#BasicsKeys): Keys are unique identifiers for objects within a bucket. They represent the object’s path and can include prefixes and subdirectories to organize objects within a bucket.

[S3 Versioning](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html#Versions): S3 supports versioning, which enables you to store multiple versions of an object. This feature helps in tracking changes and recovering from accidental deletions or modifications.

[Version ID](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html#BasicsVersionID): In Amazon S3, when versioning is enabled for a bucket, each object can have multiple versions. Each version of an object is assigned a unique identifier called a Version ID. The Version ID is a string that uniquely identifies a specific version of an object within a bucket.

[Bucket policy](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html#BucketPolicies): A bucket policy in Amazon S3 is a set of rules that define the permissions and access controls for a specific S3 bucket. It allows you to manage access to your S3 bucket at a more granular level than the permissions granted by IAM (Identity and Access Management) policies.

[S3 Access Points](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html#BasicsAccessPoints): S3 Access Points in Amazon S3 provide a way to easily manage access to your S3 buckets. Access points act as unique hostnames and entry points for applications to interact with specific buckets or prefixes within a bucket. Here are some key points about S3 Access Points:

[Access control lists (ACLs)](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html#S3_ACLs): ACLs (Access Control Lists) in Amazon S3 are a legacy method of managing access control for objects within S3 buckets. While bucket policies and IAM policies are the recommended methods for access control in S3, ACLs can still be used for fine-grained control in specific scenarios.

[Regions](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html#Regions): S3 is available in different geographic regions worldwide. When you create a bucket, you select the region where it will be stored. Each region operates independently and provides data durability and low latency within its region.

> *You can access Amazon S3 and its features only in the AWS Regions that are enabled for your account.*

# **How Amazon S3 works?**

1. You create a bucket. A bucket is like a folder that holds your data.
    
2. You upload your data to the bucket. You can upload files of any size, and you can even upload folders and subfolders.
    
3. You can access your data from anywhere. You can use the Amazon S3 website, the AWS Command-Line Interface (CLI), or any other application that supports Amazon S3.
    

# **Tasks**

# **Task 1: Launch an EC2 instance using the AWS Management Console and connect to it using Secure Shell (SSH). Create an S3 bucket and upload a file to it using the AWS Management Console. Access the file from the EC2 instance using the AWS Command Line Interface (AWS CLI).**

*Launch an EC2 instance using the AWS Management Console and connect to it using Secure Shell (SSH).*

![](https://miro.medium.com/v2/resize:fit:875/1*4vzl8yJrz-XBw8dx_M72oQ.png align="left")

Connect to it using SSH:

![](https://miro.medium.com/v2/resize:fit:875/1*4bo9w8zNItgRi3-1DUHN3w.png align="left")

*Create an S3 bucket and upload a file to it using the AWS Management Console.*

Search S3 in the AWS Management Console.

> *Click on Create Bucket.*
> 
> *Bucket name: s3awsbucket.01*

![](https://miro.medium.com/v2/resize:fit:875/1*mW-cRO6BxRzzbro-EMInPQ.png align="left")

*Let the other options be the default and click on Create.*

![](https://miro.medium.com/v2/resize:fit:875/1*nFCVuO2fCyXvHXdZLYuyXw.png align="left")

Let us upload a file to the bucket we created just now.

Click Open the bucket you just created. And in the objects section click on Upload.

![](https://miro.medium.com/v2/resize:fit:875/1*ZxZNDZcUfCOqN3WSdGC2yg.png align="left")

Click on Add Files and select the file you want to upload.

![](https://miro.medium.com/v2/resize:fit:875/1*X8_Rc4rMNSJwaeWVtQitAg.png align="left")

And click on Upload.

![](https://miro.medium.com/v2/resize:fit:875/1*xnVd6A7CFYZg5FYIQiVuxg.png align="left")

You can see that the File upload was successful.

*Access the file from the EC2 instance using the AWS Command Line Interface (AWS CLI).*

Here’s the link to [install AWS CLI and configure the CLI with credentials.](https://muditm12.hashnode.dev/iam-programmatic-access-and-aws-cli)

To check the S3 buckets present:

```plaintext
aws s3 ls
```

![](https://miro.medium.com/v2/resize:fit:875/1*Xf9epcogSykUWqQHjXafYQ.png align="left")

Let’s create a file in the instance and upload it to the S3 using CLI.

```plaintext
echo "This is for testing purposes" > sample2.txt
ls
cat sample2.txt
aws s3 cp sample2.txt s3://s3awsbucket.01
```

![](https://miro.medium.com/v2/resize:fit:875/1*zJjOuMWMKVjcokSXqSIRhA.png align="left")

This can be verified in the AWS Console:

![](https://miro.medium.com/v2/resize:fit:875/1*gGokRxGIohzWRpkr9YJCVw.png align="left")

Let’s download a file from the console to your local using CLI:

```plaintext
aws s3 cp s3://s3awsbucket.01/sample3.txt .
ls
```

![](https://miro.medium.com/v2/resize:fit:875/1*y1QgIk8EnhrK07N7GrG9zQ.png align="left")

Let us sync the contents of the local folder with our bucket.

```plaintext
touch file{1..10}.txt
ls 
#aws s3 sync <local-folder> s3://bucket-name
aws s3 sync . s3://s3awsbucket.01
```

![](https://miro.medium.com/v2/resize:fit:875/0*BlA9d5bPBgLj5yGH align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*7_s3oNWsuoqhCLuS align="left")

This sync can be verified in the console:

![](https://miro.medium.com/v2/resize:fit:875/1*uJwxn5a8Mo6LH1w0Ai0awg.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*tMv2Nrhvz3Ib82RMNTnQZg.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*mqypmg2-ijK2aeZGXKLxyQ.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*7_Mr5i3yhlV7OmZF9Z_4jQ.png align="left")

To list the objects in an S3 bucket:

```plaintext
aws s3 ls s3://bucket-name
```

![](https://miro.medium.com/v2/resize:fit:875/1*OLSpaeeKE7vyFb6upkvwUw.png align="left")

To delete an object from an S3 bucket:

```plaintext
aws s3 rm s3://bucket-name/file.txt
aws s3 ls s3://s3awsbucket.01
```

![](https://miro.medium.com/v2/resize:fit:875/1*c169WX8C_UIP6fDVX4sSsA.png align="left")

To create a new bucket:

```plaintext
aws s3 mb s3://bucket-name
aws s3 ls
```

![](https://miro.medium.com/v2/resize:fit:875/1*iT3oBNnZMpYifBAw5brRXg.png align="left")

To delete a bucket from S3:

```plaintext
aws s3 rb s3://bucket-name
```

![](https://miro.medium.com/v2/resize:fit:875/1*I5rV48y5ZhXwJA6QeV0PXg.png align="left")

# **Task 2: Create a snapshot of the EC2 instance and use it to launch a new EC2 instance. Download a file from the S3 bucket using the AWS CLI. Verify that the contents of the file are the same on both EC2 instances.**

*Create a snapshot of the EC2 instance and use it to launch a new EC2 instance.*

> *In Amazon EC2, you can create a snapshot of an EBS (Elastic Block Store) volume to create a point-in-time copy of the data stored on the volume. This snapshot can be used to back up data, migrate volumes between regions, or create new volumes from the snapshot.*

Search EC2 in the console &gt; Scroll down to EBS (Elastic Block Store) &gt; Select Snapshots.

![](https://miro.medium.com/v2/resize:fit:875/1*pslRt8C6iDv-ACJetBzn0Q.png align="left")

Click on Create Snapshot &gt; Select Instance &gt; Select the Instance ID &gt; Click on Create Snapshot

![](https://miro.medium.com/v2/resize:fit:875/1*y_A644F0z5FF9XtVbQ-Vzg.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*KHpU_bHKR_vgsnw2mWiV-Q.png align="left")

Let us use this Snapshot to launch a new EC2 instance.

Select the Snapshot &gt; Click on Actions &gt; Select Create image from the snapshot.

![](https://miro.medium.com/v2/resize:fit:875/1*eUlYRjX7b957IK4WEK5lww.png align="left")

*Image Name: s3-image*

*Description: image from snapshot*

![](https://miro.medium.com/v2/resize:fit:875/1*BapnPvMbHqQr76nlHRhwQw.png align="left")

*Click on Create Image. In the AMI section, you can observe that the AMI is created:*

![](https://miro.medium.com/v2/resize:fit:875/1*Zl18roiIuQfwn9nTi5w19w.png align="left")

*Select the Instance &gt; Actions &gt; Click on Launch Instance from AMI*

![](https://miro.medium.com/v2/resize:fit:875/1*pBzH6HqBuWaS0B2CmfQl4g.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*0bR6Nk-PnUJTHh2F align="left")

And that’s how we can access and modify S3 and its contents through CLI.

In this blog, I have discussed S3 programmatic access with AWS CLI. If you have any questions or want to share your experiences, please comment below. Don’t forget to read my blogs and connect with me on LinkedIn and let’s have a conversation.

To help me improve my blog and correct my mistakes, I am available on LinkedIn as [Mudit Mathur.](https://www.linkedin.com/in/mudit--mathur/) Do reach me and I am open to suggestions and corrections.

#Day43 #90daysofdevops