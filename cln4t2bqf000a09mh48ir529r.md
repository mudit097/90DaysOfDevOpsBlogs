---
title: "Managing Persistent Volumes in Deployment"
datePublished: Fri Sep 29 2023 16:15:21 GMT+0000 (Coordinated Universal Time)
cuid: cln4t2bqf000a09mh48ir529r
slug: managing-persistent-volumes-in-deployment
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696004053002/1a9a686b-eba9-4e31-b7a3-ecc0d53c2966.jpeg
tags: blogging, aws, devops, 90daysofdevops, trainwithshubham

---

# **Persistent Volumes (PV) in K8s**

* Persistent Volumes (PVs) are a mechanism to provide persistent storage for applications running in the cluster. PVs represent a piece of network-attached storage that is provisioned by the cluster administrator.
    
* A Persistent Volume is a cluster-level resource that decouples storage from individual pods or applications. It has a lifecycle independent of any specific pod and can be dynamically provisioned or statically created.
    
* PVs have configurable properties such as capacity, access modes (e.g., ReadWriteOnce, ReadOnlyMany, ReadWriteMany), and storage class (a way to dynamically provision PVs). They can be dynamically provisioned by storage providers, or manually created and managed by the cluster administrator.
    
* PVs can be backed by various storage types, including local storage, network-attached storage (NAS), cloud storage, or other external storage systems. They provide a persistent and reliable storage solution for applications, allowing data to persist even if the associated pod is deleted or rescheduled.
    

# **Persistent Volume Claim (PVC) in K8s**

* Persistent Volume Claim (PVC) is a resource that allows applications to request specific storage resources from available Persistent Volumes (PVs). PVCs act as a “claim” on a PV, specifying the desired storage capacity, access modes, and other requirements.
    
* When an application requires persistent storage, it creates a PVC with the desired characteristics. Kubernetes then matches the PVC with an appropriate PV based on the PVC’s specifications, such as storage capacity, access modes, and storage class.
    
* Once a PVC is bound to a PV, the PV becomes exclusively used by the application associated with the PVC. The application can then mount the PVC as a volume in its pods and use it for storing and retrieving data. The PVC provides a stable and portable way for the application to access the requested storage.
    

# **Benefits of having PV and PVC in k8s**

1. **Improved High Availability:** By using PVs and PVCs, applications can achieve high availability and fault tolerance. PVs can be backed by replicated storage systems, ensuring data redundancy and availability.
    
2. **Abstraction and Portability:** PVs and PVCs abstract the underlying storage details from applications. This allows applications to request and use storage resources in a standardized and portable manner.
    
3. **Ease of Scaling and Migration:** With PVs and PVCs, applications can easily scale by dynamically provisioning additional PVs or increasing the capacity of existing PVs.
    
4. **Data Persistence:** PVs and PVCs ensure that data persists even if a pod or application is terminated or rescheduled. The decoupling of storage from pods allows the data to be retained in the PV, ensuring data durability and availability.
    
5. **Resource Management:** PVs and PVCs provide better resource management by separating storage from applications. Administrators can define storage classes and allocate appropriate storage resources to different PVCs based on capacity, access modes, and other criteria.
    
6. **Dynamic Provisioning:** PVCs support dynamic provisioning, where the cluster automatically creates PVs to fulfill the storage requirements specified in the PVC. This enables on-demand storage allocation and eliminates the need for manual PV creation.
    
7. **Flexibility and Customization:** PVCs allow applications to request storage resources with a specific capacity, and access modes (e.g., ReadWriteOnce, ReadOnlyMany, ReadWriteMany). This flexibility enables applications to choose the appropriate storage characteristics that align with their needs, ensuring optimal performance, security, and data access patterns.
    

# **Task 1: Add a Persistent Volume to your Deployment todo app.**

Create a Persistent Volume using a file on your node.

vim pv.yml

```plaintext
  apiVersion: v1
  kind: PersistentVolume
  metadata:
    name: pv-todo-app
  spec:
    capacity:
      storage: 1Gi
    accessModes:
      - ReadWriteOnce
    persistentVolumeReclaimPolicy: Retain
    hostPath:
      path: "/tmp/data"
```

