---
title: "Working with Services in Kubernetes"
datePublished: Fri Sep 29 2023 16:12:20 GMT+0000 (Coordinated Universal Time)
cuid: cln4syfxj000108l71dhccq2d
slug: working-with-services-in-kubernetes
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696003881556/f9141028-200a-47b5-add4-4a2377d2a634.jpeg
tags: blogging, aws, kubernetes, devops, trainwithshubham

---

# **Task 1:Create a Service for accessing todo-app**

1. Create a Service for your todo-app Deployment from Day-32
    

Create a Service definition for your todo-app Deployment in a YAML file.

Now create a service.yml where we will deploy NodePort.

```plaintext
 apiVersion: v1
 kind: Service
 metadata:
   name: my-django-app-service
   namespace: my-django-app
 spec:
   type: NodePort
   selector:
     app: django-app
   ports:
       # By default and for convenience, the 'targetPort' is set to the same value as the 'port' field.
     - port: 80
       targetPort: 8000
       # Optional field
       # By default and for convenience, the Kubernetes control plane will allocate a port from a range (default: 30000-32767)
       nodePort: 30009
```

![](https://miro.medium.com/v2/resize:fit:875/1*AYEWK0JVyehqErFbFeGVWw.png align="left")

2\. Apply the Service definition to your K8 cluster using the kubectl apply -f service.yml.

```plaintext
 kubectl apply -f service.yml

 # Getting the service. (svc is short form of service)
 kubectl get svc -n=my-django-app
```

![](https://miro.medium.com/v2/resize:fit:875/1*N4d2DhLA5Od3B6Q138PgZw.png align="left")

3\. So edit the inbound rule of the worker node and add port number 30009 so that we can access the pod outside

![](https://miro.medium.com/v2/resize:fit:875/1*wtI9w8PtJJDOaOn5yzThag.png align="left")

4\. Verify that the Service is working by accessing the todo-app using the Service’s IP and Port in your Namespace.

![](https://miro.medium.com/v2/resize:fit:875/1*bjPxSTk-YQuvnjKoYK1Iug.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*Mq9-QBdqOLrvMmwjOHQTdg.png align="left")

# **Task 2:Create a ClusterIP Service for accessing the todo-app**

1. Create a ClusterIP Service for accessing the todo-app from within the cluster
    

```plaintext
 vim cluster-ip-service.yml
```

```plaintext
 apiVersion: v1
 kind: Service
 metadata:
   name: my-django-app-cluster
   namespace: my-django-app
 spec:
   type: ClusterIP
   selector:
     app: django-app
   ports:
     - name: http
       protocol: TCP
       port: 8000
       targetPort: 8000
```

![](https://miro.medium.com/v2/resize:fit:875/1*lN9wfIo7rbWMfJAu-SSSlA.png align="left")

2\. Apply the Service definition to the cluster using the following command:

```plaintext
 kubectl apply -f cluster-ip-service.yml -n my-django-app
```

3\. Verify that the service is running by running the following command:

```plaintext
 kubectl get svc -n my-django-app
```

![](https://miro.medium.com/v2/resize:fit:875/1*ion1I9alDy9uefZY4SSOtg.png align="left")

4\. Deploy another Pod in the my-django-app namespace to test the service. You can use the following YAML definition to create a simple test Pod:

```plaintext
 apiVersion: v1
 kind: Pod
 metadata:
   name: test-pod
   namespace: my-django-app
 spec:
   containers:
   - name: busybox
     image: busybox
     command: ['sh', '-c', 'while true; do wget -q -O- my-django-app-cluster-ip:8000; done']
```

![](https://miro.medium.com/v2/resize:fit:875/1*qAdjIu20PVEF5N4bcOUX7w.png align="left")

5\. Apply the Pod definition using the following command:

```plaintext
 kubectl apply -f test-pod.yml -n my-django-app
```

![](https://miro.medium.com/v2/resize:fit:875/1*K1XFkM6_ihq8limRyPoXnw.png align="left")

6\. Now enter into this pod :

```plaintext
 kubectl exec -it test-pod -n my-django-app -- /bin/sh
```

![](https://miro.medium.com/v2/resize:fit:875/1*JSYZjlujCllVWnVh8-Glag.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*2X2-gk-sGK7WJX8x2_7zzQ.png align="left")

7\. Test Todo app

```plaintext
 # Inside the test pod execute the wget commad.
 wget -qO- http://<ip-of-my-django-app-cluster-ip>:<port

 # wget -qO- http://10.96.146.9:8000
```

Now you successfully Access it through another Port:

![](https://miro.medium.com/v2/resize:fit:875/1*4d1VVAxenVEMiGhxKz6LXA.png align="left")

# **Task 3:Create a LoadBalancer Service for accessing the todo-app**

1. Create a YAML file named load-balancer-service.yml with the following contents:
    

```plaintext
 apiVersion: v1
 kind: Service
 metadata:
   name: my-django-app-cluster-ip
   namespace: my-django-app
 spec:
   selector:
     app: django-app
   ports:
     - port: 80
       targetPort: 8000
   type: LoadBalancer
```

![](https://miro.medium.com/v2/resize:fit:875/1*26ZkshCX4-Xor8kvVN9Skw.png align="left")

2\. Apply the LoadBalancer Service definition to your K8s cluster using the following command:

```plaintext
 kubectl apply -f load-balancer-service.yml -n my-django-app
```

![](https://miro.medium.com/v2/resize:fit:875/1*mjFC9HuI4Q2Rp8h0qyJs9Q.png align="left")

3\. Verify that the LoadBalancer Service is working by accessing the todo-app from outside the cluster in your namespace.

```plaintext
 kubectl get service -n=my-django-app
```

![](https://miro.medium.com/v2/resize:fit:875/1*RUxmSZ4CjmWdBzwi2NDFFw.png align="left")

4\. Get the IP from the service and then open the port in the Worker Node.

![](https://miro.medium.com/v2/resize:fit:875/1*LheP2LZZDGhPXjRtLf2AOw.png align="left")

5\. copy the Public IPv4 DNS and access through the browser by providing the port number in the URL

```plaintext
 Public-IPv4-DNS:<loadbalancer-port-number>
```

![](https://miro.medium.com/v2/resize:fit:875/1*g7Kmqv5bd3oe184t3L9HkQ.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*d3kYGZAshzB8uUi6J6ut0Q.png align="left")

In this blog, we embarked on a journey through the world of Kubernetes services, tackling three essential tasks along the way. First, we created a service to access our todo-app, highlighting the significance of service abstraction in Kubernetes. Next, we delved deeper by setting up a ClusterIP service, optimizing internal communication within our application. Lastly, we explored the power of LoadBalancer services, ensuring seamless external access to our todo-app.

As we continue our DevOps adventure, remember that these tasks serve as building blocks for crafting robust and accessible applications within Kubernetes clusters. The ability to create and configure services is a crucial skill in modern container orchestration.

If you have questions or wish to share your experiences, please don’t hesitate to leave a comment below. Stay tuned for more insightful blogs as we delve deeper into the world of DevOps. And remember, you can always connect with me on LinkedIn as [Mudit Mathur](https://www.linkedin.com/in/mudit--mathur/). Your feedback and suggestions are highly valued, so feel free to reach out with your thoughts.

#Day34 #90daysofdevops