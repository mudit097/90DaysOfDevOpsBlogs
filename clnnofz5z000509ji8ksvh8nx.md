---
title: "Ansible Tutorial for DevOps Engineers"
datePublished: Thu Oct 12 2023 21:13:37 GMT+0000 (Coordinated Universal Time)
cuid: clnnofz5z000509ji8ksvh8nx
slug: ansible-tutorial-for-devops-engineers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697145144109/0c965c38-0f17-45fd-a629-7bec6d47b453.webp
tags: aws, ansible, devops, 90daysofdevops, trainwithshubham

---

**What is ansible ?**

It is a configuration management tool , open source .

Uses YAML scripting .

Works on push management .

**Required architecture :**

We need to create 1 master node and 3 server nodes

![](https://miro.medium.com/v2/resize:fit:875/0*xFxhTGybO2K5x8mP.png align="left")

**Create an instance ,**

Instance name : ansible\_master

![](https://miro.medium.com/v2/resize:fit:875/0*lx-tIUIDzW4PB9pO.png align="left")

Select ubuntu server 22.04 as amazon machine image .

![](https://miro.medium.com/v2/resize:fit:875/0*pkmwN2VAprp6jTw7.png align="left")

Allocate port — 22

![](https://miro.medium.com/v2/resize:fit:875/0*44bHpg9Cupf7yh8Z.png align="left")

Launch the instance ,

![](https://miro.medium.com/v2/resize:fit:875/0*RyOrpcvielNspa7F.png align="left")

we have launched 1 master node , we need 3 server nodes

select the instance &gt; actions &gt; image and templates &gt; launch more like these

![](https://miro.medium.com/v2/resize:fit:875/0*rvY9Hvj0MYA1IVk2.png align="left")

Launch 3 instances with the same configurations ,

And launch instance

![](https://miro.medium.com/v2/resize:fit:875/0*RuyFsX3af6npVzuo.png align="left")

Change the name of the 3 — instances ,

![](https://miro.medium.com/v2/resize:fit:875/0*CeuHF-9m-QKC8KV4.png align="left")

Connect to the ansible master instance ,

Click on the instance &gt; connect

![](https://miro.medium.com/v2/resize:fit:875/0*qG2ek1mjG0eMO7XA.png align="left")

Use command ,

**sudo apt update**

![](https://miro.medium.com/v2/resize:fit:875/0*pLhsVOBQK1I8vsp2.png align="left")

Now install ansible ,

![](https://miro.medium.com/v2/resize:fit:875/0*PppBdTjTjlXQ8aW-.png align="left")

After configuring the master , we need to ssh with the nodes (node 1 , node 2, node 3)

Now lets connect with ansible\_server\_2 ,

![](https://miro.medium.com/v2/resize:fit:875/0*BLrk8-UO3mhaX58G.png align="left")

Go to the master server ,

use command

**ssh-keygen** to generate id\_rsa.pub

![](https://miro.medium.com/v2/resize:fit:875/0*lGBs8L2O-RzusBFG.png align="left")

Copy the key from id\_rsa.pub

![](https://miro.medium.com/v2/resize:fit:875/0*PbM-ZsGgabko2pRq.png align="left")

Now go to the ansible *server*2 instance ,

Go to .ssh &gt; authorized\_keys

![](https://miro.medium.com/v2/resize:fit:875/0*I1zzcCwisDmU9NEx.png align="left")

And paste the public key here ,

![](https://miro.medium.com/v2/resize:fit:875/0*x4d2Y7nh1fV6nw5U.png align="left")

Save and exit.

Do the same for ansible\_server\_1 and ansible\_server\_3 ,

![](https://miro.medium.com/v2/resize:fit:875/0*11Y9PR1ThXugl93X.png align="left")

Copy and paste the key from id\_rsa.pub(ansible\_master) — authorized\_keys (ansible\_server\_1)

![](https://miro.medium.com/v2/resize:fit:875/0*SmYnJ6XWovI2J3tv.png align="left")

Copy and paste the key from id\_rsa.pub(ansible\_master) — authorized\_keys (ansible\_server\_3)

Now go to the ansible\_master

Use the command ,

**ssh** [**ubuntu@52.221.219.146**](mailto:ubuntu@52.221.219.146) (public ip address of ansible\_server\_2)

![](https://miro.medium.com/v2/resize:fit:875/0*cHhZ8j8OCjN1vYxG.png align="left")

Now we have connected from one server to another server , this is called secured shell (ssh).

Now we have to create an inventory file ,

![](https://miro.medium.com/v2/resize:fit:875/0*q6U8CUv6GkJ3tzrD.png align="left")

Go to ansible and create hosts ,

**vim hosts**

![](https://miro.medium.com/v2/resize:fit:875/0*uirBurU95hPMUdFH.png align="left")

Now add the servers inside the inventory ,

![](https://miro.medium.com/v2/resize:fit:875/0*zdN62DX0ICTuGk5y.png align="left")

Now the servers are ready in the inventory .

To install python by default in all the servers ,

![](https://miro.medium.com/v2/resize:fit:875/0*TaZ4CCcHl6Co1XSH.png align="left")

Save and exit .

Now lets check if the inventory / host file is correct ,

**ansible-inventory — list -y**

![](https://miro.medium.com/v2/resize:fit:875/0*ODtogBVzMXp2T4ar.png align="left")

We get this error because our host file is in different directory ,

**/home/ubuntu/ansible**

![](https://miro.medium.com/v2/resize:fit:875/0*IRP3YtrKqQTvbwVT.png align="left")

Use the command ,

**ansible-inventory — list -y -i /home/ubuntu/ansible/hosts**

![](https://miro.medium.com/v2/resize:fit:875/0*HzUjsvzMdKKP_831.png align="left")

we have got all the details of the server .

Now lets ping all the servers with a module .

**What is module ?**

module is a command or set of commands to be executed on client side .

**ansible all -m ping -i /home/ubuntu/ansible/hosts**

![](https://miro.medium.com/v2/resize:fit:875/0*thoPESkDznBQeoXq.png align="left")

Now to check memory usage ,

**ansible all -a “free -h” -i /home/ubuntu/ansible/hosts**

![](https://miro.medium.com/v2/resize:fit:875/0*7qdbop8DXxdgVPK2.png align="left")

To check server uptime ,

**ansible servers -a “uptime” -i /home/ubuntu/ansible/hosts**

![](https://miro.medium.com/v2/resize:fit:875/0*t1Of73_iE9SYNC4J.png align="left")

**If this post was helpful, please do follow and click the clap 👏 button below to show your support 😄**

**\- Thank you for reading 💚**

**\-Mudit Mathur🌻✨**