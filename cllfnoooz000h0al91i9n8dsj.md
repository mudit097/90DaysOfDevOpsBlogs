---
title: "Day-22 Getting Started with Jenkins"
datePublished: Thu Aug 17 2023 21:10:50 GMT+0000 (Coordinated Universal Time)
cuid: cllfnoooz000h0al91i9n8dsj
slug: day-22-getting-started-with-jenkins
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692293538909/775e9adc-6942-46d6-89f8-79a6f22f88e5.jpeg
tags: ubuntu, java, devops, jenkins, 90daysofdevops

---

In this blog, I will introduce and explain Jenkins, the lifeline for a CI/CD engineer. Also, I will create a Jenkins freestyle project to understand the working of Jenkins.

But let us understand what is CI/CD first.

# **1\. 🔄 CI/CD**

CI stands for Continuous Integration and CD stands for Continuous Delivery/Deployment.

Continuous integration (CI) is a software development practice in which developers merge their changes to a shared mainline several times a day.

Continuous Delivery (CD) takes CI further by automating the deployment process. It involves continuously preparing the software application for deployment by packaging it, configuring the environment, and performing additional tests, such as user acceptance testing (UAT).

Continuous Deployment is an extension of Continuous Delivery where the deployment process is fully automated.

A CI/CD pipeline is a series of automated steps or stages that enable Continuous Integration (CI) and Continuous Delivery/Deployment (CD) of software applications.

There are a few popular tools for CI/CD pipeline such as Jenkins, GitLab, CircleCI, Bamboo, Azure DevOps, etc.

Jenkins is one of the most widely used, mainly as it is open source, which is also my topic to discuss for the next few days! Let’s go!

# **2\. 🏗️ Jenkins**

Jenkins is a self-contained, open-source automation server that can be used to automate all sorts of tasks related to building, testing, and delivering or deploying software. Jenkins is based on Java programming language.

## **2.1 Why Jenkins?**

* Jenkins is open-source and free to use.
    
* Jenkins is very versatile.
    
* Jenkins has a large and active community.
    
* Jenkins is constantly being updated.
    
* Jenkins is flexible and customizable.
    
* Jenkins supported customizable build.
    

## **2.2 Jenkins Architecture**

Jenkins is based on the Master-Slave architecture.

