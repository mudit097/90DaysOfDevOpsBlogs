---
title: "Launching your First Kubernetes Cluster with Nginx running"
datePublished: Thu Sep 28 2023 20:11:09 GMT+0000 (Coordinated Universal Time)
cuid: cln3m1pce000n0ammaxdt9nhb
slug: launching-your-first-kubernetes-cluster-with-nginx-running
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1695927999572/097c1dec-3281-4c0e-bb4c-d0a812da4a4f.jpeg
tags: aws, kubernetes, devops, 90daysofdevops, trainwithshubham

---

## **What is minikube?**

* Minikube is a tool that quickly sets up a local Kubernetes cluster on macOS, Linux, and Windows. It can deploy as a VM, a container, or on bare metal.
    
* Minikube is a pared-down version of Kubernetes that gives you all the benefits of Kubernetes with a lot less effort.
    
* This makes it an interesting option for users who are new to containers, and also for projects in the world of edge computing and the Internet of Things.
    

## **Features of minikube**

1. Supports the latest Kubernetes release (+6 previous minor versions)
    
2. Cross-platform (Linux, macOS, Windows)
    
3. Deploy as a VM, a container, or on bare-metal
    
4. Multiple container runtimes (CRI-O, containerd, docker)
    
5. Direct API endpoint for blazing-fast image load and build
    
6. Advanced features such as LoadBalancer, filesystem mounts, FeatureGates, and network policy
    
7. Addons for easily installed Kubernetes applications
    
8. Supports common CI environments.
    

## **Define Pod**

* Pods are the smallest deployable units of computing that you can create and manage in Kubernetes.
    
* A Pod (as in a pod of whales or pea pod) is a group of one or more containers, with shared storage and network resources, and a specification for how to run the containers.
    
* A Pod's contents are always co-located and co-scheduled, and run in a shared context. A Pod models an application-specific "logical host": it contains one or more application containers that are relatively tightly coupled.
    

## **Types of Installation of K8s**

1. Mini Kube (Docker Inside Docker DIND) → least use in Prod → Easiest
    
2. Kubeadm :→ Baremetal (open-source tool) → Used in Prod → Intermediate
    
3. Managed K8s Cluster
    
    AWS → EKS (Elastic Cloud Kubernetes)
    
    Azure → AKS (Azure Kubernetes Service)
    
    GCP → GKE (Google Kubernetes Engine)
    
4. KIND (Kubernetes in Docker)
    

## **Task 1: Install minikube on your local**

1. Create a new VM instance having 2 CPUs, 4GB of free memory, 20 GB of free disk space.
    
    When creating a new EC2 instance select t2.medium.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695928580455/d6484976-41c5-4675-8f7a-0656ce3f4238.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695928609297/24a8a54a-32dd-403c-b5e1-57e626827622.png align="center")
    
2. Install Docker in your system.
    
    ```plaintext
     sudo apt update -y
     sudo apt install docker.io -y
    
     sudo systemctl start docker
     sudo systemctl enable docker
     sudo systemctl status docker
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695928691447/83b642ee-04eb-4f27-bcce-f96546b3ff4f.png align="center")
    
    Add the user to the docker group
    
    ```plaintext
     sudo usermod -aG docker $USER && newgrp docker
    ```
    
3. Install Minikube in system.
    
    ```plaintext
     curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
    
     sudo install minikube-linux-amd64 /usr/local/bin/minikube
    ```
    
4. And then install Kubelet.
    
    ```plaintext
     sudo snap install kubectl --classic
    ```
    
5. Start Minikube as per the image and check Minikube status
    
    ```plaintext
     minikube start --driver=docker
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695928904500/7b7c9737-d4ed-4def-8343-c79e397e8507.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695928941465/e202e7b4-5478-4879-bf5a-d1bdefd17b27.png align="center")
    
6. Check if minikube cluster has been set up successfully or not by checking pods or namespace status.
    
    ```plaintext
     kubectl get pods
    
     kubectl get namespace
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695928977113/d2f429c0-be7b-4e50-a858-40174aa4b6ee.png align="center")
    

## **Task 2: Create your first pod on Kubernetes through minikube.**

1. To create a pod, we have to write a YAML file which is a.k.a Manifest file. So to create a pod for NGINX we have to pass the values & attributes in key-value format.
    
    In the manifest file, we are passing values:
    
    apiVersion → Kubernetes Version
    
    Kind → Type of deployment
    
    metadata → More Details about pod
    
    container → Details of containers in object
    
    containerPort → The port where the pod will deploy
    
    ```plaintext
     apiVersion: v1
     kind: Pod
     metadata:
       name: nginx
     spec:
       containers:
       - name: nginx
         image: nginx:1.14.2
         ports:
         - containerPort: 80
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695929304498/e5b1c324-21ec-4605-ac63-aab12b9a9baf.png align="center")
    
2. Run the kubectl command to create a pod.
    
    ```plaintext
     kubectl apply -f pod.yml
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695929350912/d4f012b6-1fe9-47a3-9730-2156d372a46c.png align="center")
    
3. Check the pod's status by kubectl get pods, you can see a NGINX pod is created successfully by it's status
    
    ```plaintext
     kubectl get pods
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695929395799/e5b95719-b3de-4185-8eea-fdb895558935.png align="center")
    
