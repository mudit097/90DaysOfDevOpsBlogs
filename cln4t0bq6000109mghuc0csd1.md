---
title: "Mastering ConfigMaps and Secrets in Kubernetes"
datePublished: Fri Sep 29 2023 16:13:48 GMT+0000 (Coordinated Universal Time)
cuid: cln4t0bq6000109mghuc0csd1
slug: mastering-configmaps-and-secrets-in-kubernetes
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696003961628/d4074555-263c-45ba-9376-10e908718924.jpeg
tags: aws, kubernetes, devops, 90daysofdevops, trainwithshubham

---

# **Define ConfigMaps**

* ConfigMaps in Kubernetes is a way to store configuration data as key-value pairs or plain text files, separate from the application code.
    
* ConfigMaps can be used to store environment variables, configuration files, command-line arguments, or any other configuration data required by an application.
    
* ConfigMaps can be created manually using the Kubernetes CLI or YAML files, or they can be generated automatically from configuration files or directories using the Kubernetes API.
    
* When a ConfigMap is created, it can be mounted as a volume or used as environment variables in a Pod. The data in the ConfigMap can be updated independently of the application code, allowing for dynamic configuration changes without redeploying the application.
    
* ConfigMaps are useful for managing the configuration of applications running in Kubernetes, particularly in microservices architectures where many small services may have their own unique configuration requirements.
    
* By centralizing configuration data in ConfigMaps, it becomes easier to manage and update configurations across multiple services, without the need for complex scripting or manual intervention.
    

# **Define Secrets in K8s**

* Secrets in Kubernetes are similar to ConfigMaps, in that they are used to store and manage sensitive information, such as passwords, API keys, and certificates.
    
* Secrets are designed specifically to keep this sensitive data secure, by encrypting it at rest and providing secure mechanisms for distributing and using the data.
    
* When a Secret is created, the data is stored in an encrypted format and can be mounted as a volume or used as environment variables in a Pod. The data is encrypted using a key that is managed by Kubernetes and is only accessible to authorized users or processes.
    
* Secrets are essential for managing sensitive information in Kubernetes, particularly in production environments where security is critical. By centralizing sensitive data in Secrets, it becomes easier to manage and update the data across multiple services, while ensuring that the data is kept secure at all times.
    

# **Set Up MySQL Client using ConfigMap & Secrets**

# **Task 1:**

Create a ConfigMap for your Deployment using a file or the command line.

vim configMap.yml

```plaintext
  kind: ConfigMap
  apiVersion: v1
  metadata:
    name: mysql-config
    labels:
      app: todo
  data:
    MYSQL_DB: "todo-db"
```

