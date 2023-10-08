---
title: "Project:- Deploy Flask App using ECS & ECR"
datePublished: Sun Oct 08 2023 00:05:19 GMT+0000 (Coordinated Universal Time)
cuid: clngpdip9000008l6d3fmh59p
slug: project-deploy-flask-app-using-ecs-ecr
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696723277891/98725562-c842-4f2b-9dd1-dae29fe77995.png
tags: aws, projects, devops, 90daysofdevops, trainwithshubham

---

# **What is ECS?**

* ECS stands for Elastic Container Service is a fully managed container orchestration service provided by AWS. It allows you to run, manage, and scale Docker containers in a highly scalable and flexible manner.
    
* With ECS, you can easily deploy containers as tasks within clusters of EC2 instances or by utilizing AWS Fargate, a serverless compute engine for containers.
    
* ECS takes care of the underlying infrastructure, including resource provisioning, load balancing, and automatic scaling, enabling you to focus on running your applications. It integrates seamlessly with other AWS services, providing a comprehensive ecosystem for building and deploying containerized applications.
    
* ECS offers features such as task definitions, which define container configurations, and services, which help with managing and scaling tasks. It provides fine-grained control over networking, security, and access control, ensuring reliable and secure container deployments at scale.
    

# **What is ECR?**

* ECR stands for Elastic Container Registry, it is a fully managed Docker container registry provided by AWS. ECR allows you to store, manage, and deploy Docker container images, making it easier to build, test, and deploy applications using containers.
    
* With ECR, you can securely store and share your container images, ensuring reliable access and high availability. It integrates seamlessly with other AWS services like ECS, EKS (Amazon Elastic Kubernetes Service), and CodePipeline, enabling streamlined container workflows.
    
* ECR supports private repositories, fine-grained access control, image lifecycle management, and automatic encryption at rest.
    
* By using ECR, developers can easily push, pull, and manage container images, while ensuring their availability, security, and scalability within the AWS ecosystem.
    

# **What is Fargate?**

* AWS Fargate is a serverless compute engine for containers provided by Amazon Web Services (AWS). It allows you to run containers without the need to manage the underlying infrastructure.
    
* With Fargate, you can focus solely on deploying and scaling your containers, while AWS takes care of provisioning and managing the necessary compute resources.
    
* Fargate abstracts away the complexities of managing EC2 instances and allows you to run containers as tasks directly. It automatically scales the underlying infrastructure based on the resource requirements specified in your task definitions.
    
* Fargate integrates seamlessly with other AWS services like ECS and EKS, enabling you to build scalable and highly available containerized applications.
    
* By using Fargate, developers can enjoy the benefits of serverless computing for containers, such as reduced operational overhead, improved resource utilization, and simplified deployment workflows, ultimately allowing them to focus more on application development and innovation.
    

# **Deploy Flask APP**

# **Setting Up EC2 instance**

* Create a new EC2 instance and SSH into it
    

