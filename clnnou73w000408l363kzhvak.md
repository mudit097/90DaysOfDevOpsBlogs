---
title: "Day 58 : Ansible Project"
datePublished: Thu Oct 12 2023 21:24:41 GMT+0000 (Coordinated Universal Time)
cuid: clnnou73w000408l363kzhvak
slug: day-58-ansible-project
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697145375955/91a9973c-10d4-4c86-8f2f-1d0363a91240.png
tags: blogging, aws, devops, 90daysofdevops, trainwithshubham

---

Welcome back for creating an Ansible Project using Ansible Playbook. In this blog post, we dive into the world of Ansible projects, exploring how to structure and organize your automation workflows effectively.

Discover best practices for creating Ansible projects that simplify configuration management, application deployment, and system orchestration. Harness the power of Ansible to streamline your infrastructure management and drive efficiency in your IT operations.

# **Deploy a Website 🌐using Ansible Playbook**

* Create 4 EC2 instances. Out of 4, One will be the Ansible Master node and the other 3 are child nodes. Make sure all three child nodes are created with the same key pair as Ansible Master.
    

![](https://miro.medium.com/v2/resize:fit:875/0*rLelTxX8Bz5YrJuw.png align="left")

* Install Ansible on Ansible Master node only.
    

```plaintext
  # Add ansible repository to your instance
  sudo apt-add-repository ppa:ansible/ansible

  # Update the package
  sudo apt update

  # Install the Ansible
  sudo apt install ansible
```

![](https://miro.medium.com/v2/resize:fit:875/0*ejMEH45qD_lV7a_Z.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*1rVklKpbi3fIQkFu.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/0*9o_Jge4jXmu9PGbC.png align="left")

* Once the installation is complete, you can check the version of Ansible using the following command:
    

```plaintext
  ansible --version
```

![](https://miro.medium.com/v2/resize:fit:875/0*oqdFHBZwaWQV5vSq.png align="left")

* Copy the private key from local to the Host server (Ansible Master) at the /home/ubuntu/.ssh folder location.
    

```plaintext
  sudo scp -i "<pem_key>" <pem_key> <ubuntu@ec2.amazonecom>:/home/ubuntu/.ssh/
```

![](https://miro.medium.com/v2/resize:fit:875/1*W5dy9nGKGc2i5cuTjxTQuQ.png align="left")

* Once the file is copied to the .ssh directory, change the private key permission rwx to the user only.
    

```plaintext
  chmod 700 flask-server
```

![](https://miro.medium.com/v2/resize:fit:875/0*QQ7fjPRmhstmHTyQ.png align="left")

* Access the inventory file using `sudo cat /etc/ansible/hosts`
    

![](https://miro.medium.com/v2/resize:fit:875/1*B9WYcLvc6wTuVy5bbY7USw.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*EN9HSEAh8zukMOPWrdXR-Q.png align="left")

* Edit the inventory file and add the list of hosts or servers, add the IP addresses of the servers also add private key file location to use for authentication.
    

```plaintext

  [my-servers]
  server1 ansible_host=<Server1_IPv4_Addr>
  server2 ansible_host=<Server2_IPv4_Addr>
  server3 ansible_host=<Server3_IPv4_Addr>

  [all:vars]
  ansible_ssh_private_key_file=/home/ubuntu/.ssh/flask-server.pem
  ansible_python_interpreter=/usr/bin/python3
  ansible_user=ubuntu
```

![](https://miro.medium.com/v2/resize:fit:875/1*hTR5TGMvP0gdadUMcZ_IJw.png align="left")

Now create a playbook to install Nginx

```plaintext
  -
    name: Install and Start Nginx
    hosts: my-servers
    become: yes

    tasks:
      - name: Update apt
        apt:
           update_cache: yes
      - name: Install Nginx
        apt:
          name: nginx
          state: latest
      - name: Start Nginx
        service: 
           name: nginx
           state: started
           enabled: yes
```

![](https://miro.medium.com/v2/resize:fit:875/1*e1x-ujnp6ibb8umbjxZW6A.png align="left")

Run the playbook using the ansible-playbook command

```plaintext
  ansible-playbook install_nginx.yml
```

![](https://miro.medium.com/v2/resize:fit:875/1*Tt4U0_b8b7ILZzGvbjioDQ.png align="left")

Check the status of Nginx on all the child servers.

```plaintext
  ansible all -a "sudo systemctl status nginx"
```

![](https://miro.medium.com/v2/resize:fit:875/1*5afF_2Y_UMixkAsEQa4ajA.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*ZQ3jGCMCoPpuVRaAfXkGKA.png align="left")

For deploying a static website, Create a new file index.html and add the file path in the playbook directory, and add some sample content in the index file.

```plaintext
<!DOCTYPE html>
<html>
<head>
    <title>Mudit Mathur - DevOps Engineer</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #F6F6F6;
            color: #333;
            text-align: center;
            margin: 0;
            padding: 0;
        }

        h1 {
            color: #007BFF;
        }

        p {
            margin: 20px;
        }

        a {
            color: #007BFF;
            text-decoration: none;
        }

        a:hover {
            text-decoration: underline;
        }
    </style>
</head>
<body>
    <h1>Mudit Mathur - DevOps Engineer</h1>
    <p>
        Mudit Mathur is a highly skilled DevOps Engineer with over 2 years of experience in the field. With a strong background in supporting, automating, and optimizing deployments on AWS, I have successfully streamlined software development and delivery processes for various organizations.
    </p>
    <p>
        My expertise lies in leveraging configuration management tools, implementing CI/CD pipelines, and following DevOps best practices to ensure efficient and reliable software releases. I am well-versed in technologies such as Jenkins, Git, Linux, Ansible, and various AWS services, allowing me to design and implement robust DevOps solutions.
    </p>
    <p>
        Throughout my career, I have consistently delivered tangible results by improving efficiency and enhancing productivity through automation and collaboration. By automating manual processes, I have reduced deployment times, minimized errors, and improved overall system reliability. Additionally, my ability to work closely with cross-functional teams and foster a collaborative culture has resulted in successful project outcomes and seamless integration of new features and enhancements.
    </p>
    <p>
        As a detail-oriented professional, I strive for continuous improvement and stay updated with the latest trends and tools in the DevOps domain. I am passionate about finding innovative solutions to complex challenges and thrive in fast-paced, dynamic environments.
    </p>
    <p>
        If you are looking for a DevOps Engineer who can drive process optimization, enhance system scalability, and ensure seamless software delivery, please feel free to reach out. I am always eager to contribute my skills and expertise to help organizations achieve their goals.
    </p>
    <p>
        Let's connect and explore how we can work together to create efficient and robust DevOps solutions!
    </p>
    <p>
        LinkedIn: <a href="https://www.linkedin.com/in/mudit-mathur-535786146">linkedin.com/in/mudit-mathur-535786146</a>
    </p>
    <p>
        Email: <a href="muditmathur121@gmail.com">muditmathur121@gmail.com</a>
    </p>
</body>
</html>
```

![](https://miro.medium.com/v2/resize:fit:875/1*1Co_ITHW6GccheOvIdmFCw.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*vuNHB7ZfTv0jjvnrBBQfrw.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*LwVe1t9fBeuhEXmY9aPPwQ.png align="left")

Update the Ansible playbook file by providing the index.html file path and destination will be the default NGINX web page, install\_nginx.yml, in the playbook directory:

```plaintext
  -
     name: Install and Start Nginx
     hosts: my-servers
     become: yes

    tasks:
      - name: Update apt
        apt:
           update_cache: yes
      - name: Install Nginx
        apt:
          name: nginx
          state: latest
      - name: Start Nginx
        service: 
           name: nginx
           state: started
           enabled: yes
      - name: Deploy Nginx
        copy:
            src: /home/ubuntu/index.html
            dest: /var/www/html/index.html
        become: true
        become_user: root
        become_method: sudo
```

![](https://miro.medium.com/v2/resize:fit:875/1*SyY7Yrv4TW49YRsvcKUT8w.png align="left")

Run the playbook using ansible-playbook command.

```plaintext
  ansible-playbook install_nginx.yml
```

![](https://miro.medium.com/v2/resize:fit:875/1*9Es_wnngUXv1YRG6ljmjWw.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*CKRJM2-fswy4iQ_ehCZRkw.png align="left")

Once the playbook finishes executing, open a web browser and enter the public IP address of one of the EC2 instances running Nginx

Server1

![](https://miro.medium.com/v2/resize:fit:875/1*zPhCO-x396bAK0P1nhxhMw.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*s0EYRWhf8WuKsevFsfisUw.png align="left")

Server 2

![](https://miro.medium.com/v2/resize:fit:875/1*JkYpRO2ZPxmxJKCmmxV1Uw.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*doindsMc1x_YWcb1A-vjyg.png align="left")

Server 3

![](https://miro.medium.com/v2/resize:fit:875/1*ovBcZOLX32mYtJfrYmOLAw.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*PHkJfxMgR4sCuBoWp7FUiA.png align="left")

The blog post provides a comprehensive guide on deploying a website using Ansible Playbook. It covers setting up an Ansible project structure, creating EC2 instances, installing Ansible, configuring secure communication, and deploying Nginx for a static website. The author encourages feedback and connections on LinkedIn at Mudit Mathur and promises more DevOps insights and Ansible tips as they continue their journey. #Day58 #90daysofdevops

Your feedback is crucial to our growth, so don’t hesitate to connect with me on [LinkedIn at Mudit Mathur.](https://www.linkedin.com/in/mudit--mathur/)

Stay tuned for more DevOps insights and Ansible tips as we continue our journey. #Day58 #90daysofdevops