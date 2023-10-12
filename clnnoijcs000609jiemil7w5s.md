---
title: "Day 57 Ansible Playbook"
datePublished: Thu Oct 12 2023 21:15:37 GMT+0000 (Coordinated Universal Time)
cuid: clnnoijcs000609jiemil7w5s
slug: day-57-ansible-playbook
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697145259667/23a499dc-29fe-4ea7-a04f-b2648f14daac.png
tags: aws, devops, iac, 90daysofdevops, trainwithshubham

---

Welcome to the world of Ansible Playbooks — your gateway to streamlined and efficient automation. In this blog, we’ll introduce you to Ansible Playbooks, their powerful features, and guide you on how to harness their potential for simplifying your infrastructure management. Whether you’re an experienced administrator or new to automation, this guide will empower you to take control of your IT tasks with ease. Let’s dive in!

# **What is Ansible Playbook**

* An Ansible playbook is a configuration file written in YAML format that defines a set of tasks and configurations to be executed on remote systems.
    
* Playbooks provide a way to automate complex workflows and orchestrate multiple tasks. They can include variables, conditionals, loops, and more, enabling flexible and reusable automation.
    
* Ansible Playbook organizes the steps between the assembled machines or servers and gets them organized and running in the way the users need them to.
    
* Playbooks are the core building blocks of Ansible and allow for the definition of desired system states, making configuration management and application deployment consistent and repeatable.
    

