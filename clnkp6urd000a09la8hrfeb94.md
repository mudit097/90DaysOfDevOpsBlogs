---
title: "Day 53: CI/CD Pipeline On AWS-Part 4 CodeCommit"
datePublished: Tue Oct 10 2023 19:11:13 GMT+0000 (Coordinated Universal Time)
cuid: clnkp6urd000a09la8hrfeb94
slug: day-53-cicd-pipeline-on-aws-part-4-codecommit
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696965031718/54ecfa3b-8ed2-4993-8ce6-63d0256da9a4.png
tags: blogging, aws, devops, 90daysofdevops, trainwithshubham

---

# **AWS CodePipeline**

AWS CodePipeline is a continuous delivery service you can use to model, visualize, and automate the steps required to release your software.

You can quickly model and configure the different stages of a software release process. CodePipeline automates the steps required to release your software changes continuously.

You can refer to the official documentation by AWS to learn more about CodePipeline. The link is here: [https://docs.aws.amazon.com/codepipeline/index.html](https://docs.aws.amazon.com/codepipeline/index.html)

# **Tasks**

# **Create a CodePipeline that gets the code from CodeCommit, Builds the code using CodeBuild, and deploys it to a Deployment Group.**

We need to have a Deployment group for this activity. You can follow this link for that: [https://muditm12.hashnode.dev/day-52-cicd-pipeline-on-aws-part-3-codecommit](https://muditm12.hashnode.dev/day-52-cicd-pipeline-on-aws-part-3-codecommit)

Now in the AWS Management Console &gt; Navigate to CodePipeline &gt; Click on pipelines &gt; Create Pipeline

![](https://miro.medium.com/v2/resize:fit:875/1*D0eMNW80eMHAq5qI3ABE0g.png align="left")

# **Step 1: Choose pipeline settings**

Pipeline name: day53-app &gt; Select New Service Role &gt; Click on Next

![](https://miro.medium.com/v2/resize:fit:875/0*yHHUuXLxzcXMka6N align="left")

# **Step 2: Add source stage**

Source Provider: AWS CodeCommit &gt; Repository name & Branch Name: Select your repository & branch &gt; Change detection options: AWS CodePipeline &gt; Click on Next

![](https://miro.medium.com/v2/resize:fit:875/1*2jxXPXENED2T8uvnPY-ITw.png align="left")

# **Step 3: Add build stage**

Build provider: AWS CodeBuild &gt; Project Name: Select your Build Project &gt; Click on Next

![](https://miro.medium.com/v2/resize:fit:875/1*0zutQW3YgZAt4W6wuLJSbw.png align="left")

# **Step 4: Add the deploy stage**

Deploy provider: AWS CodeDeploy &gt; Application name & Deployment group : Select your respective choices &gt; Click on Next

![](https://miro.medium.com/v2/resize:fit:875/0*SKhoI-t5q_TMfyYu align="left")

Review your options and click on Create Pipeline.

![](https://miro.medium.com/v2/resize:fit:875/0*ZH5ER0HJk2zeYciQ align="left")

Once your pipeline is successfully created, you can see that this pipeline automatically triggers the code thereby automating the process.

![](https://miro.medium.com/v2/resize:fit:875/0*VXAA1D5k5k4dj_Nr align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*pfr8eS7RNkbmTGjC align="left")

And yay our pipeline is successfully run. To verify this let us reach our NginX server via our EC2 instance’s Public IPv4.

![](https://miro.medium.com/v2/resize:fit:875/1*I-RgEEIxpFwFb3kxu0hldQ.png align="left")

In this blog, I have used the AWS CodePipeline service. If you have any questions or want to share your experiences, please comment below. Don’t forget to read my blogs and connect with me on LinkedIn and let’s have a conversation.

To help me improve my blog and correct my mistakes, I am available on LinkedIn as [Mudit Mathur.](https://www.linkedin.com/in/mudit--mathur/) Do reach me, and I am open to suggestions and corrections.

#Day53 #90daysofdevops