---
title: "Ansible Ad-Hoc Commands"
datePublished: Thu Oct 12 2023 21:11:01 GMT+0000 (Coordinated Universal Time)
cuid: clnnocm1w000208l3dzlm43u6
slug: ansible-ad-hoc-commands
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697144970243/98be0638-cf2c-432a-8ed5-5306be117df6.png
tags: blogging, aws, devops, 90daysofdevops, trainwithshubham

---

Ansible ad hoc commands are one-liners designed to achieve a very specific task. They are like quick snippets and your compact Swiss army knife when you want to do a quick task across multiple machines.

To put it simply, Ansible ad hoc commands are one-line Linux shell commands, and playbooks are like a shell script, a collective of many commands with logic.

# **What are Ansible Ad-hoc commands**

Ansible ad hoc commands are one-line commands used to perform simple tasks on remote systems without the need for complex playbooks. They allow you to execute specific modules on target hosts directly from the command line.

Ad hoc commands are particularly useful for quick tasks, troubleshooting, and one-time operations, providing flexibility and ease of use without the need for writing and maintaining a full playbook.

Ad hoc commands follow the syntax

```plaintext
ansible <host-pattern> -m <module> -a <arguments>

# If you’re using a custom SSH key to connect to the remote servers, 
# you can provide it at execution time with the --private-key

ansible <host-pattern> -m <module> -a <arguments> --private-key=~/.ssh/custom_id
```

* `<host-pattern>` specifies the target hosts or groups of hosts where the command should be executed.
    
* `<module>` refers to the Ansible module to be used for the task. Modules provide functionality for different operations like file manipulation, package management, user management, etc.
    
* `<arguments>` are optional arguments specific to the module, allowing customization and specifying the desired behavior.
    

# **Ad-hoc command to ping 3 servers from the inventory file**

```plaintext
# For selecting indivisual servers
ansible server1:server2:server3 -m ping

# For selecting all servers listed on inventory file
ansible all -m ping
```

![](https://miro.medium.com/v2/resize:fit:875/1*KUpnDXfm3JFIbwOmc79J8Q.png align="left")

# **Ad-hoc command to check system uptime**

```plaintext
ansible all -m command -a uptime
```

![](https://miro.medium.com/v2/resize:fit:875/1*4QgbyskHRz3CTpiaTY2Aag.png align="left")

# **Ad-hoc command to check the free memory or memory usage of hosts**

```plaintext
ansible all -a "free -m"
```

![](https://miro.medium.com/v2/resize:fit:875/1*LS73qgKwEyVXryf91hxlrg.png align="left")

# **Ad-hoc command to get physical memory allocated to the host**

```plaintext
 ansible all -m shell -a "cat /proc/meminfo|head -2"
```

![](https://miro.medium.com/v2/resize:fit:875/1*yQxBb9pwkajOuNdJKY1EhA.png align="left")

# **Ad-hoc command to check whether Nginx is installed on all the servers**

```plaintext
ansible all -b -m shell -a 'nginx -v'
```

![](https://miro.medium.com/v2/resize:fit:875/1*SJNCnVhy0UNOzNOIl3zASA.png align="left")

# **Ad-hoc command to check whether Docker is installed on all the servers**

```plaintext
ansible all -b -m shell -a 'docker --version'
```

![](https://miro.medium.com/v2/resize:fit:875/1*sFOAVtqS2KfGOZAk2yYZFQ.png align="left")

# **Ad-hoc command to check Python is installed on all the servers**

```plaintext
ansible all -b -m shell -a 'python --version'
```

![](https://miro.medium.com/v2/resize:fit:875/1*TNj_ciajExxe5SEofvImUg.png align="left")

In this blog, we’ve delved into the world of Ansible Ad-hoc commands, a powerful tool in the realm of infrastructure management. These commands offer a quick and efficient way to perform tasks and gather information across multiple servers. We explored a range of practical use cases, including:

\- Pinging three servers from the inventory file.  
\- Checking system uptime on hosts.  
\- Monitoring free memory or memory usage across hosts.  
\- Determining physical memory allocation for each host.  
\- Verifying the presence of Nginx and Docker on all servers.  
\- Checking for the installation of Python across all servers.

These Ansible Ad-hoc commands are invaluable for real-time system administration and maintenance. They empower you to swiftly collect data and perform tasks across your infrastructure. Your feedback is crucial to our growth, so don’t hesitate to connect with me on [LinkedIn at Mudit Mathur.](https://www.linkedin.com/in/mudit--mathur/)

Stay tuned for more DevOps insights and Ansible tips as we continue our journey. #Day56 #90daysofdevops