---
title: "Launching your Kubernetes Cluster with Deployment"
datePublished: Fri Sep 29 2023 16:06:49 GMT+0000 (Coordinated Universal Time)
cuid: cln4srccp000509mse9mv2pt7
slug: launching-your-kubernetes-cluster-with-deployment
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696003482461/e25aa51d-c4db-46ae-973d-a80675bbe8a7.jpeg
tags: aws, kubernetes, devops, 90daysofdevops, trainwithshubham

---

# **Deployment in K8s**

* A Deployment is a high-level resource that provides declarative updates for managing a set of identical replicas of a pod. A pod is the smallest deployable unit in Kubernetes that represents a single instance of a containerized application.
    
* Deployments use a rolling update strategy by default, which ensures that new replicas are gradually introduced and old replicas are gracefully terminated. This strategy helps to minimize downtime and ensure that the application remains available during the update process.
    

# **Use Case**

The following are typical use cases for Deployments:

* [Create a Deployment to rollout a ReplicaSet](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#creating-a-deployment). The ReplicaSet creates Pods in the background. Check the status of the rollout to see if it succeeds or not.
    
* [Declare the new state of the Pods](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#updating-a-deployment) by updating the PodTemplateSpec of the Deployment. A new ReplicaSet is created and the Deployment manages moving the Pods from the old ReplicaSet to the new one at a controlled rate. Each new ReplicaSet updates the revision of the Deployment.
    
* [Rollback to an earlier Deployment revision](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#rolling-back-a-deployment) if the current state of the Deployment is not stable. Each rollback updates the revision of the Deployment.
    
* [Scale up the Deployment to facilitate more load](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#scaling-a-deployment).
    
* [Pause the rollout of a Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#pausing-and-resuming-a-deployment) to apply multiple fixes to its PodTemplateSpec and then resume it to start a new rollout.
    
* [Use the status of the Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#deployment-status) as an indicator that a rollout has stuck.
    
* [Clean up older ReplicaSets](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#clean-up-policy) that you don’t need anymore.
    

# **Example of NGINX Deployment:**

```plaintext
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```

# **Components of Deployment**

The key components of deployment in Kubernetes are:

1. **Labels and Selectors:** Labels are key-value pairs attached to Kubernetes objects, including pods and deployments. Selectors are used to specify criteria based on labels to identify and group related objects. Deployments use labels and selectors to manage and control the pods associated with them.

2\. **Scaling:** Deployments allow you to scale your application horizontally by adjusting the number of replicas. You can manually scale up or down based on the desired load or configure autoscaling based on metrics such as CPU utilization.

3\. **Replicas:** The number of replicas determines how many instances of your application should be running at any given time. It allows you to scale your application horizontally by increasing or decreasing the number of replicas.

4. **Pod Template:** A deployment specifies a pod template that defines the desired state of the pods running your application. It includes details such as the container image, environment variables, resource limits, and volumes.

5. **Rollback**: Kubernetes deployments support rollback functionality. If an update doesn’t work as expected, you can roll back to the previous version of your application by specifying the revision or using the built-in rollback command.

6\. **Health Checks:** Kubernetes provides liveness and readiness probes to check the health of your application. Liveness probes determine if the application is running properly, and readiness probes indicate if the application is ready to accept traffic.

# **Task 1: Create one Deployment file to deploy a sample todo-app on K8s using the “Auto-healing” and “Auto-Scaling” feature**

1. Clone the repository into the master.
    

```plaintext
 git clone https://github.com/mudit097/django-todo-cicd.git
```

![](https://miro.medium.com/v2/resize:fit:875/1*DY0_QE_S6jiltMuRxUzK7g.png align="left")

2\. Create an image from the Dockerfile

```plaintext
 cat Dockerfile

 docker build . -t mudit097/django-todo:latest
```

![](https://miro.medium.com/v2/resize:fit:875/1*9hlsMfPtxTRuGuXgOXZkng.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*K5qFCvhzDBW7FjbYGkPLfQ.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*OjS8RLbgiw6iS4XoOPinGA.png align="left")

3\. Check the docker image and push it into DockerHub.

```plaintext
 docker images

 docker login

 docker push mudit097/django-todo:latest
```

![](https://miro.medium.com/v2/resize:fit:875/1*rU-PsQlRlN2tSPh0ZGGbfg.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*OGr_6e4WuI8biM_5IpzJ_w.png align="left")

4\. Now we can verify in the DockerHub that image is pushed into the repo.

![](https://miro.medium.com/v2/resize:fit:875/1*9fS1i49fNNjLYkWny2KUig.png align="left")

5\. Then create a Manifest file named deployment.yml where all the configuration related to the image will store. Add a deployment.yml file. vim deployment.yml

```plaintext
 apiVersion: apps/v1
 kind: Deployment
 metadata:
   name: my-django-app-deployment
   labels:
     app: django-app
 spec:
   replicas: 2
   selector:
     matchLabels:
       app: django-app
   template:
     metadata:
       labels:
         app: django-app
     spec:
       containers:
       - name: django-app-container
         image: mudit097/django-todo:latest
         ports:
         - containerPort: 8000
```

![](https://miro.medium.com/v2/resize:fit:875/1*jGa_0V0jgIQfsCl9m16rVA.png align="left")

6\. Apply the deployment to your k8s (minikube) cluster by following the command

```plaintext
 kubectl apply -f deployment.yml
```

![](https://miro.medium.com/v2/resize:fit:875/1*-uaLr1Iy5E0WUt_SqR_LnA.png align="left")

7\. We can verify the pods are running,

```plaintext
 kubectl get pods
```

![](https://miro.medium.com/v2/resize:fit:875/1*JB3bq3eUnGnmu0wBKU4ubA.png align="left")

8\. On the worker node, to test docker container working or not.

```plaintext
 # Get the list of running docker container
 docker ps

 # Get into the docker container
 sudo docker exec -it <docker-container> bash

 curl -L http://127.0.0.1:8000
```

![](https://miro.medium.com/v2/resize:fit:875/1*k410ZxrL8UV-fU2kV96hjg.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*o3aqO5LmEPeAMNiOvFxjsg.png align="left")

9\. Now we can delete a pod by using the following command,

```plaintext
 kubectl delete pod <pod-name>
```

![](https://miro.medium.com/v2/resize:fit:875/1*XzMI9XXworOQkjEfvMfINg.png align="left")

10\. But after deleting a pod still we get 2 pods as Auto Healing is working, so even though 1 pod is removed or deleted a new pod is replaced with the older one.

```plaintext
kubectl get pods
```

![](https://miro.medium.com/v2/resize:fit:875/1*8Q55AjWv36_Pai_mQ6OnhA.png align="left")

11\. To delete a complete deployment, so that deployment is brought down we can use the following command,

```plaintext
kubectl delete -f deployment.yaml
```

![](https://miro.medium.com/v2/resize:fit:875/1*ALXF-RKDVWRxwbQX9sUbsA.png align="left")

To recap, we explored Kubernetes Deployments, including their use cases, an NGINX example, and a practical task deploying a todo-app with auto-healing and auto-scaling on Day 32 of our #90daysofdevops journey.

Feel free to share your questions or experiences by leaving a comment. Stay tuned for more blogs and connect with me on LinkedIn for in-depth discussions. Your feedback and suggestions are invaluable; connect with me as [Mudit Mathur on LinkedIn](https://www.linkedin.com/in/mudit--mathur/). Let’s continue our DevOps journey together! #Day32 #90daysofdevops