---
title: "IAM Programmatic access and AWS CLI"
datePublished: Mon Oct 02 2023 22:49:01 GMT+0000 (Coordinated Universal Time)
cuid: cln9hg4ms000008mjbp4sejyi
slug: iam-programmatic-access-and-aws-cli
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696286856806/c2869520-4722-4a93-ada7-17eb696a7192.png
tags: blogging, aws, devops, 90daysofdevops, trainwithshubham

---

# **IAM Programmatic access**

IAM programmatic access refers to enabling access to AWS services and resources through APIs and command-line tools using access keys.

When you enable programmatic access for an IAM user, you generate access keys (access key ID and secret access key) that can be used to authenticate and authorize API requests.

Here’s how you can enable IAM programmatic access and obtain access keys:

1. Open the IAM console: Sign in to the AWS Management Console, open the IAM service, and navigate to the “Users” section.
    
2. Create a new IAM user or select an existing user: Click on “Add user” or choose an existing user from the list.
    
3. Set the access type: In the “Set permissions” step, select the desired permissions for the user. You can choose to assign policies directly or add the user to IAM groups with preconfigured policies.
    
4. Configure the user details: Provide a user name and select the “Programmatic access” checkbox to enable programmatic access for the user.
    
5. Set permissions boundaries and tags (optional): You can set additional permissions boundaries or add tags to the user if required.
    
6. Review and create the user: Review the user details and click on “Create user” to create the IAM user.
    
7. Access key creation: After creating the user, you will be presented with the option to download the access keys. Click on “Download .csv” to obtain a CSV file containing the access key ID and secret access key. Make sure to securely store this file, as the secret access key will not be accessible again.
    

# **AWS CLI**

The AWS Command Line Interface (AWS CLI) is a unified tool to manage your AWS services. With just one tool to download and configure, you can control multiple AWS services from the command line and automate them through scripts.

Here’s the link to the documentation of the latest version of [AWS CLI](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/index.html).

To use the AWS CLI:

* You need to have it installed on your local machine.
    
* Once the AWS CLI is installed, you need to configure it with your AWS credentials.
    
* The configuration will be stored in a file named `~/.aws/credentials` on Linux and macOS or `%USERPROFILE%\.aws\credentials` on Windows.
    

Some common AWS CLI commands used are aws s3 &lt;cmd&gt;, aws ec2 &lt;cmd&gt;, aws rds &lt;cmd&gt;, and aws iam &lt;cmd&gt;.

Here’s the link to [AWS CLI Command Reference](https://awscli.amazonaws.com/v2/documentation/api/latest/index.html).

# **Tasks**

# **Task 1: Create AWS\_ACCESS\_KEY\_ID and AWS\_SECRET\_ACCESS\_KEY from AWS Console.**

On the right top corner, Click on your profile name &gt; Select Security Credentials.

![](https://miro.medium.com/v2/resize:fit:875/1*6JWzSpGOl5uHuMA7krmWLA.png align="left")

Scroll down to Access Keys &gt; Select Create Access Key.

![](https://miro.medium.com/v2/resize:fit:875/1*YFKZ1RWm20Er5rvtZB7RYw.png align="left")

Click on I understand checkbox &gt; Create Access Key.

![](https://miro.medium.com/v2/resize:fit:875/1*RROsebDu62uySd4hAzWHmA.png align="left")

Make sure you download the access key file and store it securely with you.

# **Task 2: Set up and install AWS CLI and configure your account credentials.**

Here is the official documentation for installing [AWS CLI in different OS.](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)

Install AWS CLI in your Linux machine using the following steps:

```plaintext
sudo apt-get update
sudo apt install unzip
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
unzip awscliv2.zip
sudo ./aws/install
```

![](https://miro.medium.com/v2/resize:fit:875/1*ZEHRIvTsqXxIQkHUtVaXmA.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*aRRO6wpp8x6-6HpVBWcXLQ.png align="left")

To check the version & installation, try running the commands:

```plaintext
aws --version
```

![](https://miro.medium.com/v2/resize:fit:875/1*qoA42E5Xc5JngtSrfqmHdg.png align="left")

Configure your account credentials by using:

```plaintext
aws configure
```

Pass the Access Key ID, Secret Access Key, Region Name, and default output format you need through the terminal.

Don’t worry, by the time you read this blog I would have deleted these access keys, so I am safe.

![](https://miro.medium.com/v2/resize:fit:875/1*efVss2yCTp-KlGsTLcGODg.png align="left")

Let’s check if the AWS CLI is working or not. To check the S3 bucket details:

```plaintext
aws s3 ls
```

To list all EC2 instances:

```plaintext
aws ec2 describe-instances
```

![](https://miro.medium.com/v2/resize:fit:875/1*pbs_tOPpjA4FUwi0Z9cvXA.png align="left")

Like this, we can use more of AWS CLI.

In this blog, I have discussed IAM Programmatic Access and AWS CLI. If you have any questions or would like to share your experiences, please leave a comment below. Don’t forget to read my blogs and connect with me on LinkedIn and let’s have a conversation.

To help me improve my blog and correct my mistakes, I am available on LinkedIn as [Mudit Mathur](https://www.linkedin.com/in/mudit--mathur/) . Do reach me and I am open to suggestions and corrections.

#Day42 #90daysofdevops