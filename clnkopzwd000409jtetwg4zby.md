---
title: "Day 52: CI/CD Pipeline On AWS-Part 3 CodeCommit"
datePublished: Tue Oct 10 2023 18:58:06 GMT+0000 (Coordinated Universal Time)
cuid: clnkopzwd000409jtetwg4zby
slug: day-52-cicd-pipeline-on-aws-part-3-codecommit
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696964208393/c0075df4-fd0e-419b-9ff0-2d0442019f35.png
tags: aws, devops, jenkins, 90daysofdevops, trainwithshubham

---

In the previous blogs, we dealt with AWS CodeCommit & CodeBuild. In this blog let’s discuss AWS CodeDeploy.

# **AWS CodeDeploy**

CodeDeploy is a deployment service that automates application deployments to Amazon EC2 instances, on-premises instances, serverless Lambda functions, or Amazon ECS services.

CodeDeploy can deploy application content that runs on a server and is stored in Amazon S3 buckets, GitHub repositories, or Bitbucket repositories. CodeDeploy can also deploy a serverless Lambda function. You do not need to make changes to your existing code before you can use CodeDeploy.

CodeDeploy makes it easier for you to:

* Rapidly release new features.
    
* Update AWS Lambda function versions.
    
* Avoid downtime during application deployment.
    
* Handle the complexity of updating your applications, without many of the risks associated with error-prone manual deployments.
    

The service scales with your infrastructure so you can easily deploy to one instance or thousands.

# **Tasks**

# **Task 1: Deploy index.html file on EC2 machine using nginx (you have to set up a CodeDeploy agent to deploy code on EC2)**

