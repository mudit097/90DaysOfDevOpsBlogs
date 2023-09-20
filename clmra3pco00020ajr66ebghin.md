---
title: "An End-to-End Jenkins CI/CD Project Continuously Integrate and Deploy a NodeJS Application using Jenkins"
datePublished: Wed Sep 20 2023 05:03:33 GMT+0000 (Coordinated Universal Time)
cuid: clmra3pco00020ajr66ebghin
slug: an-end-to-end-jenkins-cicd-project-continuously-integrate-and-deploy-a-nodejs-application-using-jenkins
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1695185939216/6fd1163d-8a5e-46c6-838f-914d83335330.png
tags: blogging, docker, devops, jenkins, 90daysofdevops

---

In this blog, I will discuss GitHub WebHooks and an end-to-end Jenkins CI/CD project to continuously integrate and deploy a node.js application. Cherry on the cake: You can include this in your resume as proof of your Jenkins skills!

Before I directly jump into the project, let’s understand what Webhooks are.

# **1\. GitHub Webhooks**

Webhooks allow you to build or set up integrations that subscribe to certain events on GitHub.

Webhooks allow you to automate workflows and integrate your repositories with external services. When certain events occur, such as a push to a repository or the creation of a new issue, GitHub can send an HTTP POST payload to a specified URL endpoint.

## **1.1. How to create Webhooks?**

To create a GitHub webhook:

1. Go to the settings page for your repository.
    
2. Click on the “Webhooks & Services” tab.
    
3. Then, click on the “Add webhook” button.
    
4. In the webhook configuration, you will need to provide the following information:
    

* Payload URL: This is the URL that will receive the webhook notifications.
    
* Events: Select the events that you want to be notified about.
    
* Secret: This is a secret key that will be used to verify the authenticity of the webhook notifications.
    

5\. Once you have configured the webhook, click on the “Create webhook” button.

## **1.2. Why Webhooks?**

* To stay up-to-date on changes in your applications.
    
* To automate tasks.
    
* To improve security.
    

Now comes the interesting part of the blog. The CI/CD project. Let’s go!

# **2\. Jenkins CI/CD Project**

Project Explanation: I am going to continuously integrate and deploy a Node JS application on Docker using Jenkins and GitHub Integration.

This project is inspired and learned from [Shubham Londhe](https://hashnode.com/@ShubhamLondhe). The link to the live project deployment is [CI/CD project using Jenkins and GitHub Integration by Shubham Londhe](https://www.youtube.com/live/nplH3BzKHPk?feature=share).

The repository link used for this project is [https://github.com/mudit097/node-todo-cicd](https://github.com/mudit097/node-todo-cicd).

## **2.1. Task 1: Run the project using dockerfile**

Come let’s jump into the project:

1) Log in to the AWS Console. Open the EC2 service and create an EC2 Instance.

Here’s a detailed explanation of [how to create an EC2 instance.](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html)

2) Connect to the EC2 instance.

3) Install Docker, Docker-Compose, Java, and Jenkins in your system.

In my previous blogs, I have explained how to install these. Here are the links to the same: [Install Docker](https://muditm12.hashnode.dev/day-16-introduction-to-docker-for-devops-engineers), [Install Docker-Compose](https://muditm12.hashnode.dev/day-18-docker-compose-for-devops-engineers#heading-31-task-1-learn-how-to-use-the-docker-composeyml-file-to-set-up-the-environment-configure-the-services-and-links-between-different-containers-and-also-to-use-environment-variables-in-the-docker-composeyml-file), [Install Java, and Jenkins](https://muditm12.hashnode.dev/day-22-getting-started-with-jenkins#heading-32-installing-jenkins).

4) Once Jenkins is installed, Open port 8080 to your system in the AWS console. Log in to the Jenkins dashboard and create a freestyle Pipeline named “todo-node-app”.

