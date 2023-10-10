---
title: "Day 51: CI/CD Pipeline On AWS-Part 2 CodeCommit"
datePublished: Tue Oct 10 2023 18:50:20 GMT+0000 (Coordinated Universal Time)
cuid: clnkog08g000s09jhevgicgjt
slug: day-51-cicd-pipeline-on-aws-part-2-codecommit
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696963727815/1814abf0-73e2-4aeb-b4d9-b073263cf3fa.png
tags: blogging, aws, devops, 90daysofdevops, trainwithshubham

---

In this blog, let’s discuss AWS CodeBuild.

# **AWS CodeBuild**

AWS CodeBuild is a fully managed build service in the cloud. CodeBuild compiles your source code, runs unit tests, and produces artifacts that are ready to deploy.

CodeBuild eliminates the need to provision, manage, and scale your own build servers.

It provides prepackaged build environments for popular programming languages and build tools such as Apache Maven, Gradle, and more.

You can also customize build environments in CodeBuild to use your own build tools. CodeBuild scales automatically to meet peak build requests.

# **How CodeBuild Works?**

![](https://miro.medium.com/v2/resize:fit:829/0*yHRcrd8jWlBJQ_DS.png align="left")

1. As input, you must provide CodeBuild with a build project.
    
2. A *build project* includes information about how to run a build, including where to get the source code, which build environment to use, which build commands to run, and where to store the build output.
    
3. A *build environment* represents a combination of operating systems, programming language runtime, and tools that CodeBuild uses to run a build. For more information, see:
    

* [Create a build project](https://docs.aws.amazon.com/codebuild/latest/userguide/create-project.html)
    
* [Build environment reference](https://docs.aws.amazon.com/codebuild/latest/userguide/build-env-ref.html)
    

1. CodeBuild uses the build project to create the build environment.
    
2. CodeBuild downloads the source code into the build environment and then uses the build specification (buildspec), as defined in the build project or included directly in the source code. A *buildspec* is a collection of build commands and related settings, in YAML format, that CodeBuild uses to run a build. For more information, see the [Buildspec reference](https://docs.aws.amazon.com/codebuild/latest/userguide/build-spec-ref.html).
    
3. If there is any build output, the build environment uploads its output to an S3 bucket. The build environment can also perform tasks that you specify in the buildspec. For an example, see [Build notifications sample](https://docs.aws.amazon.com/codebuild/latest/userguide/sample-build-notifications.html).
    
4. While the build is running, the build environment sends information to CodeBuild and Amazon CloudWatch Logs.
    
5. While the build is running, you can use the AWS CodeBuild console, AWS CLI, or AWS SDKs to get summarized build information from CodeBuild and detailed build information from Amazon CloudWatch Logs. If you use AWS CodePipeline to run builds, you can get limited build information from CodePipeline.
    

# **Buildspec file**

A buildspec file is a YAML file used in AWS CodeBuild to define the build and deployment stages of your project.

It provides instructions on how CodeBuild should build, test, and deploy your application.

# **Buildspec file name and storage location**

In AWS CodeBuild, the buildspec file should be named `buildspec.yml` or `buildspec.yaml`. It should be placed in the root directory of your source code repository.

You can use the `buildspecOverride` parameter to specify the file name and location of your buildspec.

You can specify only one buildspec for a build project, regardless of the buildspec file’s name.

# **Buildspec syntax**

The syntax used in a buildspec file is:

```plaintext
version: 0.3

phases:
  pre_build:
    commands:
      - echo "Installing dependencies..."
      - npm install

  build:
    commands:
      - echo "Building the application..."
      - npm run build

  post_build:
    commands:
      - echo "Running tests..."
      - npm test

artifacts:
  files:
    - index.html
    - dist/**
  discard-paths: yes
```

version

Required mapping. Represents the buildspec version. We recommend that you use `0.2`.

run-as

Optional sequence. Available to Linux users only. Specifies a Linux user that runs commands in this buildspec file. `run-as` grants the specified user read and run permissions. When you specify `run-as` at the top of the buildspec file, it applies globally to all commands.

env

Optional sequence. Represents information for one or more custom environment variables.

* env/shell: Optional sequence. Specifies the supported shell for Linux or Windows operating systems.
    
* env/variables: Required if `env` is specified, and you want to define custom environment variables in plain text.
    
* env/parameter-store: Required if `env` is specified, and you want to retrieve custom environment variables stored in Amazon EC2 Systems Manager Parameter Store.
    
* env/secrets-manager: Required if you want to retrieve custom environment variables stored in AWS Secrets Manager.
    
* env/exported-variables: Used to list environment variables you want to export.
    
* env/git-credential-helper: Used to indicate if CodeBuild uses its Git credential helper to provide Git credentials.
    

proxy

Used to represent settings if you run your build in an explicit proxy server. Optional setting.

phases

Required sequence. Represents the commands CodeBuild runs during each phase of the build.

artifacts

Optional sequence. Represents information about where CodeBuild can find the build output and how CodeBuild prepares it for uploading to the S3 output bucket.

# **Tasks**

# **Task 1: Create a simple index.html file in CodeCommit Repository.**

I am using the repository that was used.

Clone the repository using git clone.

Create an index.html file.

```plaintext
vim index.html
```

The contents of index.html would be:

```plaintext
<DOCTYPE html>
<html>
          <head>
                      <style>
      body {
                      font-family: Arial, sans-serif;
                              background-color: #f2f2f2;
                                      color: #333;
                                              text-align: center;
                                                    }

            h1 {
                            font-size: 36px;
                                    margin-top: 50px;
                                            color: #6130e8;
                                                  }

                  p {
                                  font-size: 18px;
                                          margin: 20px 0;
                                                }
                      </style>
                        </head>
                          <body>
                                      <h1>Welcome to my new page - Mudit Mathur</h1>
                                          <p>Contribute to DevOps Community</p>
                                            </body>
</html>
```

![](https://miro.medium.com/v2/resize:fit:875/0*NVA8Z76HsfrNPMkn.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*3pWRB099mek9Yhud.png align="left")

Add these changes and commit to the repository.

```plaintext
git add .
git commit -m "Adding index.html file"
```

![](https://miro.medium.com/v2/resize:fit:875/0*qzRnWfEkdpY-0L7y.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*S42-E9_tBzOcYOYm.png align="left")

Let us push these changes to the CodeCommit repository.

```plaintext
git push origin master
```

![](https://miro.medium.com/v2/resize:fit:875/0*eIs8aRN6264AnDHh.png align="left")

Verify the same in the CodeCommit.

![](https://miro.medium.com/v2/resize:fit:875/0*8H-OMioozgV9OPt9.png align="left")

# **Task 2: Add buildspec.yaml file to CodeCommit Repository and complete the build process.**

Let us create the buildspec.yaml file and push it to our repository.

```plaintext
vim buildspec.yaml
```

![](https://miro.medium.com/v2/resize:fit:875/0*ScaUkXBRvnPQQmBO.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*HmFJ_iKURZU2XVuL.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*pAKvwRdV9YUTqQM9.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*oiZcHGC0Y9DfidoI.png align="left")

Make sure you have the indentations correct for your buildspec.yml file.

The buildspec.yml file contains:

```plaintext
version: 0.2

phases:
  install:
    commands:
      - echo Installing NGINX
      - sudo apt-get update
      - sudo apt-get install nginx -y
  build:
    commands:
      - echo Build started on 'date'
      - cp index.html /var/www/html/
  post_build:
    commands:
      - echo Configuring NGINX

artifacts:
  files:
    - /var/www/html/index.html
```

In the left navigation panel &gt; Go to Build: CodeBuild &gt; Build Projects &gt; Click on Create Build Projects.

![](https://miro.medium.com/v2/resize:fit:875/0*70iFeYmVibggXQ7Y.png align="left")

Project name: codebuild

In the source section, Select AWS CodeCommit as Source Provider and select the repository, and branch your code is hosted.

![](https://miro.medium.com/v2/resize:fit:875/0*lzTkIIN1LVD9WRmh.png align="left")

In the Environment section, Select OS as Ubuntu.

![](https://miro.medium.com/v2/resize:fit:875/0*64KmWNSLhC8g422y.png align="left")

And create a New Service Role.

![](https://miro.medium.com/v2/resize:fit:875/0*RGSiOT4hFtcRD7el.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*0PdZebeskj2ECrVk.png align="left")

And let others be the default, click on Create build project.

![](https://miro.medium.com/v2/resize:fit:875/0*nbzncespWlF-FFZG.png align="left")

Click on Start Build. Wait until the build succeeds.

![](https://miro.medium.com/v2/resize:fit:875/0*3Pyl2R-kXg1GiAv5.png align="left")

We add these artifacts to the project and store them in an S3 bucket.

First, let us create an S3 Bucket.

![](https://miro.medium.com/v2/resize:fit:875/0*xghn-vMXixmefn-S.png align="left")

We need this bucket to be accessible to the public. Let others be the default and click on Create Bucket.

![](https://miro.medium.com/v2/resize:fit:875/0*LnYzRl7BvY5UdZGy.png align="left")

In the CodeBuild &gt; Build console &gt; Click on Edit &gt; Artifacts.

![](https://miro.medium.com/v2/resize:fit:875/0*3Gxr6DkxyGfxZRFw.png align="left")

Select the Amazon S3 for Artifact Type and select the bucket you just created.

And click on Update Artifacts.

![](https://miro.medium.com/v2/resize:fit:875/0*WWgUNODn1X4mHWyo.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*1SxdC6lOydOYoWWB.png align="left")

Click on Build again.

Once the build is successful, you can see that the artifacts are uploaded to the S3 bucket.

![](https://miro.medium.com/v2/resize:fit:875/0*JqedNN51IjoKi__E.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*oqlBIsI53suVSvkL.png align="left")

Navigate through the index.html file in the CodeBuild:

![](https://miro.medium.com/v2/resize:fit:875/0*AcTdbz4nQgJ9sJ_g.png align="left")

Use the Open tab to reach the server.

![](https://miro.medium.com/v2/resize:fit:875/0*fYxB6VZ2wNtQ9VQi.png align="left")

In this blog, I have created a repository in CodeCommit, cloned it to the local, and pushed the files from local to the CodeCommit. Then using the CodeBuild, build the application using the Nginx server and uploaded the artifacts to S3. If you have any questions or want to share your experiences, please comment below. Don’t forget to read my blogs and connect with me on LinkedIn and let’s have a conversation.

To help me improve my blog and correct my mistakes, I am available on LinkedIn as [Mudit Mathur](https://www.linkedin.com/in/mudit--mathur/). Do reach me, and I am open to suggestions and corrections.

#Day51 #90daysofdevops