![](https://miro.medium.com/v2/resize:fit:875/1*ndC0BUzAUNXvSKWPhLg5Aw.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*nugru0D6K8XVaEUL6sqf6A.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*STt7sAehmGsNTcodAplg0w.png align="left")

# **Create an ECS cluster:**

* In the ECS service, click on “Create Cluster”.
    

![](https://miro.medium.com/v2/resize:fit:875/1*uNXffI3qTuEQyMi3zmENJQ.png align="left")

* Configure the cluster settings, such as the cluster name, VPC, and subnet.
    

![](https://miro.medium.com/v2/resize:fit:875/1*05ytYzHa_ZIpIqqlr_ubkQ.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*COq_3U4bjsQOdImi9JSYrg.png align="left")

* We are using Fargate as Serverless and now Click on ‘Create’.
    

![](https://miro.medium.com/v2/resize:fit:875/1*x-2SqzJ4BRO13AI9jUvfiA.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*8z_UE09p7Q5vcKp-wfRfpA.png align="left")

# **Create an ECR repository to store the Image**

* In the ECR, Click on “Create Repository”
    

![](https://miro.medium.com/v2/resize:fit:875/1*H2oanQt0mDWod1ZbZr3rng.png align="left")

* Keep the repo public so that we can access easily.
    

![](https://miro.medium.com/v2/resize:fit:875/1*9rtFyJAKkLWBTK419nqu8Q.png align="left")

* Provide the reasonable repository name
    

![](https://miro.medium.com/v2/resize:fit:875/1*1Gpe7uuul9COOxlNaP_PYQ.png align="left")

* Once all the details are filled in, now click on “Create the Repository”.
    

![](https://miro.medium.com/v2/resize:fit:875/1*Uil_zhXrYLmllsIWxs_CfA.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*JZLritFiyxpj7u5PELlMTw.png align="left")

* The ECR Repo has been created, we have to push the application image from the server.
    

![](https://miro.medium.com/v2/resize:fit:875/1*2ULAMuQnnhICdF6jfgBnwg.png align="left")

# **Push the Flask Application Image to ECR Repo**

Setup docker into the EC2 instance

* Install docker in the EC2 Instance using below commands.
    

```plaintext
  sudo apt update
  sudo apt install docker.io -y

  sudo usermod -aG docker $USER
  sudo reboot
```

![](https://miro.medium.com/v2/resize:fit:875/1*O4Y6fowT90Lx7PBQZ3IdHA.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*zk8sdhVRxjLvFACp8GX8hA.png align="left")

* Now git clone the Flask app code from the GitHub Repo
    

```plaintext
git clone https://github.com/mudit097/flask-app-ecs.git
```

![](https://miro.medium.com/v2/resize:fit:875/1*cYCR0WsvDDUaFFBhSVSiIA.png align="left")

* Change into the repository folder.
    

```plaintext
  cd flask-app-ecs
```

![](https://miro.medium.com/v2/resize:fit:875/1*elI6wSwvbA_ChfNpR82Bbw.png align="left")

* We can verify the content of the file using cat command.
    

```plaintext
FROM python:3.7

RUN apt-get update -y 
COPY ./ /app
WORKDIR /app
RUN pip install flask
ENTRYPOINT [ "python" ]
CMD [ "run.py" ]
```

![](https://miro.medium.com/v2/resize:fit:875/1*cAop9ai1t8AMAN9hLoTHlg.png align="left")

* Now copy and paste the ECR commands one by one that is provided.
    

![](https://miro.medium.com/v2/resize:fit:875/1*revdZ5Rf4fhYtEBJm_Ysug.png align="left")

* Login to the ECR repo in the EC2 Instance using “View Push Command”
    

```plaintext
aws ecr-public get-login-password --region us-east-1 | docker login --username AWS --password-stdin public.ecr.aws/u4b9o6e2
```

![](https://miro.medium.com/v2/resize:fit:875/1*WXg-qHfdYJORcUTmBXPeJA.png align="left")

* Build the Flask app using Dockerfile.
    

```plaintext
docker build -t flask-app-dev .
```

![](https://miro.medium.com/v2/resize:fit:875/1*_IUtMponbK_kNnCQnOCFRA.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*ZBvoVKByU9zt4XGHCFQ4tQ.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*HQ_ktD1vGNKRKRGoKwIa2Q.png align="left")

* Tag the container
    

```plaintext
docker tag flask-app-dev:latest public.ecr.aws/u4b9o6e2/flask-app-dev:latest
```

![](https://miro.medium.com/v2/resize:fit:875/1*OAqT_FCThfSytlIw6cAWDw.png align="left")

* Now push container into ECR Container.
    

```plaintext
docker push public.ecr.aws/u4b9o6e2/flask-app-dev:latest 
```

![](https://miro.medium.com/v2/resize:fit:875/1*m4rEVMv1K2Z8KHzqTq4MaA.png align="left")

* We can verify in ECS that our image is pushed into the ECR repo.
    

![](https://miro.medium.com/v2/resize:fit:875/1*_mU3p1lqvWEh9_QzYBB67w.png align="left")

# **Create a task definition:**

* In the ECS service, click on “Task Definitions”, and then click on “Create new Task Definition”.
    

![](https://miro.medium.com/v2/resize:fit:875/1*qwwCYUHriQTBPQHLHgt5dw.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*6HZ3KOJ51TKC3NL-M4NvGg.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*FlO7M2nuhcmLb6papNrYHQ.png align="left")

* Set the container name to “run-flask-app”, and copy and paste the Image URL from ECR where we updated the flask app image previously. Specify the port mappings for HTTP, by setting the “Container port” to 80.
    

![](https://miro.medium.com/v2/resize:fit:875/1*zDNu2a5-ldYA09aKXMT8ig.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*tsuCXRoGVcpIbeSbI4LwCQ.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*kD-B1bKd83iyMGY9VG6TCg.png align="left")

* Choose the Fargate launch type, Configure the task settings, such as the task memory and CPU limits, here CPU is 1vCPU and the memory is 3GB.
    

![](https://miro.medium.com/v2/resize:fit:875/0*2Ndg7PKaBz-Ye4K7 align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*j27KGTnnpwu86YFW align="left")

* Monitor & logging
    

![](https://miro.medium.com/v2/resize:fit:875/0*XSZZEVc-qN4FcbK8 align="left")

* Now review the configuration and create the task definition.
    

![](https://miro.medium.com/v2/resize:fit:875/1*n1g-aTYD7cMYtJ9nBDz65w.png align="left")

* Run the Task Definition
    
* From the ECS container, click on Deploy and then Run Task
    

![](https://miro.medium.com/v2/resize:fit:875/1*TfFKEYU33jREAEK3tKbeYQ.png align="left")

* Select the cluster where it should run
    

![](https://miro.medium.com/v2/resize:fit:875/1*v353EMRTTpCI1LUWz4tD_g.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*EKc57syNdFc6baH0fGWUzQ.png align="left")

* In the Deployment Configuration provide the details.
    

![](https://miro.medium.com/v2/resize:fit:875/1*wOmRGeQ4eDvLwT7ioK-BlQ.png align="left")

* Choose the VPC and SG as per requirement.
    

![](https://miro.medium.com/v2/resize:fit:875/1*_hf1ARpcTstyMHW9TjkZ9Q.png align="left")

* Once the task definition is created, Now launch the task.
    

![](https://miro.medium.com/v2/resize:fit:875/1*aqItiVOK0HqpAjYmHUL1ug.png align="left")

* As the task is running, the app is successfully up & running.
    

![](https://miro.medium.com/v2/resize:fit:875/1*kKO9DewhF-6vMKdp8aGUDg.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*pfuC-J34JpFpoVDXCv0jxw.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*PbyZaZZmZEhoYGUrVw_FXQ.png align="left")

* Browse the Public IP address, you can see the default Flask app.
    

![](https://miro.medium.com/v2/resize:fit:875/1*vnWcO5hERZ6Cg5XqfKegLQ.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*SDm1weA2-MTqzXl7mb5oyA.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*ZbphQ5ALPpGWb0X4BuV3Gw.jpeg align="left")

In our project, “Deploy Flask App using ECS & ECR,” we explored essential AWS services like ECS, ECR, and Fargate. We deployed a Flask app on an EC2 instance within an ECS cluster, using an ECR repository to store our Docker image. This project provides a solid foundation for efficient containerized app deployment on AWS.

If you have any questions or want to share your experiences, please comment below. Don’t forget to read my blogs and connect with me on LinkedIn and let’s have a conversation.

To help me improve my blog and correct my mistakes, I am available on LinkedIn as [Mudit Mathur.](https://www.linkedin.com/in/mudit--mathur/) Do reach out to me; I am open to suggestions and corrections.

#project #90daysofdevops