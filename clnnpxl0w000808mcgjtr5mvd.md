---
title: "Ansible Interview Q&A"
datePublished: Thu Oct 12 2023 21:55:19 GMT+0000 (Coordinated Universal Time)
cuid: clnnpxl0w000808mcgjtr5mvd
slug: ansible-interview-qa
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697145964216/2ec30ede-770c-4326-9814-3845ff5239be.png
tags: interview, aws, ansible, tips, devops

---

Introduction: In today’s DevOps landscape, Ansible stands out as a powerful automation tool. It’s widely used for simplifying complex IT tasks, ensuring system consistency, and boosting productivity. In this blog, we’ll help you tackle the most commonly asked Ansible interview questions, breaking them into two sections: “Most Asked Ansible Q&A” and “Intermediate Ansible Q&A.”

**Most Asked Ansible Q&A:** In this section, we’ll cover the essentials, introducing Ansible, comparing it to Puppet, and discussing its pros and cons. We’ll also explore core concepts like playbooks, modules, and Ad-Hoc commands.

**Intermediate Ansible Q&A:** Here, we’ll delve into advanced topics, from managing diverse machine configurations to upgrading Ansible and deploying applications with Docker. You’ll also learn about secrets management and Ansible’s interactions with Docker and Docker API.

By the end of this blog, you’ll be well-prepared for Ansible-related interviews and real-world automation challenges. Let’s begin your journey to Ansible mastery, offering insights and answers one question at a time.

# **Most Asked Ansible Q&A**

# **1: What is Ansible and why it’s the most popular tool in DevOps?**

* Ansible is an open-source automation tool used for IT orchestration, configuration management, and application deployment.
    
* It’s popular in DevOps due to its agentless architecture, simplicity, wide platform support, scalability, idempotency, integration capabilities, and active community.
    
* With its human-readable syntax and extensive ecosystem, Ansible enables efficient and streamlined automation of repetitive tasks, making it a preferred choice for DevOps practitioners.
    

# **2️: How Ansible is different from Puppet?**

* Ansible and Puppet are both configuration management tools used in DevOps. Ansible uses an agentless architecture, communicates via SSH, and employs a YAML-based syntax for playbooks.
    
* Puppet uses an agent-based architecture, relies on a central Puppet master, and employs a declarative Puppet language.
    
* Ansible emphasizes simplicity and ease of use, while Puppet offers more advanced features for complex configurations and a stronger focus on state enforcement.
    

# **3️: Can you list down the pros and cons of Ansible?**

Pros of Ansible:

1. Agentless architecture.
    
2. Simple and easy-to-understand syntax.
    
3. Wide platform support.
    
4. Scalable and efficient.
    
5. Idempotent execution.
    
6. Strong integration capabilities.
    
7. Active community and extensive ecosystem.
    

Cons of Ansible:

1. Slower execution compared to agent-based tools.
    
2. Limited support for complex configurations.
    
3. Lack of built-in reporting and monitoring.
    
4. Reliance on SSH connectivity for communication.
    
5. Limited support for Windows environments (compared to Linux).
    

# **4️: What is the minimum requirement for Ansible to work?**

Currently, Ansible can be run from any machine with Python 2 (versions 2.6 or 2.7) or Python 3 (versions 3.5 and higher) installed (Windows isn’t supported for the control machine). This includes Red Hat, Debian, CentOS, OS X, any of the BSDs, and so on.

# **5️: Explain dynamic inventory and its use cases in Ansible.**

* Dynamic inventory in Ansible refers to the ability to generate inventory information dynamically at runtime.
    
* Instead of relying on a static inventory file, dynamic inventory sources can be scripts, APIs, or external systems.
    
* It allows for automatically discovering and provisioning hosts, making it useful for dynamic or cloud-based environments, auto-scaling scenarios, and managing large-scale infrastructures where hosts may change frequently.
    

# **6️: Which protocol does Ansible use to communicate with Linux & Windows?**

For Linux, the protocol used is SSH

For Windows, Protocol used in WinRM

# **7️: What are Ansible Modules?**

* Ansible modules are reusable units of code that perform specific tasks or actions within Ansible playbooks.
    
* They encapsulate functionality such as managing files, executing commands, configuring services, and interacting with various systems and platforms.
    
* Modules can be written in any programming language and are used to define the desired state and perform actions on managed hosts during Ansible automation tasks.
    

# **8️: What are Ansible Tasks?**

* In Ansible, a task is a unit of work defined in a playbook that performs a specific action on a target host.
    
* Tasks are executed sequentially and can include commands, module invocations, or even include other tasks.
    
* They define the desired state and actions to be taken to achieve that state, such as installing packages, configuring services, or managing files on the managed hosts.
    

# **9️: Can you explain what is a playbook in Ansible?**

* In Ansible, a playbook is a file written in YAML format that defines a set of tasks and configurations to be executed on one or more hosts.
    
* Playbooks allow for orchestrating complex automation workflows by defining the desired state, including tasks, roles, and variables.
    