You can refer to this link to understand how to utilize the AWS CodeCommit and CodeBuild services: [https://muditm12.hashnode.dev/day-51-cicd-pipeline-on-aws-part-2-codecommit](https://muditm12.hashnode.dev/day-51-cicd-pipeline-on-aws-part-2-codecommit)

Let’s create a CodeDeploy application:

Navigate to CodeDeploy &gt; Applications &gt; Click on Create Application.

![](https://miro.medium.com/v2/resize:fit:875/1*tkj_x5R5dm23V_Gc54sNQA.png align="left")

I am giving the below details:

![](https://miro.medium.com/v2/resize:fit:875/0*wOIdIlRXg_6pikS1 align="left")

> *Application Name: app-nginx*
> 
> *Compute platform: EC2/On-premises*

And click on Create Application.

![](https://miro.medium.com/v2/resize:fit:875/0*_XcLjzAKsVABTz5Q align="left")

We need to establish connections between CodeDeploy and other AWS services. How do we do it? We can connect the CodeDeploy to other AWS services by creating a service role in the IAM.

Navigate to Roles in IAM. And Create a New Role having these permissions:

[AmazonEC2FullAccess](https://us-east-1.console.aws.amazon.com/iamv2/home?region=us-east-1#/policies/details/arn%3Aaws%3Aiam%3A%3Aaws%3Apolicy%2FAmazonEC2FullAccess), [AmazonEC2RoleforAWSCodeDeploy](https://us-east-1.console.aws.amazon.com/iamv2/home?region=us-east-1#/policies/details/arn%3Aaws%3Aiam%3A%3Aaws%3Apolicy%2Fservice-role%2FAmazonEC2RoleforAWSCodeDeploy), [AmazonS3FullAccess](https://us-east-1.console.aws.amazon.com/iamv2/home?region=us-east-1#/policies/details/arn%3Aaws%3Aiam%3A%3Aaws%3Apolicy%2FAmazonS3FullAccess), [AWSCodeDeployRole](https://us-east-1.console.aws.amazon.com/iamv2/home?region=us-east-1#/policies/details/arn%3Aaws%3Aiam%3A%3Aaws%3Apolicy%2Fservice-role%2FAWSCodeDeployRole), [AWSCodeDeployFullAccess](https://us-east-1.console.aws.amazon.com/iamv2/home?region=us-east-1#/policies/details/arn%3Aaws%3Aiam%3A%3Aaws%3Apolicy%2FAWSCodeDeployFullAccess), [AmazonEC2RoleforAWSCodeDeployLimited](https://us-east-1.console.aws.amazon.com/iamv2/home?region=us-east-1#/policies/details/arn%3Aaws%3Aiam%3A%3Aaws%3Apolicy%2Fservice-role%2FAmazonEC2RoleforAWSCodeDeployLimited).

![](https://miro.medium.com/v2/resize:fit:875/0*9JB1xi8eD77dIJcL align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*2XX_XXdKjsSbkpAo align="left")

Let us change the trust relationship:

![](https://miro.medium.com/v2/resize:fit:875/0*UmDwX2wWBNyz-bl3 align="left")

We will need to have an EC2 instance to deploy the index.html file.

Let us create a deployment group:

In the CodeDeploy console &gt; Go to the Deployment Groups Tab &gt; Click on Create deployment group:

![](https://miro.medium.com/v2/resize:fit:875/0*uFN6k-BvNWehOonZ align="left")

Deployment group name: codedeploy-group

Service role: Select the service role which you created previously with all the permissions.

Deployment type: In-place

Environment configuration: Select Amazon EC2 instances. Select the key and value to select the EC2 instance you created for this activity.

![](https://miro.medium.com/v2/resize:fit:875/0*U_oYKoJ74u8KOnc7 align="left")

Install AWS CodeDeploy Agent: Never

Disable load balancing.

And click on create deployment group.

![](https://miro.medium.com/v2/resize:fit:875/0*r03gfGyIipsnwGSu align="left")

Now let us set up a CodeDeploy agent to deploy code on EC2.

> *The AWS CodeDeploy agent is a software package that is installed on instances in an Amazon EC2 Auto Scaling group or an Amazon EC2 instance. It enables the deployment of applications to these instances by interacting with the AWS CodeDeploy service.*

Install the CodeDeploy agent on your EC2 instance using the installation script.

```plaintext
#!/bin/bash
sudo apt-get update
sudo apt-get install ruby-full ruby-webrick wget -y
cd /tmp
wget https://aws-codedeploy-us-east-1.s3.us-east-1.amazonaws.com/releases/codedeploy-agent_1.3.2-1902_all.deb
mkdir codedeploy-agent_1.3.2-1902_ubuntu22
dpkg-deb -R codedeploy-agent_1.3.2-1902_all.deb codedeploy-agent_1.3.2-1902_ubuntu22
sed 's/Depends:.*/Depends:ruby3.0/' -i ./codedeploy-agent_1.3.2-1902_ubuntu22/DEBIAN/control
dpkg-deb -b codedeploy-agent_1.3.2-1902_ubuntu22/
sudo dpkg -i codedeploy-agent_1.3.2-1902_ubuntu22.deb
systemctl list-units --type=service | grep codedeploy
sudo service codedeploy-agent status
```

![](https://miro.medium.com/v2/resize:fit:875/0*1Hgm2F8z8-HUwyKT align="left")

COPY

```plaintext
bash install_codedeploy_agent.sh
```

We can see that the CodeDeploy agent is installed and running successfully.

![](https://miro.medium.com/v2/resize:fit:875/0*Mxc8X0Ka2KyLhGS7 align="left")

Let us create an index.html file. I am using my previous day’s tasks index.html file.

# **Task 2: Add appspec.yaml file to CodeCommit Repository and complete the deployment process.**

Let us create an appspec.yml file to deploy index.html on nginx. Also we will create two scripts for installing and starting nginx.

The contents of the appspec.yml file would look like:

```plaintext
version: 0.0
os: linux
files:
  - source: /
    destination: /var/wwiw/html
hooks:
  AfterInstall:
    - location: scripts/install_nginx.sh
      timeout: 300
      runas: root
  ApplicationStart:
    - location: scripts/start_nginx.sh
      timeout: 300
      runas: root
```

![](https://miro.medium.com/v2/resize:fit:711/0*aDD5mJL6Oj47tGMk align="left")

Let us push all the files to our CodeCommit repo.

![](https://miro.medium.com/v2/resize:fit:875/0*8iDbYk4D6psRblUJ align="left")

Now let us build the project using CodeBuild. While building select the S3 for Artifacts and also enable artifact packaging (.zip).

![](https://miro.medium.com/v2/resize:fit:875/0*av7UVw31aFyIlBpO align="left")

Click on Create Build project.

We can see that our build is succeeded.

![](https://miro.medium.com/v2/resize:fit:875/0*3EeEIDZsqpgVZNZU align="left")

Now go to the S3 and copy the location where the .zip file is located.

![](https://miro.medium.com/v2/resize:fit:875/0*XERlfTWuxFmXY7e3 align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*8i2-KZl9avfnImUi align="left")

Before that, I will have to create a Service role named new-service-role-for-ec2-s3-codedeploy for the EC2, S3, and CodeDeploy to communicate with each other, with the following permissions: [AmazonEC2FullAccess](https://us-east-1.console.aws.amazon.com/iamv2/home?region=us-east-1#/policies/details/arn%3Aaws%3Aiam%3A%3Aaws%3Apolicy%2FAmazonEC2FullAccess), [AmazonS3FullAccess](https://us-east-1.console.aws.amazon.com/iamv2/home?region=us-east-1#/policies/details/arn%3Aaws%3Aiam%3A%3Aaws%3Apolicy%2FAmazonS3FullAccess), [AWSCodeDeployFullAccess](https://us-east-1.console.aws.amazon.com/iamv2/home?region=us-east-1#/policies/details/arn%3Aaws%3Aiam%3A%3Aaws%3Apolicy%2FAWSCodeDeployFullAccess).

We will have to attach this role to our EC2 instance.

![](https://miro.medium.com/v2/resize:fit:875/0*9HPP0yBbc_HB7Sxq align="left")

Now go to Deployment Groups &gt; For the group which we created before &gt; Revision type, S3, and paste the above S3 URL:

![](https://miro.medium.com/v2/resize:fit:875/0*i84rUXSVlfZfOs3s align="left")

And click on Create the Deployment.

Once the deployment is successful, you should be able to reach it the output file of index.html.

In this blog, I have created a repository in CodeCommit, cloned it to the local, and pushed the files from local to the CodeCommit. Then using the CodeBuild, build the application using the Nginx server and upload the artifacts to S3. CodeDeploy can deploy application content that runs on a server and is stored in Amazon S3 buckets, GitHub repositories, or Bitbucket repositories. CodeDeploy can also deploy a serverless Lambda function.

If you have any questions or want to share your experiences, please comment below. Don’t forget to read my blogs and connect with me on LinkedIn and let’s have a conversation.

To help me improve my blog and correct my mistakes, I am available on LinkedIn as [Mudit Mathur.](https://www.linkedin.com/in/mudit--mathur/) Do reach me, and I am open to suggestions and corrections.

#Day52 #90daysofdevops