---
title: "AWS and IAM Basics"
datePublished: Sun Oct 01 2023 19:54:36 GMT+0000 (Coordinated Universal Time)
cuid: cln7vrz3g00010amp46fy4o6f
slug: aws-and-iam-basics
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696189838087/ba77ea2d-4573-4986-a319-6423979a96fa.jpeg
tags: blogging, aws, devops, 90daysofdevops, trainwithshubham

---

# **User Data in AWS**

In the previous blog, [Getting Started with AWS Basics](https://muditm12.hashnode.dev/getting-started-with-aws-basics-aws) [](https://muditm12.hashnode.dev/getting-started-with-aws-basics-aws)I explained AWS, its global infrastructure, and services offered by AWS that are useful for a DevOps engineer. In this blog let’s switch to a bit of automation part. I had taken a break of almost ten days owing to my mental health. Let’s continue.

# **User Data in AWS**

When you create an instance, in Amazon EC2 (Elastic Compute Cloud), you can provide some extra information to the instance. This additional information is known as “user data,” and it helps you automate certain setup tasks or run scripts on the instance after it starts.

User data can be passed to Amazon EC2 in two formats: shell scripts and cloud-init directives.

Shell scripts: Shell scripts are a series of commands or instructions that can be executed by the instance’s operating system.

Cloud-init directives: Cloud-init is a widely used system for configuring instances in the cloud. It supports a broader range of configuration options compared to shell scripts. With cloud-init, you can provide a set of directives that specify how the instance should be configured.

> *Why User Data? By passing user data to Amazon EC2 instances, you can automate the initial setup and configuration processes, saving time and effort.*

You can also pass this data into the launch instance wizard as plain text, as a file (this is useful for launching instances using the command line tools), or as base64-encoded text (for API calls).

# **IAM**

AWS Identity and Access Management (IAM) is a web service that helps you securely control access to AWS resources. With IAM, you can centrally manage permissions that control which AWS resources users can access.

Let’s discuss IAM Roles, IAM Users, and Groups.

# **IAM Users**

IAM Users are identity within your IAM account. IAM users have specific permission for a single application or person.

> *When to use IAM User? An IAM user is created if there is any specific use case that requires long-term credentials.*

IAM users have their own set of credentials (username and password or access keys) that they use to authenticate themselves when accessing AWS services.

Each user has a unique set of credentials and can have specific permissions assigned to them.

# **IAM Groups**

IAM Groups are a collection of IAM users. You can’t sign in as a Group. IAM Groups are used to specify permissions for multiple users at a time. IAM Groups make it easier to manage permissions for a large set of users.

# **IAM Roles**

IAM Roles are identity within an AWS account that has specific permissions. IAM roles are used to grant permissions to entities or services within AWS, rather than to individual users.

IAM roles are designed to provide temporary security credentials to AWS services, applications, or other entities, enabling them to access AWS resources securely. Roles are typically used for applications running on AWS services, such as EC2 instances, Lambda functions, or ECS tasks.

> *When to use IAM Roles? IAM Roles are used when you need to temporarily access a service.*

IAM Roles promote the principle of least privilege by allowing you to assign specific and temporary permissions to entities as needed, reducing the risk of unauthorized access.

# **Difference between IAM Users and IAM Roles**

## **IAM Users:**

\- Purpose: IAM Users are designed to represent individual people or entities.  
\- Usage: They are typically used for interactive access to AWS resources.  
\- Authentication: IAM Users use long-term credentials, such as username/password or access keys, for authentication.  
\- Permission: Permissions are assigned directly to the user.  
\- Trust Relationship: There is no concept of a trust relationship for IAM Users.  
\- Credential Rotation: IAM Users may have long-term credentials that need to be manually rotated periodically.  
\- Auditing and Compliance: IAM Users have separate audit trails and activity tracking.

## **IAM Roles:**

\- Purpose: IAM Roles are used to grant permissions to AWS services or non-human entities.  
\- Usage: They are commonly used to provide access for applications running on AWS services.  
\- Authentication: IAM Roles provide temporary credentials for entities assuming the role.  
\- Permission: Permissions are attached to the role and are assumed by entities.  
\- Trust Relationship: IAM Roles define trust relationships that specify which entities are allowed to assume the role.  
\- Credential Rotation: IAM Roles provide temporary credentials that are automatically rotated by AWS.  
\- Auditing and Compliance: Actions performed by entities assuming a role are logged under the role’s activity.

In the previous blog, we performed a task on IAM too. Let’s get started with the tasks and learn further.

# **Tasks**

## **Task 1: Launch the EC2 instance with already installed Jenkins on it. Once the server shows up in the console, hit the IP address in the browser and your Jenkins page should be visible.**

> *Take a screenshot of the Userdata and Jenkins page, this will verify the task completion.*

In the AWS Management console &gt; Search EC2 &gt; Click on Launch an Instance.

Given the below details for the creation of instance:

> *Name of the instance: userdata\_server*
> 
> *Application and OS Images (Amazon Machine Image): Ubuntu*
> 
> *Instance Type: t2.micro*
> 
> *Key Pair: Select the key pair you have generated or create a new key pair.*
> 
> *Network settings: Check the boxes for “Allow HTTPS traffic from the Internet” and “Allow HTTP traffic from the Internet”*
> 
> *Now expand the Advanced Details tab.*

Scroll down to User Data — optional box.

![](https://miro.medium.com/v2/resize:fit:875/1*8kzKe1Qr98aaOt8XZXnafw.png align="left")

In the box, enter the script that we need to be executed.

```plaintext
#!/bin/bash
sudo apt-get update -y
sudo apt install openjdk-11-jre -y
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins -y
sudo systemctl enable jenkins
sudo systemctl start jenkins
```

![](https://miro.medium.com/v2/resize:fit:875/1*u67-dScjyC-f1cE2RrqGow.png align="left")

And click on Launch Instance. Make sure you open port 8080 to the instance.

![](https://miro.medium.com/v2/resize:fit:875/1*ar7stxiv2wmpDcopzRbe9w.png align="left")

Now copy the Public IP of instance and the port you just opened.

In the browser open the Jenkins UI using the following format:

> [*PublicIP:8080*](https://publicip:8080/)

We will get the Jenkins page if the script we passed as User Data was executed successfully.

![](https://miro.medium.com/v2/resize:fit:875/1*u1Z0ZoDwXMYQEvxhzBI9ng.png align="left")

And hence, we complete the task.

# **Task 2: Create three Roles named: DevOps-User, Test-User, and Admin.**

Go to AWS Management Console &gt; IAM &gt; Roles.

> *You can find roles on the left side of your screen under the Access Management tab.*

![](https://miro.medium.com/v2/resize:fit:875/1*hELddbnY7CQCGLzqbjgG9Q.png align="left")

Click on Create Roles.

Step 1: Select trusted entity

![](https://miro.medium.com/v2/resize:fit:875/1*S35VH-HwQzVqlnpCiyBVpA.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*JpcZge6gsDkZo1CZyh5axw.png align="left")

Select AWS Service. Common Use Cases as EC2. Click on Next.

Step 2: Add permissions

I am giving full access to EC2 creation and management.

![](https://miro.medium.com/v2/resize:fit:875/1*Ls24fMq94FH3YVfnpjJ6Bw.png align="left")

Click on Next.

Step 3: Name, review, and create

I am creating the user Devops-user.

![](https://miro.medium.com/v2/resize:fit:875/1*U1outit5iJJekn8vTgwz6A.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*5AbjXZBuc9vTCm0s6I_bvQ.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*3e7DwFLJfWS1PfVNjVhmeA.png align="left")

Click on Create Role.

Similarly, create the roles Test-User and Admin.

![](https://miro.medium.com/v2/resize:fit:875/1*C3l6shuqGvEh3KMubm3lww.png align="left")

Yay! We created IAM roles.

**While creating IAM roles, we need to select the trusted entity. Here is a brief description of the trusted entity:**

* **AWS service: Allows an AWS service to assume the role.**
    
* **Another AWS account: Allows another AWS account to assume the role.**
    
* **Web identity: Allows web-based identity providers (such as Amazon Cognito, Google, or Facebook) to assume the role.**
    
* **SAML 2.0 federation: Allows an external identity provider that supports SAML 2.0 to assume the role.**
    
* **IAM user: Allows an IAM user within your AWS account to assume the role.**
    

It’s a new day in learning. In this blog, I have discussed how to automate EC2 instance creation using User Data and more about IAM. If you have any questions or would like to share your experiences, please leave a comment below. Don’t forget to read my blogs and connect with me on LinkedIn and let’s have a conversation.

To help me improve my blog and correct my mistakes, I am available on LinkedIn as [Mudit Mathur.](https://www.linkedin.com/in/mudit--mathur/) Do reach me and I am open to suggestions and corrections.

#Day39 #90daysofdevops