* They provide a structured and readable way to define the automation logic and allow for easy repeatability and scalability.
    

# **1️0️: How do handlers work in task execution in Ansible?**

* Handlers in Ansible are tasks that are triggered only when notified by other tasks. They are typically used to handle specific events or changes in the system, such as service restarts or configuration updates.
    
* Handlers are defined separately from tasks and can be triggered using the “notify” keyword. When notified, handlers are executed at the end of the playbook run to ensure consistency and order in task execution.
    

# **1️1️: Can you explain what is Ad-Hoc command in Ansible?**

* Ad-Hoc commands in Ansible are one-time, on-the-fly commands that can be executed against one or more remote hosts without the need for writing a separate playbook.
    
* They are run using the `ansible` command followed by the target hosts and the desired module and parameters.
    
* Ad-Hoc commands are useful for quick tasks like running commands, gathering information, or performing simple configurations without the need for a full playbook.
    

# **1️2️: What is Ansible Vault?**

* Ansible Vault is a feature in Ansible that provides secure encryption and decryption of sensitive data such as passwords, API keys, and other secrets.
    
* It allows users to encrypt files or individual variables within playbooks, protecting them from unauthorized access.
    
* Vault ensures that sensitive information remains secure and can be safely stored and shared within an Ansible project.
    

# **1️3️: Can you explain the concept of Blocks in Ansible?**

* Blocks in Ansible provide a way to group related tasks together and apply error-handling and exception-handling logic.
    
* They allow for logical organization and control flow within a playbook. Tasks within a block are executed sequentially, and if any task fails within the block, error-handling strategies can be defined, such as retrying the block or moving to a specific rescue block for error handling.
    

# **1️4️: What are Groups of Groups and Group Variables in Ansible?**

* In Ansible, groups of groups (also known as nested groups) allow for hierarchical organization of hosts into logical groups. It enables grouping hosts based on different criteria, such as environment or role.
    
* Group variables, on the other hand, are variables specific to a group or groups of hosts. They provide a way to set shared variables that can be accessed by all hosts within a group, simplifying configuration management.
    

# **1️5️: Do you have any idea how to turn off the facts in Ansible?**

* To turn off gathering facts in Ansible, you can use the `gather_facts` directive in your playbook. Set `gather_facts: no` at the playbook level to disable facts gathering for all hosts within the playbook.
    
* Alternatively, you can set `gather_facts: no` at the task level to disable facts gathering for specific tasks, allowing for more granular control over when facts are collected during playbook execution.
    

# **1️6️: How variables are merged in Ansible?**

* In Ansible, variable merging follows a specific order of precedence.
    
* Variables are merged in the following order: the highest priority is given to variables defined in the playbook or role defaults, then variables defined in inventory files, followed by variables defined in playbook vars, and finally, variables defined in host or group vars.
    
* This merging process ensures that variables are resolved based on their defined scope and priority.
    

# **1️7️: What are Cache Plugins in Ansible? Any idea how they are enabled?**

* Cache plugins in Ansible are used to cache gathered facts, playbook results, and other data to improve performance by reducing the need for re-execution.
    
* They can be enabled by configuring the `ansible.cfg` file and specifying the cache plugin to use.
    
* Ansible provides various cache plugins, such as Redis, Memcached, JSON, and more, allowing users to choose the most suitable caching mechanism for their environment.
    

# **1️8️: What are Registered Variables in Ansible?**

* Registered variables in Ansible are used to capture and store the output or results of a task for later use within the playbook.
    
* When a task is executed, the result can be saved to a variable using the `register` keyword.
    
* The registered variable can then be accessed and utilized in subsequent tasks or conditionals, enabling more complex workflows and decision-making based on task outcomes.
    

# **1️9️: How Network Module work in Ansible?**

* The Network module in Ansible provides a collection of modules specifically designed for managing network devices, such as routers, switches, and firewalls.
    
* These modules communicate with network devices using protocols like SSH, Telnet, or APIs. They allow for tasks like configuring interfaces, managing VLANs, updating access control lists (ACLs), and more, providing a streamlined and consistent approach to network automation within Ansible playbooks.
    

# **2️0️: How Ansible manages multiple communication protocols?**

* Ansible manages multiple communication protocols by leveraging the concept of connection plugins. Connection plugins are responsible for establishing the communication between the Ansible control node and the target hosts.
    
* Ansible provides a range of connection plugins that support various protocols like SSH, WinRM, and local connections.
    
* By configuring the appropriate connection plugin, Ansible can seamlessly manage hosts with different communication requirements
    

# **Intermediate Ansible Q&A**

# **1️: How to handle different machines needing different user accounts or ports to log in with using Ansible?**

* To handle different machines needing different user accounts or ports for logging in with Ansible, you can utilize the “ansible\_user” and “ansible\_port” variables in your inventory or playbook.
    