![](https://miro.medium.com/v2/resize:fit:875/1*asPEvP0QXDQJsbqWq0-zTw.png align="left")

Now apply the configMap.

```plaintext
  kubectl apply -f configMap.yml
```

![](https://miro.medium.com/v2/resize:fit:875/1*YTPW7yoELXqlD7nYpQWcig.png align="left")

Verify that the ConfigMap has been created by checking the status of the ConfigMaps in your Namespace.

The command shows the list of available configMap

```plaintext
  kubectl get configmap
```

![](https://miro.medium.com/v2/resize:fit:875/1*mObRA-FBRZQi0sbaUdsjlw.png align="left")

# **Task 2:**

* Create a Secret for your Deployment using a file or the command line vim secrect.yml
    

```plaintext
  apiVersion: v1
  kind: Secret
  metadata:
    name: mysql-secret
  type: Opaque
  data:
    password: dHJhaW53aXRoc2h1YmhhbQ==
```

![](https://miro.medium.com/v2/resize:fit:875/1*koYegvnR11MASOBMyoEjkg.png align="left")

We can Encode & decode the Base64 key by ourselves.

```plaintext
  # To Decode Base64 key
  echo "dHJhaW53aXRoc2h1YmhhbQ==" | base64 --decode

  # To Encode Base64 key
  echo "test@123" | base64
```

![](https://miro.medium.com/v2/resize:fit:875/1*tLaAhOBkirJ3ijpnEIWO8g.png align="left")

Now, apply the secret.

```plaintext
  kubectl apply -f secret.yml
```

![](https://miro.medium.com/v2/resize:fit:875/1*iYamYe57aLxTv5N05ICHYA.png align="left")

Verify that the Secret has been created by checking the status of the Secrets in your Namespace.

The command shows the list of available secrets

```plaintext
  kubectl get secrets
```

![](https://miro.medium.com/v2/resize:fit:875/1*wsXUV63hvdMDyMvOY4eEUQ.png align="left")

Now update the deployment.yml file to include the configMap & Secret

```plaintext
  apiVersion: apps/v1
  kind: Deployment
  metadata:
    name: mysql
    labels:
      app: mysql
  spec:
    replicas: 1
    selector:
      matchLabels:
        app: mysql
    template:
      metadata:
        labels:
          app: mysql
      spec:
        containers:
        - name: mysql
          image: mysql:8
          ports:
          - containerPort: 3306
          env:
          - name: MYSQL_ROOT_PASSWORD
            valueFrom:
              secretKeyRef:
                name: mysql-secret
                key: password
          - name: MYSQL_DATABASE
            valueFrom:
              configMapKeyRef:
                name: mysql-config
                key: MYSQL_DB
```

![](https://miro.medium.com/v2/resize:fit:875/1*GSTFGWkXuBng04HSFe1L0A.png align="left")

Apply the updated deployment using the command:

```plaintext
  kubectl apply -f deployment.yml
```

![](https://miro.medium.com/v2/resize:fit:875/1*4jDTDnuEkfwVQzkQeR27Ew.png align="left")

To verify the MySQL pods are running, we can get the MySQL pod by running the following command.

```plaintext
  kubectl get pods
```

![](https://miro.medium.com/v2/resize:fit:875/1*kNTEsNxGYqrsc6YEj-4zgg.png align="left")

To expose the MySQL use the K8s service, Create a service.yml file and make the configuration by headless service.

```plaintext
  apiVersion: v1
  kind: Service
  metadata:
    name: mysql-service
  spec:
    ports:
    - name: mysql
      port: 3306
    clusterIP: None
    selector:
      app: mysql
```

![](https://miro.medium.com/v2/resize:fit:875/1*btZYfIcXp1NbHsOz2JLEUg.png align="left")

Now apply for the service, so that the pod is exposed.

```plaintext
  kubectl apply -f service.yml
```

![](https://miro.medium.com/v2/resize:fit:875/1*PDy0J97Q_h66dOY2pqUi4g.png align="left")

Now on the Worker Node install the MySQL client on it.

```plaintext
  sudo apt install mysql-client-core-8.0
```

![](https://miro.medium.com/v2/resize:fit:875/1*aQuxN_c7G161Y_envt7ZVg.png align="left")

Now connect the MySQL to the Master node using the below command

```plaintext
  # Get inside of the mysql pod 
  kubectl exec -it mysql-b7f864b95-stmsw /bin/sh

  # Now connect the mysql using username root and password from Secret
  mysql -u root -p${MYSQL_ROOT_PASSWORD}
```

![](https://miro.medium.com/v2/resize:fit:875/1*uWhaKIN28QuWkM6YYtu5Qg.png align="left")

Now we are finally in MySQL console, so we can do CRUD operation in it. And use the todo-db that we had created before and that is listed in the databases.

In this blog, we delved into the world of Kubernetes and explored two essential concepts: ConfigMaps and Secrets. These are crucial for managing configuration data and sensitive information in your Kubernetes applications.

In Task 1, we defined ConfigMaps and discussed how to use them to store configuration data that can be injected into your pods. This is incredibly handy for maintaining flexibility in your deployments.

Task 2 introduced us to Secrets in Kubernetes, which are designed to securely store sensitive information like passwords and API keys. We learned how to create and manage Secrets to enhance the security of our applications.

But that’s not all! We also walked through the process of setting up a MySQL client using ConfigMaps and Secrets, demonstrating real-world application of these concepts.

If you’re eager to dive deeper into the world of DevOps and Kubernetes, stay tuned for more exciting blogs. I’m always eager to hear your questions, experiences, and suggestions, so please don’t hesitate to leave a comment below.

For further discussions and to keep up with the latest updates, connect with me on LinkedIn as [Mudit Mathur](https://www.linkedin.com/in/mudit--mathur/). Your feedback is invaluable as it helps me improve my content and provide you with more valuable insights.

Thank you for joining me on Day 35 of #90daysofdevops, and I look forward to sharing more knowledge with you in the days to come.