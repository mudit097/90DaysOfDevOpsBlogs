---
title: "Jenkins Agents | Master & Agent(Slave) Nodes"
datePublished: Mon Sep 25 2023 21:37:58 GMT+0000 (Coordinated Universal Time)
cuid: clmzetswr000108l6binp999t
slug: jenkins-agents-master-agentslave-nodes
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1695677753658/91a924a9-d49f-4395-9453-66eea97b030b.png
tags: docker, aws, jenkins, 90daysofdevops, trainwithshubham

---

# **Jenkins Master (Server)**

Jenkins Master (Server) is the primary node that manages and distributes the software development processes across various worker nodes. It is responsible for coordinating the build process, managing plugins, and scheduling jobs. The Jenkins Master node serves as the central point of control for all tasks and workflows, and it provides a web interface for managing and monitoring the build process.

# **Jenkins Agent**

Jenkins Agent, also known as Jenkins Node is a worker node that executes the tasks and builds assigned by the Jenkins Master. It works as a distributed system where the Jenkins Master assigns tasks to Jenkins Agents, which then execute the tasks on the machines they are running on.

Jenkins Agents are often used to distribute builds and tests across multiple machines, allowing for parallel execution of tasks and faster build times. Jenkins Agents can be configured to run on a variety of machines, including physical machines, virtual machines, and containers to include any necessary tools and dependencies required for the tasks assigned by the Jenkins Master.