* In the inventory file, specify the respective user account and port for each machine. Alternatively, you can define these variables directly in the playbook using the “vars” section. Ansible will then use the specified user account and port when connecting to the corresponding machines during execution.
    

# **2️: How to see a list of all of the ansible variables?**

* To see a list of all Ansible variables, you can use the debug module with the “msg” parameter set to “{{vars}}” in your playbook.
    
* This will print the entire set of variables and their values for the specific host being targeted. When executing the playbook, you will see the list of all Ansible variables in the output for that host.
    

# **3️: How to create an AWS EC2 key using Ansible?**

* To create an AWS EC2 key pair using Ansible, you can use the `ec2_key` module. Here's an example playbook:
    

```plaintext
  - name: Create EC2 Key Pair
    hosts: localhost
    gather_facts: false
    tasks:
      - name: Create EC2 Key Pair
        ec2_key:
          name: my-key
          region: us-east-1
        register: keypair

      - name: Save private key to file
        copy:
          content: "{{ keypair.key.private_key }}"
          dest: /path/to/private/key.pem
          mode: 0600
```

* In this example, the `ec2_key` module creates a key pair with the name "my-key" in the specified region. The private key of the created key pair is then saved to a file using the `copy` module. Adjust the values according to your desired key name, region, and file destination.
    

# **4️: How to upgrade the Ansible version to the latest version?**

* One can easily upgrade the Ansible version to the specific version using the below one-liner command:
    

```plaintext
  sudo pip install ansible==<version-number>
```

# **5️: How to install a WordPress application inside a Docker container using Ansible?**

* To install WordPress inside a Docker container using Ansible, you can utilize Ansible’s Docker modules. Here’s an example playbook:
    

```plaintext
  - name: Install WordPress in Docker
    hosts: localhost
    gather_facts: false
    tasks:
      - name: Create a network for containers
        docker_network:
          name: wordpress_network

      - name: Start MySQL container
        docker_container:
          name: mysql_db
          image: mysql:latest
          env:
            MYSQL_ROOT_PASSWORD: mysecretpassword
          networks:
            - name: wordpress_network

      - name: Start WordPress container
        docker_container:
          name: wordpress_app
          image: wordpress:latest
          env:
            WORDPRESS_DB_HOST: mysql_db
            WORDPRESS_DB_PASSWORD: mysecretpassword
          ports:
            - "8080:80"
          networks:
            - name: wordpress_network
```

* In this example, the playbook creates a network using the `docker_network` module. It then starts a MySQL container using the `docker_container` module, specifying the necessary environment variables. Finally, it starts a WordPress container with the appropriate environment variables and port mapping. Adjust the container names, network names, environment variables, and ports as per your requirements.
    

# **6️: How to generate encrypted passwords for the user module in Ansible?**

* To generate encrypted passwords for the user module in Ansible, you can use the `mkpasswd` command-line tool available in most Linux distributions. Here's an example:
    

1. Open a terminal on your Ansible control node.
    
2. Run the following command to generate an encrypted password:
    

```plaintext
 cssCopy codemkpasswd --method=SHA-512
```

3\. Enter the desired password when prompted.

4\. Copy the generated encrypted password.

5\. In your Ansible playbook, use the copied encrypted password as the value for the `password` parameter in the `user` module.

* By generating the password using `mkpasswd` with the desired encryption method (e.g., SHA-512), you can ensure that the password is securely encrypted for use with the `user` module in Ansible.
    

# **7️: How to keep secret data in my playbook in Ansible?**

* To keep secret data secure in your playbook, you can use Ansible Vault. Vault allows you to encrypt sensitive information such as passwords, API keys, and credentials.
    
* You can create an encrypted vault file with the `ansible-vault` command and reference the encrypted values in your playbook. During playbook execution, Ansible will prompt the vault password to decrypt the sensitive data.
    

# **8️: What is the minimum requirement for using Docker modules in Ansible?**

* To use Docker modules in Ansible, you need the following minimal requirements:
    

1. Ansible version 2.1 or later installed on the control node.
    
2. Docker is installed on the target hosts where you want to manage containers.
    
3. Network connectivity between the control node and the target hosts. With these prerequisites met you can use Ansible’s Docker modules to manage Docker containers and images from your Ansible playbooks.
    

# **9️: How does the Ansible module connect to Docker API?**

* Ansible connects to the Docker API using the Docker SDK for Python. The Docker modules in Ansible utilize this SDK to interact with the Docker daemon on the target host.
    
* The Docker SDK communicates with the Docker API over HTTP or a Unix socket, allowing Ansible to perform actions such as managing containers, images, networks, and volumes using the Docker API endpoints.
    

In Conclusion:

Our journey through Ansible, the cornerstone of DevOps automation, has provided essential knowledge and insights. If you have questions, feedback, or wish to connect, you can find me on LinkedIn at [Mudit Mathur](https://www.linkedin.com/in/muditmathur/).

Stay tuned for more DevOps wisdom and Ansible tips as we venture further in our #90daysofdevops expedition.