Here’s a step-by-step guide on [how to create a Freestyle Pipeline in Jenkins!](https://muditm12.hashnode.dev/day-22-getting-started-with-jenkins#heading-41-task-1-create-a-freestyle-pipeline-to-print-hello-world)

![](https://miro.medium.com/v2/resize:fit:875/1*aSXwISFKm0O3vpughQSqdA.png align="left")

5) Go to Configure, in the General section &gt; Type the project description you want.

![](https://miro.medium.com/v2/resize:fit:875/1*18iYy-MoVv785lH4qssGGA.png align="left")

Scroll down to Source Code Management on the Configure page and paste the Repository URL and the branch your code is one. For me, it’s the master branch.

Since my repository is in a public branch, credentials are not required. I will explain in a later blog how to add credentials to Jenkins.

![](https://miro.medium.com/v2/resize:fit:875/1*NfkZOfkp2b7Gzpde5OTrHw.png align="left")

6) In the readme file, the developer has given the commands that need to be run for the application to become running.

From that we can conclude that these are the criteria required to create a docker file:

\-OS with NodeJS installed.

\-Copy Code.

\-Run the command npm install.

\-Expose port number 8080.

* Command node app.js for the application to be run.
    

If you are new to the docker file, here’s my blog explaining a [docker file and its format.](https://muditm12.hashnode.dev/day-17-task-docker-project-for-devops-engineers)

7) Before that, open port 8000 to the world for your system as they need to access the application. Here you can observe that port 8080 is also opened to your system IP as it’s the port used to access Jenkins.

![](https://miro.medium.com/v2/resize:fit:875/1*YSJosMbGgOMxh7Uujcj9vQ.png align="left")

8) Now in the host system, create a dockerfile.

```plaintext
sudo vim dockerfile
```

The dockerfile contents would look like this:

```plaintext
FROM node:12.2.0-alpine
WORKDIR /app
COPY . .
RUN npm install
EXPOSE 8000
CMD ["node","app.js"]
```

![](https://miro.medium.com/v2/resize:fit:875/1*pvB1KrGlIudkBO7i9shlIA.png align="left")

Save the file and exit, using the Esc button and typing:wq!.

9) Now in Jenkins go to Dashboard &gt; Configure &gt; Add Build Steps &gt; Execute Shell. In the Command section, type the following command:

```plaintext
sudo docker build . -t todo-node-app
sudo docker run -d --name todo-node-app -p 8000:8000 todo-node-app
```

![](https://miro.medium.com/v2/resize:fit:875/1*kZY_NicowNFs1kJL2NtUDA.png align="left")

Save & Build.

The build has failed as the daemon socket is unable to connect due to permission issues.

![](https://miro.medium.com/v2/resize:fit:875/1*oO05mOrV-jCrSLWRGRzKHA.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*y4ag_5rSt8nAuD9vCukHIg.png align="left")

To fix this, run the following commands:

```plaintext
sudo usermod -aG docker jenkins
sudo systemctl restart jenkins
```

After you run the above commands, refresh your Jenkins dashboard and then try re-building it.

![](https://miro.medium.com/v2/resize:fit:875/1*rYrpNfzTmL0aTWYCuskVOQ.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*yF9DLDefA-sPZlrnT-1XqA.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*671H4vF-uAXHIRUM9XVZLw.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*Na-u_d0c03FKb3rvA3LPfA.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*Ybn7IFXTB3S8FTKBVGfnlg.png align="left")

The error is solved. Job is successful. That means, the application is up and running. To access the application, use the following format of URL: public\_IP\_of\_EC2:8080.

This would open the following page:

![](https://miro.medium.com/v2/resize:fit:875/1*4chyEJzk_veEbOpIWiVQWw.png align="left")

10) All this was done manually. Let’s automate this. We use Webhooks for GitHub for any events that take place in the repository, like a push or a commit. And Jenkins, as it is integrated with GitHub Webhooks, will automatically build the job.

11) Before that let’s install the GitHub Integration plugin in Jenkins, to integrate it with Webhooks. Go to Manage Jenkins &gt; Manage Plugins &gt; Available Plugins &gt; Search for “GitHub Integration” &gt; Select Install Without Restart

![](https://miro.medium.com/v2/resize:fit:875/1*076p73u3SluE6MdgUkUMlA.png align="left")

Once the Installation starts, select Restart after installation is complete and wait for the Jenkins server to come up after the successful installation of the plugin.

12) In the AWS console, edit the Inbound rules of your host machine. Change port 8080 inbound rules from MyIP to Anywhere IPv4. We are enforcing this change as we need GitHub to access integration with Jenkins.

![](https://miro.medium.com/v2/resize:fit:875/1*Cp1MMGIkvN6eVr5cV4UeBg.png align="left")

13) Configure GitHub Webhook in the meantime. In the repository settings &gt; Go to Webhooks &gt; Add Webhook

![](https://miro.medium.com/v2/resize:fit:875/1*8tcT0pvZAokcWaDdCsBirw.png align="left")

The Payload URL will be in the format: [jenkins-URL/github-webhook](https://jenkins-url/github-webhook).

For example, my payload URL will look like this:

![](https://miro.medium.com/v2/resize:fit:798/1*xjUP_QAK_g10KV7cgwurNw.jpeg align="left")

Change content type to application/json.

![](https://miro.medium.com/v2/resize:fit:875/1*sJ6N2rtbib1vICfQHKGbXA.png align="left")

Select Just the push event and Active. Click on Add Webhook.

If the URL is correct and accessible, after a refresh of the page, a webhook will be successfully added. A green tick would appear, besides the payload URL, like the below picture:

![](https://miro.medium.com/v2/resize:fit:875/1*pUPtnGit9tTqa0J-YiWc9Q.png align="left")

For me, Webhook is successfully integrated.

14) Now go to Jenkins &gt; Dashboard &gt; Job &gt; Configure &gt; Build Triggers &gt; Select “GitHub hook trigger for GITScm polling”

![](https://miro.medium.com/v2/resize:fit:875/1*8T4jg7cWYGXovcFigSUdJw.png align="left")

Click on Save. Now change the code in GitHub a bit to see if the integration works.

15) To change the code go to repository &gt; Open views &gt; Open todo.js file &gt; Edit line number 17 to “I am performing Jenkins with GitHub Integration! I am completing an End to End Projects!”

![](https://miro.medium.com/v2/resize:fit:875/1*Tjemy0CehQRot7DvQ3VqDw.png align="left")

Commit changes.

![](https://miro.medium.com/v2/resize:fit:875/1*IOOWCsG3wEhwdE2idLun4w.png align="left")

We can observe that Build number 5 started on its own.

![](https://miro.medium.com/v2/resize:fit:875/1*5ztbSH7h8hl5ULafaG3nIw.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*jkUq_CTLkXV_zoAHKnmtDg.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*8o1JThkT-radozqyWEhxWw.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*dkokRAKqcM42p7gfHRe1_g.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*K9XxCBuD6UZmbFTDo8kwBA.png align="left")

16) We can observe the changes to the code we made by accessing the application:

![](https://miro.medium.com/v2/resize:fit:875/1*6zqLBTwVdkiCWCyOjiywgg.png align="left")

## **2.2. Task 2: Run the application using docker-compose.**

Make sure you have docker-compose installed in your system.

17) Add a docker-compose.yaml file to your project.

![](https://miro.medium.com/v2/resize:fit:875/1*NvKK9_PYoWqWxQh7Nq6sKA.png align="left")

The docker-compose.yaml would look like this:

```plaintext
version: '3.9'

services:
  web:
    image: "trainwithshubham/node-app-test-new:latest"
    ports:
      - "8081:8000"
```

18) In Jenkins go to Dashboard &gt; Configure &gt; Build Steps &gt; And add the following commands:

> *Caution: Before going ahead with the build, make sure you delete the previous containers by using the docker kill command.*

```plaintext
docker-compose down
docker-compose up --build -d
```

![](https://miro.medium.com/v2/resize:fit:875/1*2OskyizlVwttwWEo7F6ZuQ.png align="left")

Save & Build. You can see that the build was successful.

![](https://miro.medium.com/v2/resize:fit:875/1*vyFu7-PtWL0cHltXkrnKZQ.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*qKKgeFqGcoj5W23obNdFZQ.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*K7W3TcCm2n-GkKXUtxCy_A.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*BcieDFzcTMs-7LZ_uuq4Tg.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*4brTcR_0_vNRevmOdvKrwA.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*ZsjRGqQDZBUL-AVnqpjkUw.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*exXFKJUSKdGV2I_38glnAA.png align="left")

Try accessing the application.

![](https://miro.medium.com/v2/resize:fit:875/1*jq46gE9H-SlU5DMYsp1ltA.png align="left")

Yes ! My application is up and running.

We can see that the container is created by using the docker ps command:

![](https://miro.medium.com/v2/resize:fit:875/1*XObbu7dW7Ttof8qHULvdMw.png align="left")

In this blog, I have completed an end-to-end Jenkins CI/CD project to deploy Node JS using GitHub Integrations. Hope this helps you with your resume and learning. If you have any questions or would like to share your experiences, feel free to leave a comment below. Don’t forget to read my blogs and connect with me on LinkedIn and let’s have a conversation.

To help me improve my blog and correct my mistakes, I am available on LinkedIn as [Mudit Mathur](https://www.linkedin.com/in/mudit--mathur/). Do reach me and I am open to suggestions and corrections.

#Day24 #Day25 #90daysofdevops