![](https://miro.medium.com/v2/resize:fit:625/0*9IdIEYx3xSXF9vZe align="center")

The master node is responsible for managing the system and coordinating the workload, while the slave nodes (also called agents or workers) perform the actual build and deployment tasks.

The master node communicates with the slave nodes to assign jobs, collect build results, and monitor progress. Slave nodes can be distributed across different machines, allowing for parallel execution and workload distribution.

# **3\. 🛠️ Setting up Jenkins**

Launch an EC2 instance based on Ubuntu and connect to it. I have followed the Jenkins official documentation for [Installing Jenkins on Linux: Official Documentation](https://www.jenkins.io/doc/book/installing/linux/).

## **3.1 Prerequisites**

Minimum hardware requirements:

* 256 MB of RAM
    
* 1 GB of drive space (although 10 GB is a recommended minimum if running Jenkins as a Docker container)
    

Jenkins requires Java 11 or 17 since Jenkins 2.357 and LTS 2.361.1.

## **3.2 Installing Jenkins**

1. Install Java 11 on your machine.
    
    ```plaintext
     sudo apt-get update
     sudo apt install openjdk-11-jdk
    ```
    
    ![](https://miro.medium.com/v2/resize:fit:875/1*h1jRQiegs3Bh56ULDIBbkg.jpeg align="center")
    
    To check the version installed, use the following command:
    
    ```plaintext
     java -version
    ```
    
    ![](https://miro.medium.com/v2/resize:fit:875/1*5tKs-UreBdsSJdnnescqLg.jpeg align="center")
    
2. Install Jenkins.
    
    Download the Jenkins repository key and save it in a file using sudo.
    
    ```plaintext
     curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
       /usr/share/keyrings/jenkins-keyring.asc > /dev/null
    ```
    
    Add the Jenkins repository as a package for the package manager (apt) on your Ubuntu.
    
    ```plaintext
     echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
       https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
       /etc/apt/sources.list.d/jenkins.list > /dev/null
    ```
    
    ![](https://miro.medium.com/v2/resize:fit:875/1*mS9JuDRGuUoVJG6Ebc6STg.jpeg align="center")
    
    Update your system, again.
    
    ```plaintext
     sudo apt-get update
    ```
    
    Install Jenkins:
    
    ```plaintext
     sudo apt-get install jenkins
    ```
    
    ![](https://miro.medium.com/v2/resize:fit:875/1*lR3-d3yK_Xn5qe42HPIwxg.jpeg align="center")
    
3. Configure Jenkins
    
    On your AWS console, modify the security group for Inbound rules. Open port 8080 to your host from CustomTCP.
    
    ![](https://miro.medium.com/v2/resize:fit:875/1*XEF6UnHj7KDz-msMVDjt2Q.jpeg align="center")
    
    Verify Jenkins configuration by opening it in your browser.
    
    Open your hostIP:8080 in your browser. You should get the “Getting Started” page.
    
    > *Trivia: Why do we use port 8080? Port 8080 is used for Web servers.*
    > 
    > *Since Jenkins is Apache tomcat based Web server (HTTP), the default is port 8080.*
    
    ![](https://miro.medium.com/v2/resize:fit:875/1*n9USu3SRi9u_F1Gh4Mmd0Q.jpeg align="center")
    
    Use the directory and your host using the following command to get the administrator password.
    
    ```plaintext
    sudo cat /var/lib/jenkins/secrets/initialAdminPassword
    ```
    
    ![](https://miro.medium.com/v2/resize:fit:875/1*IGCZFpFH2b2QZUxYcqQu9w.jpeg align="center")
    
    You will be led to the “Customize Jenkins” page. Select “Install suggested plugins”
    
    ![](https://miro.medium.com/v2/resize:fit:875/1*WUhyeEnTYKf5XY-R59Vq6w.jpeg align="center")
    
    Wait for the installation of plugins to complete. It usually takes 4–8 minutes.
    
    Once the installation is complete, the “Create First Admin User” page appears. Provide the details and go ahead by clicking on Save and Continue.
    
    ![](https://miro.medium.com/v2/resize:fit:875/1*WUhyeEnTYKf5XY-R59Vq6w.jpeg align="center")
    
    Wait for the installation of plugins to complete. It usually takes 4–8 minutes.
    
    Once the installation is complete, the “Create First Admin User” page appears. Provide the details and go ahead by clicking on Save and Continue.
    
    ![](https://miro.medium.com/v2/resize:fit:875/1*8qKczrFLlrw_n_Yjj8wRaQ.jpeg align="center")
    
    Now the “Jenkins is Ready!” page appears. Click on “Start using Jenkins”.
    
    ![](https://miro.medium.com/v2/resize:fit:875/1*DgISzPHo1N-Z7aEBFP9hbg.jpeg align="center")
    
    Congratulations! You have successfully installed Jenkins on your host and connected to the Jenkins web server.
    
    ![](https://miro.medium.com/v2/resize:fit:875/1*jK1MmxGwCo7PU_jx51537A.jpeg align="center")
    

# **4\. ✅ Tasks**

## **4.1 Task 1: Create a freestyle pipeline to print “Hello World!”**

1. Click on “New Item” to create a new Jenkins job.
    
    ![](https://miro.medium.com/v2/resize:fit:875/1*I_u-m6RPpTArt3xVHiSlzw.jpeg align="left")
    
2. Enter the name for the job “HelloWorldPipeline” and select “Freestyle project”, then click “OK”.
    
    ![](https://miro.medium.com/v2/resize:fit:875/1*K2Eb1yXNXrgefOEtjr8DrQ.jpeg align="left")
    
3. In the configuration page that appears, scroll down to the “Build” section. Click on the “Add build step” dropdown and select “Execute shell” as the host machine’s OS is Linux.
    
    ![](https://miro.medium.com/v2/resize:fit:875/1*XY7pRq6WvztuvvK6Ck2IDw.jpeg align="left")
    
    Once you select Execute shell, the Execute shell window opens. In the command section, enter the following:
    
    ```plaintext
    echo "Hello World!"
    ```
    
    Click on Save, after entering the command to save the pipeline configuration.
    
    ![](https://miro.medium.com/v2/resize:fit:875/1*rjB1sWS7aTCc5Wu3dDah2Q.jpeg align="left")
    
4. Run the pipeline, to see the output in the console log. To run the pipeline, go to your Pipeline dashboard and click on Build Now.
    
    ![](https://miro.medium.com/v2/resize:fit:875/1*fZRUXYHqOTHnbz2UUnn0dQ.jpeg align="left")
    
    View the output in the Console output.
    
    ![](https://miro.medium.com/v2/resize:fit:875/1*vy84IJ8EO6jkoTY1fYxoKQ.jpeg align="left")
    
    Well, you can see that the build is successful, and the console output is proof of that.
    
    Yeah! This can be a mini-project to get hands on the Jenkins freestyle pipeline project.
    
    ## **4.2 Task 2: What have you understood in Jenkins? Write a small article in your own words.**
    
    For me, Jenkins is a tool all about automating the process so that I can reduce the time and manpower utilized and increase the productivity and accuracy of the tasks performed. By creating CI/CD pipelines we automate the SDLC, thereby decreasing human intervention.
    
    I understand Pipelines as a series of connected stages that helps in the flow, of day-to-day life. For example water pipeline, sewage pipeline, oil pipeline, etc. The same way is CI/CD Pipelines where the steps of SDLC are automated.
    
    For example, Jenkins projects can also be built in such a way that once a code is committed in the VCS, like GitHub, it automatically builds the next step.
    
    Jenkins is based on Master-Slave architecture. Jenkins is installed ONLY on the Master node. There is no Jenkins on slave nodes. Java should be installed on all nodes.
    
    When builds are executed on the Master node, the workspace will be created on the Slave. Job is completed on the slave/agent and the workspace files can be seen on Master Node.
    
    To conclude, Jenkins is an Open-Source tool, that is helping developers all over the world to automate the SDLC and easily implement the CI/CD pipelines.
    
    In this blog, I have understood and written about Jenkins, Jenkins architecture, Jenkins Setup, and a mini-project on Jenkins. If you have any questions or would like to share your experiences, feel free to leave a comment below. Don’t forget to read my blogs and connect with me on LinkedIn and let’s have a conversation.
    
    To help me improve my blog and correct my mistakes, I am available on LinkedIn as [Mudit Mathur](https://www.linkedin.com/in/mudit--mathur/). Do reach me and I am open to suggestions and corrections.
    
    #Day22 #90daysofdevops