![](https://miro.medium.com/v2/resize:fit:875/1*gmdxEUUvgN30Zq4NFXaFGQ.png align="left")

Now apply the persistent volume.

```plaintext
  kubectl apply -f pv.yml
```

![](https://miro.medium.com/v2/resize:fit:875/1*m7gM9rVa95c-SYUqP0PNNQ.png align="left")

Create a Persistent Volume Claim that references the Persistent Volume.

vim pvc.yml

```plaintext
  apiVersion: v1
  kind: PersistentVolumeClaim
  metadata:
    name: pvc-todo-app
  spec:
    accessModes:
      - ReadWriteOnce
    resources:
      requests:
        storage: 500Mi
```

![](https://miro.medium.com/v2/resize:fit:875/1*0cD2GNa_-Pmcfa0byBb-eA.png align="left")

Now apply the Persistent Volume Claim by using following command.

```plaintext
  kubectl apply -f pvc.yml
```

![](https://miro.medium.com/v2/resize:fit:875/1*WLwiBZ7HhuIWnHvVuZWcRA.png align="left")

Update your deployment.yml file to include the Persistent Volume Claim. After Applying pv.yml pvc.yml to your deployment file.

```plaintext
  apiVersion: apps/v1
  kind: Deployment
  metadata:
    name: todo-app-deployment
  spec:
    replicas: 1
    selector:
      matchLabels:
        app: todo-app
    template:
      metadata:
        labels:
          app: todo-app
      spec:
        containers:
          - name: todo-app
            image: mudit097/django-todo
            ports:
              - containerPort: 8000
            volumeMounts:
              - name: todo-app-data
                mountPath: /app
        volumes:
          - name: todo-app-data
            persistentVolumeClaim:
              claimName: pvc-todo-app
```

![](https://miro.medium.com/v2/resize:fit:875/1*a3S9DXUkwBA4zJkTfT3FkA.png align="left")

Apply the updated deployment using the command:

```plaintext
  kubectl apply -f deployment.yml
```

![](https://miro.medium.com/v2/resize:fit:875/1*OsOn1EtpGTuHRc4Io0UdoA.png align="left")

Verify that the Persistent Volume has been added to your Deployment by checking the status of the Pods and Persistent Volumes in your cluster. Use this commands `kubectl get pods` ,`kubectl get pv`

```plaintext
  # Getting details of Persistent Volume
  kubectl get pv

  # Getting details of Persistent Volume Claim
  kubectl get pvc

  # Getting the pvc details of the application
  kubectl describe pvc pvc-todo-app
```

![](https://miro.medium.com/v2/resize:fit:875/1*IWsMl1IlLBg4Sud9PktYCw.png align="left")

# **Task 2: Accessing data in the Persistent Volume,**

* Connect to a Pod in your Deployment using the command :
    
* `kubectl exec -it -- /bin/bash`
    
* Verify that you can access the data stored in the Persistent Volume from within the Pod by creating a file inside the `/app` directory on the worker node using the following command:
    

![](https://miro.medium.com/v2/resize:fit:875/1*SPFrF6apLlQ2YmtFNYVsCA.png align="left")

```plaintext
  # Getting the pods details
  kubectl get pods

  # Get into one of the pod
  kubectl exec -it <pod-name> /bin/bash

  # Now change dir to /app
  cd /app/

  # Create a file test.txt and put some content into it
  echo "Hello" > /app/test.txt

  # Verify the file is present in the dir or not.
  ls
```

![](https://miro.medium.com/v2/resize:fit:875/1*AapOTQMuNLfGSwCtUWjZ9w.png align="left")

Now, delete that pod where we create a file. By deleting the deployment of pod and checking if the file in the new pod is created after applying the deployment again in the server.

```plaintext
  # Checking total pods
  kubectl get pods

  # Deleting the existing pod
  kubectl delete pod <pod-name>
```

![](https://miro.medium.com/v2/resize:fit:875/1*e7QBNIOpkSjQn_JhVGrcYg.png align="left")

As Auto healing is there, a new pod is generated after the old pod is deleted. Aand verify the file you have created on the worker node:

![](https://miro.medium.com/v2/resize:fit:875/1*ZbgVLJC6IkDPFJFE9HdX7A.png align="left")

```plaintext
  #Get the docker container name of newly created pod
  docker ps

  # Now get into the newly cretaed pod
  docker exec -it <pod-name> /bin/bash

  # Then change dir to /app
  cd /app/

  # List down all the file, and we can see the file we create before is present
  ls

  # Now Read the existing file. And we had the same file and file content is also same.
  cat test.txt
```

![](https://miro.medium.com/v2/resize:fit:875/1*e9LsUtLFgJF5sDOorV-3pQ.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*D6MPDWVHOwzRjG77JSBOzw.png align="left")

In this Blog, we’ve embarked on an enlightening journey through the realm of Kubernetes (K8s) Persistent Volumes (PV) and Persistent Volume Claims (PVC). We’ve unraveled the significance and benefits of harnessing PVs and PVCs within your K8s environment to seamlessly manage data persistence.

Our voyage didn’t stop at theory; we dived into practicality with two essential tasks. Task 1 guided us in the process of integrating a Persistent Volume into our todo app Deployment. Task 2 equipped us with the know-how to efficiently access data stored within these Persistent Volumes.

Your voice matters in this learning community. Whether you seek answers to burning questions or wish to share your personal experiences with PVs and PVCs in K8s, we encourage you to leave a comment below.

As our journey continues, stay tuned for more captivating insights in our ongoing #90daysofdevops series. For in-depth discussions and real-time updates, connect with me on [LinkedIn as Mudit Mathur.](https://www.linkedin.com/in/mudit--mathur/)

Your feedback and suggestions are the driving force behind our content improvement. Please feel free to reach out through [LinkedIn](https://www.linkedin.com/in/mudit--mathur/) or other channels to share your thoughts.

Thank you for being a vital part of our DevOps community, and here’s to our collective growth and enlightenment on #Day36 of #90daysofdevops!