![](https://miro.medium.com/v2/resize:fit:875/0*2UFWdxPPkoOVTXSc align="left")

# **Project: Deploy a web app through Jenkins master to Jenkins worker node**

# **Set Up Jenkins-Master & Jenkins-Agent**

1. Create a 2 EC2 instance in AWS and connect both servers.
    

* jenkins-master
    
* jenkins-agent
    

![](https://miro.medium.com/v2/resize:fit:875/0*RuQMQvdP4lx85n52 align="left")

1. Now clear up the unwanted images from the jenkins-server
    

```plaintext
 docker rmi <image-name> --force
```

2\. Generate SSH key on the jenkins-master using “ssh-keygen” command.

```plaintext
ssh-keygen
```

![](https://miro.medium.com/v2/resize:fit:875/0*KRPPQ7c8VbSicTkp align="left")

3\. Now go to that folder and copy the id\_[rsa.pub](http://rsa.pub/) which is public key.

```plaintext
 cd .ssh
 ls
 cat id_rsa.pub
```

4\. Then on the jenkins-agent server, paste the public key from the jenkins-master in the authorized\_keys file.

```plaintext
 cd .ssh
 ls
 vi authorized_keys
```

![](https://miro.medium.com/v2/resize:fit:875/0*8A7RSdGjFkBo6it- align="left")

5\. Now from the jenkins-master we can connect the jenkins-agent server

```plaintext
 # inside ssh dir
 ssh ubuntu@<Public-IPv4-addr>

 # if we exit we will be back to jenkins-server.
```

![](https://miro.medium.com/v2/resize:fit:875/0*Ue75Pz1wgpEHf3I2 align="left")

6\. Make sure to install Java in the agent server.

```plaintext
 sudo apt-get update
 sudo apt-get install openjdk-11-jre
```

![](https://miro.medium.com/v2/resize:fit:875/0*a0z7SJdf1uyWsfZ4 align="left")

7\. Now go to the Jenkins Dashboard and click on Manage Jenkins.

8\. Now click on Manage Nodes & Clouds, and click on “+ New Node”

![](https://miro.medium.com/v2/resize:fit:875/0*6dRwdWyj-uYnmeKO align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*6IvPKpX-ak3agDoU align="left")

9\. Add details of the second agent node(make sure to fill in the Labels)

```plaintext
Node name: agent-node
✅ Permanent node

Name: agent
Desc: This is our agent which will run Node JS application

Number of executaion: 1 (cpu)
Remote root directory: /home/ubuntu/jenkins-agent
Labels: dev-server
Usage: Only build jobs with label expression matching this node
Launch method: launch agents via SSH
Host: <Public-IPv4-addr-agent>

Credentials:
Kind: SSH username with private key
ID: jenkins-ssh-key
Description: jenkins-ssh-key
Username: ubuntu
Private Key: <Private-key-master-node>
Host Key Verification Strategies: Non verifying verification strategy (SSH check with keys)
```

![](https://miro.medium.com/v2/resize:fit:726/0*X9JW1Q1JWmMsd15z align="left")

![](https://miro.medium.com/v2/resize:fit:621/0*9GDwnhOqIiM6TdQ2 align="left")

![](https://miro.medium.com/v2/resize:fit:746/0*tbtOlbsSDUk7GLtS align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*D68sfgKTw9TH5pEz align="left")

10\. Now click “OK” and Node will be connected and online.

![](https://miro.medium.com/v2/resize:fit:875/0*jYFNxvcOEUEwk3T3 align="left")

11\. Installed docker-compose for future requirements.

```plaintext
sudo apt-get install docker.io docker-compose
sudo usermod -aG docker $USER
sudo restart
```

![](https://miro.medium.com/v2/resize:fit:875/0*a5wuYFlcD2cMKJOw align="left")

# **Set Up Node Application**

1. Now create a new item with the pipeline, and named it(node-pipeline)
    

![](https://miro.medium.com/v2/resize:fit:801/0*X-uJYN06ltGJLLmS align="left")

2\. Now give it a description “This is a declarative pipeline for Node JS App” Put the GitHub repo

![](https://miro.medium.com/v2/resize:fit:875/1*zgmd105t15lG9D7oMJ3tUQ.jpeg align="left")

3\. Build Triggers ✅ GitHub hook triggers for GITScm polling.

![](https://miro.medium.com/v2/resize:fit:588/0*OL638o1X-BJx2xi_ align="left")

4\. Now we have to pass the pipeline script in the pipeline to test the script.

```plaintext
 pipeline {
     agent { label "dev-server" }
     stages{
         stage("Clone Code"){
             steps{
                 git url: "https://github.com/mudit097/node-todo-cicd.git", branch: "master"
             }
         }
         stage("Build and Test"){
             steps{
                 sh "docker build . -t node-app-test-new"
             }
         }
         stage("Push to Docker Hub"){
             steps{
                 echo "Docker Hub will receive the image"
             }
         }
         stage("Deploy"){
             steps{
                 sh "docker-compose down && docker-compose up -d"
             }
         }
     }
 }
```

5\. Now go to Manage Jenkins &gt; Manage Plugin and install the “Environment Injector” and Download and install after restart Jenkins. It will store all the environment variables where we can pass the credentials.

![](https://miro.medium.com/v2/resize:fit:875/0*AKxiXGRoxCru7QMt align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*Bz04QvqKvnhWwWSM align="left")

6\. Now go to Manage Jenkins &gt; Credentials &gt; System &gt; Global Credentials &gt; globals &gt; + Add Credentials

![](https://miro.medium.com/v2/resize:fit:875/1*sSnMhGTcLnB7cC-d-hlFUA.png align="left")

```plaintext
 Kind: username with password
 username: <DockerHub_Username>
 password: <DockerHub_Password>
 ID: dockerHub
 Desc: This is my Docker Hub Credentials
```

![](https://miro.medium.com/v2/resize:fit:875/1*zNiE5HGysZ5Kb-Ly48ej-g.png align="left")

7\. Now configure the pipeline for pushing the image into the docker hub.

```plaintext
 pipeline {
     agent { label "dev-server" }
     stages{
         stage("Clone Code"){
             steps{
                 git url: "https://github.com/LondheShubham153/node-todo-cicd.git", branch: "master"
             }
         }
         stage("Build and Test"){
             steps{
                 sh "docker build . -t node-app-test-new"
             }
         }
         stage("Push to Docker Hub"){
             steps{
                 withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                 sh "docker tag node-app-test-new ${env.dockerHubUser}/node-app-test-new:latest"
                 sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                 sh "docker push ${env.dockerHubUser}/node-app-test-new:latest"
                 }
             }
         }
         stage("Deploy"){
             steps{
                 sh "docker-compose down && docker-compose up -d"
             }
         }
     }
 }
```

![](https://miro.medium.com/v2/resize:fit:875/1*v3yGmwc241EsX0eLlyiqHQ.jpeg align="left")

8\. Click on Save, and your project will be tied to Jenkins-agent.

![](https://miro.medium.com/v2/resize:fit:875/1*IgcKAePAF2xJn_HRnAEyMQ.jpeg align="left")

9\. Now, build your project.

![](https://miro.medium.com/v2/resize:fit:875/0*0xohsN-UIRJOiyk8 align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*1xB9CEze49Kq1CCZ align="left")

10\. Open 8000 port on jenkins-agent, now the app can be accessed from the browser.

![](https://miro.medium.com/v2/resize:fit:875/0*trfZ7Z5Y0RM5-99B align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*_-ShzHtEjE3WI3rm align="left")

11\. Our application image is also pushed to DockerHub

![](https://miro.medium.com/v2/resize:fit:875/1*Rp8j9f1ATHh4_jp7hfCiRQ.jpeg align="left")

# **Set Up the Node app using Pipeline Script from SCM**

1. We can build the application using the Pipeline script from SCM by passing the GitHub URL where “Jenkinsfile” is present in the repository.
    
2. Now in the pipeline script, use “Pipeline script from SCM”
    
3. SCM: Git
    
4. Repository: &lt;URL-of-Git-Repo&gt;
    
5. Script Path: Jenkinsfile
    

![](https://miro.medium.com/v2/resize:fit:875/1*5vQeiXhwjkfcFCEYSNzUWw.jpeg align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*cdWYdztRU2MSeJ1B align="left")

Now the application is up & running and there is a new step added by Jenkins, Declarative Checkout SCM to verify that Jenfinsfile is available in the GitHub repo. Once the file is verified, then further steps proceed.

![](https://miro.medium.com/v2/resize:fit:875/0*vTKiQHIHhkFt10Vt align="left")

Congratulation!! The whole CI CD pipeline for this Node JS application is done including pushed images into the GitHub.