4. Run the **<mark>kubectl get pods -o wide</mark>** command to get more detailed information about the pod-like IP, node, age of node, and status.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695929431313/f8dc95af-9fb9-4aa0-a186-aa8e305064c2.png align="center")
    
5. To check if nginx is running locally or not, do we have to ssh the minikube go inside the minikube cluster. Then curl the IP address of the pod.
    
    ```plaintext
     #Get the IP
     kubectl get pods -o wide
    
     # SSH into minikube
     minikube ssh
    
     # Curl the IP address to access the NGINX
     curl http://<IP-Addr>
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695929495100/ebb08d83-6b27-482d-aed1-6385c7ff9acf.png align="center")
    

# **Task 3: Create NGINX pod on K8s through Kubeadm**

1. Create 2 VM instances for Master and Node.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695929799858/618e3953-4325-4cac-ae47-3e71d5325f00.png align="center")
    
2. Install Docker on both Master & Node
    
    ```plaintext
     sudo apt update -y
     sudo apt install docker.io -y
    
     sudo systemctl start docker
     sudo systemctl enable docker
     sudo systemctl status docker
    ```
    
3. Install Kebeadm on both master and node.
    
    ```plaintext
     sudo curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg
    
     echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
    ```
    
4. Again update the system.
    
    ```plaintext
     sudo apt update -y
    ```
    
5. Install Kubeadm,Kubectl and Kebelet in both Master and Node.
    
    ```plaintext
     sudo apt install kubeadm=1.20.0-00 kubectl=1.20.0-00 kubelet=1.20.0-00 -y
    ```
    
6. Connect Master with Node:
    
    Initialized Kubeadm:
    
    Run the following command only on Master:
    
    ```plaintext
     sudo su
     kubeadm init
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695930018533/749eb190-8d22-4618-9d3b-d4b4d3ca2312.png align="center")
    
7. Setup the kubeconfig for the current user
    
    ```plaintext
     mkdir -p $HOME/.kube
     sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
     sudo chown $(id -u):$(id -g) $HOME/.kube/config
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695930079434/472be8a1-a8ff-4dda-8182-100e4cd7f3ec.png align="center")
    
8. Finish the Master Setup using the following Command:
    
    ```plaintext
     kubectl apply -f https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695930146899/61adcf9d-4e9d-4a12-a548-3cddae606536.png align="center")
    
9. Now create a token to join the Master & Node connection
    
    ```plaintext
     kubeadm token create --print-join-command
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695930227915/4f6ba662-6440-4d90-8d4d-99d628afb434.png align="center")
    
10. We will get nodes for master
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695930516385/083eeab9-525e-4c68-a38f-20bfed1e1994.png align="center")
    
11. After that open port 6443 in master
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695930555929/1b9e052b-4559-4796-97f5-da527ab4a971.png align="center")
    
12. Then on the <mark>Worker Node </mark> reset the checks so it can't assign as Master.
    
    ```plaintext
    sudo su
    kubeadm reset pre-flight checks
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695930620159/f1ba007f-114f-43b2-b521-78677362a7b3.png align="center")
    
13. Paste the Join command on the worker node and append --v=5 at the end
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695930688687/42113cc6-3d0a-4d63-b947-16192e244337.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695930708489/43817ce2-7083-4c43-8a74-ac406075eb5a.png align="center")
    
14. Verify by running the command in Master:
    
    ```plaintext
    kubectl gets nodes
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695930754254/fbd1b08c-7431-471c-854f-de4eada152c9.png align="center")
    
    [**<mark>Kubeadm Installation Step</mark>**](https://github.com/RishikeshOps/Scripts/blob/main/k8sss.sh)
    

### **Create the Nginx Pod**

1. By default, the kubectl run command creates a deployment and a replica set along with the pod. If you only want to create a pod without creating a deployment or replica set, you can use the --restart=Never flag.
    
2. But if you pass --restart=Always, if your pod is deleted or having an issue, then a new pod will be replaced immediately.
    
    ```plaintext
     kubectl run nginx --image=nginx --restart=Never
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695930928613/878aa861-c7ca-411d-928e-a742ba0ba45c.png align="center")
    
3. Now we can see the docker container in the worker node
    
    ```plaintext
     docker ps
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684066430172/f0369a70-3a27-478c-821a-a1db72c38693.png?auto=compress,format&format=webp align="left")
    
4. To check if the pods are running or not
    
    ```plaintext
     kubectl get pods
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695931347947/4deef882-daf4-41b8-beb8-bbab22073834.png align="center")
    
5. Get the details of the pod
    
    ```plaintext
     kubectl get pods -o wide
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695931395396/7a4cae68-b140-40c7-8153-67d931e89dfb.png align="center")
    
6. To delete a pod in
    
    ```plaintext
     # kubectl delete pod  <pod-name>
     kubectl delete pod nginx
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1695931456270/f4f0858e-8718-47dd-bdda-30e2ec168dff.png align="center")
    

In this blog, we explored setting up a Kubernetes cluster using Minikube and creating a pod within it. If you have questions or want to share your experiences, please leave a comment below. Stay tuned for more blogs and connect with me on LinkedIn for further discussions.

I'm always open to feedback and suggestions for improving my content. You can find me on LinkedIn as [Mudit Mathur](https://www.linkedin.com/in/mudit--mathur/). Feel free to reach out with your thoughts.

#Day31 #90daysofdevops