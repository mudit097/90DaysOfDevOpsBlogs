---
title: "Day 50: CI/CD Pipeline On AWS-Part 1 CodeCommit"
datePublished: Tue Oct 10 2023 00:58:29 GMT+0000 (Coordinated Universal Time)
cuid: clnjm5lct000008jo8pjwf4a6
slug: day-50-cicd-pipeline-on-aws-part-1-codecommit
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696899437367/2b5ddf9b-5089-48f0-96e4-1b4878f6942f.png
tags: blogging, aws, devops, 90daysofdevops, trainwithshubham

---

In the upcoming 4 blogs, we will be making a CI/CD pipeline on AWS with these tools: CodeCommit, CodeBuild, CodeDeploy, and CodePipeline.

In today’s learning, let’s deal with AWS CodeCommit.

What is AWS CodeCommit?

# **AWS CodeCommit**

AWS CodeCommit is a version control service hosted by Amazon Web Services that you can use to privately store and manage assets (such as documents, source code, and binary files) in the cloud.

> *Similar alternatives are GitHub (well-known and widely used), and Azure Repos (a Feature of Azure DevOps).*

# **Why CodeCommit?**

With CodeCommit, you can:

* Benefit from a fully managed service hosted by AWS.
    
* Store your code securely.
    
* Work collaboratively on code.
    
* Easily scale your version control projects.
    
* Store anything, anytime.
    
* Integrate with other AWS and third-party services.
    
* Easily migrate files from other remote repositories.
    
* Use the Git tools you already know.
    

# **How does CodeCommit work?**

![](https://miro.medium.com/v2/resize:fit:875/0*jesQO_wbNdzZM1ie.png align="left")

1. Use the AWS CLI or the CodeCommit console to create a CodeCommit repository.
    
2. From your development machine, use Git to run the git clone, specifying the name of the CodeCommit repository. This creates a local repo that connects to the CodeCommit repository.
    
3. Use the local repo on your development machine to modify (add, edit, and delete) files, and then run git add to stage the modified files locally. Run git commit to commit the files locally, and then run git push to send the files to the CodeCommit repository.
    
4. Download changes from other users. Run git pull to synchronize the files in the CodeCommit repository with your local repo. This ensures you’re working with the latest version of the files.
    

# **Tasks**

# **Task 1: Set up a code repository on CodeCommit and clone it on your local.**

Pre-requisites:

* You should have an AWS account.
    
* Install and configure the AWS Command Line Interface (CLI) on your local machine.
    

# **Step 1: Generate Git credentials**

Go to IAM Service &gt; Click on “Users” in the left navigation pane &gt; Create a New User &gt; Checkbox for Provide user access to the AWS Management Console — *optional &gt; Select* I want to create an IAM user and give password &gt; Click on Next.

![](https://miro.medium.com/v2/resize:fit:875/1*E6Qe3uSXPOsWBW5nbfvOqQ.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*AjCkVJLXuaoKw58S3h_Nag.png align="left")

In the next step &gt; Click on Attach Policies Directly &gt; Select the policy [AWSCodeCommitFullAccess](https://us-east-1.console.aws.amazon.com/iamv2/home?region=ap-south-1#/policies/details/arn%3Aaws%3Aiam%3A%3Aaws%3Apolicy%2FAWSCodeCommitFullAccess) &gt; Click on Create User.

![](https://miro.medium.com/v2/resize:fit:875/1*5dAh-nzxFzS9lnXNmG_LLg.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*x-reAPSLbogNP_hOjgwUkw.png align="left")

Download the .csv file since this is the only time you can view and download this password.

Open the User you created &gt; Go to the Security Credentials tab &gt; Scroll down to HTTPS Git credentials for AWS CodeCommit &gt; Select Generate Credentials &gt; Download credentials and click on Close.

These are the Git credentials for accessing CodeCommit.

# **Step 2: Set up a code repository on CodeCommit.**

Navigate to CodeCommit &gt; Give your Repository a name &gt; Click Create.

![](https://miro.medium.com/v2/resize:fit:875/1*NYLIEvw63dlA_N8Svz9htg.png align="left")

# **Step 3: Clone repository from CodeCommit.**

In the dashboard, click on HTTPS to copy the URL.

![](https://miro.medium.com/v2/resize:fit:875/1*ISXTB9c590YcDQHYmJHO_w.png align="left")

At your instance terminal:

```plaintext
#git clone <https>
git clone https://git-codecommit.ap-south-1.amazonaws.com/v1/repos/CodeCommit-Repo
```

For the prompt, give the credentials you downloaded earlier.

![](https://miro.medium.com/v2/resize:fit:875/1*DnfVRS4QhdVmgKcDbTHGeQ.png align="left")

Go to the repo directory you created now using the cd command.

![](https://miro.medium.com/v2/resize:fit:875/1*X1v3w5wNkZeZBvPBSJXx_w.png align="left")

Yes! You have created an empty repository in AWS CodeCommit and cloned it to your local.

# **Task 2: Add a new file from local and commit to your local branch. Push the local changes to the CodeCommit repository.**

# **Step 1: Add a new file from local and commit to your local branch.**

Create five files using:

```plaintext
touch file{01..05}.txt
```

![](https://miro.medium.com/v2/resize:fit:875/1*IieGyOkzjX9P3x0YYgVzbg.png align="left")

Add these files to the staging area, using:

```plaintext
git status
git add .
git status
```

![](https://miro.medium.com/v2/resize:fit:875/1*skfJH_kqfMC1VEa0TLLqhw.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*sxCW-vLfKMMFBH-hV3vT_w.png align="left")

To add these in the local repositories history:

```plaintext
git commit -m "Commiting the files I created now"
```

![](https://miro.medium.com/v2/resize:fit:875/1*h7ZtaJr9QbL-NIeNyUB3jw.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*QDNcvDveYAhJRW-Hmjymtg.png align="left")

# **Step 2: Push the local changes to the CodeCommit repository**

Using the following command, push the changes from your local to the CodeCommit repository.

```plaintext
git push origin master
```

![](https://miro.medium.com/v2/resize:fit:875/1*QDNcvDveYAhJRW-Hmjymtg.png align="left")

Verify that the files are pushed into the CodeCommit repository.

In the CodeCommit Repository &gt; Repositories &gt; Code.

![](https://miro.medium.com/v2/resize:fit:875/1*gfa3yDFiImCn5zAe0IR4IA.png align="left")

And yes! You have pushed your local files to the CodeCommit Repository.

In this blog, I have created a repository in CodeCommit, cloned it to the local, and pushed the files from local to the CodeCommit. If you have any questions or want to share your experiences, please comment below. Don’t forget to read my blogs and connect with me on LinkedIn and let’s have a conversation.

To help me improve my blog and correct my mistakes, I am available on LinkedIn as [Mudit Mathur.](https://www.linkedin.com/in/mudit--mathur/) Do reach me and I am open to suggestions and corrections.

#Day50 #90daysofdevops