![](https://miro.medium.com/v2/resize:fit:875/0*J-iN2UB1nYKCpau- align="left")

# **Key Features of Ansible Playbooks**

1. Declarative Syntax: Ansible playbooks use a simple YAML-based syntax, making them easy to read, write, and understand.
    
2. Task Orchestration: Playbooks allow you to define a sequence of tasks to be executed in a specific order, ensuring a consistent and controlled workflow.
    
3. Idempotence: Playbooks are designed to be idempotent, meaning they can be run multiple times without causing unintended changes. This ensures a predictable and reliable deployment process.
    
4. Variables and Templating: Playbooks support the use of variables and Jinja2 templating, enabling dynamic and customizable configurations.
    
5. Conditionals and Loops: Ansible playbooks offer conditionals and loop structures, allowing you to control task execution based on specific conditions or iterate over lists of values.
    
6. Error Handling and Logging: Playbooks provide mechanisms for handling errors gracefully and capturing detailed logs, aiding in troubleshooting and debugging.
    
7. Reusability and Modularity: Playbooks can be modularized into roles, allowing for the reuse of tasks across multiple projects, and promoting code organization and maintainability.
    

# **How to write Ansible Playbook**

# **\- Inventory**

Define the inventory file that lists the target hosts or groups where the playbook will be executed. Ensure the inventory is well-organized and up to date.

# **\- Playbook Structure**

Organize your playbook into plays, which are units of work targeting specific hosts or groups. Each play consists of a set of tasks to be executed.

```plaintext
- name: Deploy Web Application
  hosts: web_servers
  become: true
  tasks:
    # Defined Task
```

# **\- Tasks**

Define tasks within plays to specify the actions to be performed on the target hosts. Tasks should be atomic, idempotent, and focused on achieving a specific outcome.

```plaintext
tasks:
  - name: Install required packages
    apt:
      name: ['apache2', 'php', 'mysql']
      state: present
```

# **\- Variables and Templating**

Use variables to make playbooks flexible and reusable. Define variables in separate files or inventories and use Jinja2 templating for dynamic values.

```plaintext
vars:
  app_name: MyWebApp
  app_port: 8080

tasks:
  - name: Configure Apache VirtualHost
    template:
      src: templates/virtualhost.conf.j2
      dest: /etc/apache2/sites-available/{{ app_name }}.conf
```

# **\- Handlers**

Define handlers for tasks that need to be triggered conditionally. Handlers are actions that run only when notified by tasks and are typically used for service restarts or configuration reloads.

```plaintext
tasks:
  - name: Restart Apache service
    service:
      name: apache2
      state: restarted
    notify: Reload Apache Configuration

handlers:
  - name: Reload Apache Configuration
    service:
      name: apache2
      state: reloaded
```

# **\- Conditionals and Loops**

Utilize conditionals and loops to make playbooks more dynamic and adaptable. For example, conditionally execute a task based on the presence of a file.

```plaintext
tasks:
  - name: Copy configuration file if it doesn't exist
    copy:
      src: files/config.conf
      dest: /etc/app/config.conf
    when: not ansible_check_mode and not ansible_file_exists|bool
```

# **\- Error Handling and Logging**

Implement error-handling mechanisms to handle failures gracefully. Use the `failed_when` parameter to specify conditions that indicate task failure.

```plaintext
tasks:
  - name: Ensure required packages are installed
    apt:
      name: ['package1', 'package2']
      state: present
    failed_when: "'unable to locate' in result.msg"
```

# **Task 1: File Creation Ansible playbook**

* Add all the server details in the inventory file.
    

![](https://miro.medium.com/v2/resize:fit:875/1*VNoTdPnLmcaeMRbf2JJx9w.png align="left")

* Create an Ansible playbook to create a file on a different server
    

```plaintext
  - name: A playbook to create a file 
    hosts: all
    become: true
    tasks:
    - name: Create a file
      file:
       path: /home/ubuntu/testfile.txt
       state: touch
```

![](https://miro.medium.com/v2/resize:fit:875/1*bY-AUTRHqdXh_t-dgwBRaw.png align="left")

* Now to run this playbook use the command `ansible-playbook` including the filename.
    

```plaintext
  ansible-playbook create_file.yml
```

![](https://miro.medium.com/v2/resize:fit:875/1*-y_JmJDEKWas5pHqD7TG5g.png align="left")

* Once the execution is finished, verify that the file has been created on different servers using the following command.
    

```plaintext
  ansible all -a "ls /home/ubuntu"
```

![](https://miro.medium.com/v2/resize:fit:875/1*rf2ihfYgRuf_fRaMRZDX9Q.png align="left")

# **Task 2: User Creation Ansible Playbook**

* Create an Ansible playbook for creating a new user on a different server
    

```plaintext
  - name: A playbook to create a new user
    hosts: all
    become: true
    tasks:
    - name: to create a user named <user_name>
      user: name=<user_name>
```

![](https://miro.medium.com/v2/resize:fit:875/1*QIbDtuXGsR2LZjm9jhNXMw.png align="left")

* Run the playbook using the ansible-playbook command
    

```plaintext
  ansible-playbook create_user.yml
```

![](https://miro.medium.com/v2/resize:fit:875/1*A4biArbpbCr50qRqwXLQVw.png align="left")

* Once the execution is finished, to check if the user has been created, look for the user’s name in the `/etc/passwd` file where all the user and system file details are stored on servers.
    

```plaintext
  ansible server1 -a "cat /etc/passwd"
```

![](https://miro.medium.com/v2/resize:fit:875/1*dAjeXNJRkOJLc8XwDVPesg.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*MtcVHFLazZisCT-glaCMKQ.png align="left")

# **Task 3: Docker Installation Ansible playbook**

* Create an Ansible playbook to install docker on a different server
    

```plaintext
  -
    name: A Playbook to Install Docker
    hosts: my-servers
    become: yes

    tasks:
      - name: Add Docker GPG apt Key
        apt_key:
          url: https://download.docker.com/linux/ubuntu/gpg
          state: present

      - name: Add Docker Repository
        apt_repository:
          repo: deb https://download.docker.com/linux/ubuntu focal stable
          state: present

      - name: Update apt and install docker-ce
        apt:
          name: docker-ce
          state: latest
          update_cache: true
```

![](https://miro.medium.com/v2/resize:fit:875/1*rwkSxW7td-k4AX_lSiHhyQ.png align="left")

* Run the playbook using the ansible-playbook command.
    

```plaintext
  ansible-playbook install_docker.yml
```

![](https://miro.medium.com/v2/resize:fit:875/1*FWWlM_Lx6kv9SoeFd3f5Ig.png align="left")

* Verify that Docker has been installed on multiple servers using the following command.
    

```plaintext
  ansible all -a "docker --version"
```

![](https://miro.medium.com/v2/resize:fit:875/1*N7bxdlxLJ1_CUmGnLKlMpQ.png align="left")

* To get the Docker status of all the servers, use the following command:
    

```plaintext
  ansible all -a "sudo systemctl status docker"
```

![](https://miro.medium.com/v2/resize:fit:875/1*05LYOzbqTd_giklPhUSdvQ.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*1gTtnwQtImdXFA8zS_WjTw.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*c9TjEpMqVeATWEJPuBNxzA.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*Q_ek_zjiFrinIpwJ3jJg9A.png align="left")

In this blog, we’ve unveiled the fundamental aspects of Ansible Playbooks, from their inception and key features to crafting your own Playbooks with intricate details like inventory management, task execution, and error handling.

We’ve even explored practical use cases with dedicated tasks, including file creation, user management, and Docker installation.

As you embark on your automation journey, remember that continuous learning and sharing are vital.

Your feedback is crucial to our growth, so don’t hesitate to connect with me on [LinkedIn at Mudit Mathur.](https://www.linkedin.com/in/mudit--mathur/) Stay tuned for more DevOps insights and Ansible tips as we continue our journey. #Day57 #90daysofdevops