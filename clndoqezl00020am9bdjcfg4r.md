---
title: "Deploy WordPress website on AWS"
datePublished: Thu Oct 05 2023 21:24:03 GMT+0000 (Coordinated Universal Time)
cuid: clndoqezl00020am9bdjcfg4r
slug: deploy-wordpress-website-on-aws
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696540848887/f4955909-9510-4d92-840f-6716decf7b01.png
tags: aws, databases, cloud-computing, devops, trainwithshubham

---

Over 30% of all websites use WordPress as their content management system (CMS). It is often used to run blogs, but it can also be used to run e-commerce sites, message boards, and many other famous things. In this blog, I will show you how to set up a WordPress blog site.

Here’s the guide to official documentation from AWS [to deploy this project.](https://aws.amazon.com/getting-started/hands-on/deploy-wordpress-with-amazon-rds/)

Before getting ahead, let us know why we need to use RDS:

* Database maintenance for your WordPress site is critical. Your database instance holds all of your important data for your WordPress site. If the database goes down, your website may go down with it, and you could even lose your data.
    
* Database maintenance can also be difficult, and database administrators have years of specialized experience. When setting up a WordPress site, you want to stay focused on designing your page and generating your content, not worrying about database performance and backups.
    

Amazon RDS for MySQL helps with both of these problems. Amazon RDS for MySQL is a managed database offering from AWS. With Amazon RDS for MySQL, you get:

* Automated backup and recovery so that you won’t lose data in the event of an accident
    
* Regular updates and patches, keeping your database secure and performant
    
* Easy installation with smart default parameters.
    

Let’s start the project now.

We can divide this project into seven sections, for us to make it easy to understand:

Step 1: 🚀 Launch an Amazon EC2 Instance

Step 2: 🛠️ Set Up an Amazon RDS for MySQL Database

Step 3: 🔐 Create an IAM Role for EC2 with RDS Full Access

Step 4: 🔄 Connect EC2 to RDS Using MySQL Client

Step 5: 🌐 WordPress DB Creation and Apache Server Installation

Step 6: 📝 Set up the server and post your new WordPress app.

Step 7: 🌐 Explore the Newly Set Website and Clean Up

# **Step 1: 🚀 Launch an Amazon EC2 Instance**

1. Navigate to EC2: In the AWS Console, go to the Amazon EC2 service. 🚀
    

![](https://miro.medium.com/v2/resize:fit:875/1*lScdZeFU6h5ZnyaqEHJm7Q.png align="left")

2\. Launch an EC2 Instance:

* Click on “Launch Instance” to create a new EC2 instance. 🚀
    
* Choose an Amazon Machine Image (AMI) that suits your requirements. A common choice is an Amazon Linux AMI. 📦
    

![](https://miro.medium.com/v2/resize:fit:875/1*g_aof9mGvfox44aB-HadzA.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*stTJoaffvI8YOPs2vhaavw.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*rznb5GUxPUcKR8V9GEe6pA.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*uPubh1xqUOX_xlU5I8UsxQ.png align="left")

* Select an instance type based on your website’s expected traffic and resource needs. ⚙️
    

![](https://miro.medium.com/v2/resize:fit:875/1*dAc1wqJoAKqsmnOVrzgVcg.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*JWkNHMC5RWbdPnD4fNNRTA.png align="left")

* Configure the instance details, including network settings, subnet, and IAM role (if required). 🛡️
    
* Add storage based on your needs. A recommended practice is to have enough storage to accommodate your website files. 🗂️
    
* Configure security groups to allow incoming traffic on ports 22 (SSH), 80 (HTTP) and 3306 (MySQL) to the EC2 instance. 🔒
    

![](https://miro.medium.com/v2/resize:fit:875/1*pd2eAi08zqK1vcFYF9Smjg.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*YzPjWsnaP8yRIAEQ2wCm6w.png align="left")

3\. Create or Use an Existing Key Pair: If you don’t have an existing key pair, create a new one. You’ll use this key pair to access your EC2 instance securely via SSH. 🔑

4\. Launch the EC2 Instance: Once you’ve reviewed your instance configuration, launch the instance. AWS will create it, and you can view the status in the EC2 Dashboard. 🚀

![](https://miro.medium.com/v2/resize:fit:875/1*FZ_HYKDkaz1haHQeGZDzYQ.png align="left")

# **Step 2: 🛠️ Set Up an Amazon RDS for MySQL Database**

1. Log in to AWS Console: Open your AWS Management Console.
    
2. Navigate to RDS: In the AWS Console, go to the Amazon RDS service. 🖥️
    

![](https://miro.medium.com/v2/resize:fit:875/1*GGCrK61URqyc4-ZY9rj0uw.png align="left")

3\. Create a New RDS Instance:

* Click on “Create Database” to start the RDS creation process. 📦
    
* Choose “MySQL” as the database engine since WordPress requires it. 🗄️
    

![](https://miro.medium.com/v2/resize:fit:875/1*H7LVbaguE8hdp2CWoFXpPQ.png align="left")

* Select the appropriate version and edition based on your requirements. ⚙️
    
* Configure your database instance details, including instance class, storage, and instance identifier. Make sure to set up a strong master username and password for database access. 📝
    
* Adjust advanced settings as needed, including VPC, security groups, and backups. 🧩
    

![](https://miro.medium.com/v2/resize:fit:875/1*eYZwDj7K8dnjn5kqOqSf3Q.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*eSpcOgBI6gc5n5PJB7Dlxg.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*oDgcINuH43GdQilPoUmBGw.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*6cbotiOY5sdN6TVfiv7xng.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*_l3xl221kpcLWRnlRXen5Q.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*2G3s2DSbJY35XhElNGillw.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*E3zDhRHlhC9ByCVa6brtIQ.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*E6y7U_X9GEXvz0-CTeGHkQ.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*rpjU_uvZhw1qG9DQuTHgVg.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*EpyxmBiK1rBgz3nFjTxGWQ.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*xQbtDdE3nMky0zLMNk69Ng.png align="left")

* Finally, create the RDS instance by clicking “Create Database.” 🚀
    

![](https://miro.medium.com/v2/resize:fit:875/1*yDCjDAVrsYUBzU_tj_nCnw.png align="left")

4\. Wait for Database Creation: It may take a few minutes for the RDS instance to be created. Monitor the progress in the RDS Dashboard. 🕒

5\. Retrieve Database Endpoint: Once the RDS instance is available, note down the endpoint URL. You’ll need this information to configure WordPress later. 🌐

# **Step 3: 🔐 Create an IAM Role for EC2 with RDS Full Access**

1: Log in to AWS Console 🔐

1. Go to the AWS Management Console.
    

2: Navigate to IAM 🚀

1. In the AWS Console, navigate to the “Services” menu.
    
2. Select “IAM” (Identity and Access Management) under the “Security, Identity, & Compliance” section.
    

![](https://miro.medium.com/v2/resize:fit:875/1*trIkA1kVunGkiF44zQBAhg.png align="left")

3: Create and Assign an IAM Role to EC2 Instance 🛠️

1. In the IAM Dashboard, click on “Roles” in the left navigation pane.
    
2. Click the “Create role” button.
    

![](https://miro.medium.com/v2/resize:fit:875/1*5MWV4HXrWCHGr7Th1JeKyA.png align="left")

3\. Choose “AWS service” as the trusted entity type.

4\. Under “Choose the use case,” select “EC2” as the service that will use this role.

![](https://miro.medium.com/v2/resize:fit:875/1*C2BVqBQjbAiYPYDgiXofjA.png align="left")

5\. Click “Next: Permissions.”

6\. In the “Permissions” step, attach the necessary policies. To grant full access to Amazon RDS, search for and attach the “AmazonRDSFullAccess” policy. You can also attach additional policies as needed for your use case.

![](https://miro.medium.com/v2/resize:fit:875/1*_Z5dakCEJgMIloSz3igCVQ.png align="left")

7\. Click “Next: Tags”.

8\. Provide a meaningful name for the role in the “Role name” field.

![](https://miro.medium.com/v2/resize:fit:875/1*sLOshfZCoejRwpMnSLRvQw.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*XJ_iZ_Xb6P6BahGmZk91EA.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*6T64-o27oJ1Lq2QPlrg0ww.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*Thprs3MKYESxvuEMUZoK5w.png align="left")

9\. Optionally, add a description for the role in the “Role description” field.

10\. Click the “Create role” button.

![](https://miro.medium.com/v2/resize:fit:875/1*3-K82ICsVzteFLS4OHiS3w.png align="left")

4: Assign the IAM Role to an EC2 Instance 🔄

1. Go to the EC2 Dashboard in the AWS Console.
    

![](https://miro.medium.com/v2/resize:fit:875/1*lOtotYMGzjbAZAcsbd381g.png align="left")

2\. Select the EC2 instance to which you want to assign the IAM role.

3\. In the instance details pane, click on “Actions.”

4\. Choose “Security,” and then click on “Modify IAM Role.”

![](https://miro.medium.com/v2/resize:fit:875/1*b31RG7nMyPqdtE0n3Q7rpA.png align="left")

5\. In the “IAM role” dropdown, select the IAM role you just created.

![](https://miro.medium.com/v2/resize:fit:875/1*t-fP9dr4vfTsK9talgbvDg.png align="left")

6\. Click “Apply”

The IAM role is now assigned to the EC2 instance, granting it full access to Amazon RDS. You’ve successfully created and assigned an IAM role with the necessary permissions. 🎉

# **Step 4: 🔄 Connect EC2 to RDS Using MySQL Client**

1. SSH into your EC2 instance using the key pair you saved during the EC2 instance setup.
    

```plaintext
  ssh -i your-key-pair.pem ec2-user@your-ec2-instance-ip
```

![](https://miro.medium.com/v2/resize:fit:875/1*q-Ha3jxJ8Uyay1Ig2O4D_Q.png align="left")

2\. Update your EC2 instance by running:

```plaintext
  sudo apt update -y
```

![](https://miro.medium.com/v2/resize:fit:875/1*KHbEbt8iIHYji1ED1YoAjQ.png align="left")

3\. Install the MySQL client on your EC2 instance:

```plaintext
  sudo apt install mysql-server -y
```

![](https://miro.medium.com/v2/resize:fit:875/1*s2-b4_lEPjAIAEdl85iHmg.png align="left")

4\. Connect to your RDS MySQL instance using the credentials you noted in Step 1:

```plaintext
   mysql -h <endpoint address> -P <port.no> -u <username> -p
```

![](https://miro.medium.com/v2/resize:fit:875/1*McLXvnTr1JSa1euRSUiNuQ.png align="left")

5\. Enter the MySQL password when prompted.

6\. You are now connected to your RDS MySQL instance via your EC2 instance using the MySQL client.

![](https://miro.medium.com/v2/resize:fit:875/1*f1PpLJ02JyLBUXVRWRxyKw.png align="left")

# **Step 5: 🌐 WordPress DB Creation and Apache Server Installation**

1. Create a database user for the WordPress application and give the user permission to access the WordPress database.
    

```plaintext
    CREATE DATABASE wordpress;
    CREATE USER 'wordpress' IDENTIFIED BY 'wordpress-99';
    GRANT ALL PRIVILEGES ON wordpress.* TO wordpress;
    FLUSH PRIVILEGES;
    Exit
```

![](https://miro.medium.com/v2/resize:fit:875/1*_vrakNWwGsWpimMRSuX1ZA.png align="left")

2\. To run WordPress, you need to run a web server on your EC2 instance.

To install Apache on your EC2 instance, run the following command in your terminal:

```plaintext
     sudo apt-get install apache2
```

![](https://miro.medium.com/v2/resize:fit:875/1*26rR7nXS3AUoyzvdg_IyCQ.png align="left")

3\. To start the Apache web server, run the following command in your terminal:

```plaintext
    sudo systemctl restart apache2
```

![](https://miro.medium.com/v2/resize:fit:875/1*I-wMN519j58zgE2mOSaVTw.png align="left")

4\. You can see that your Apache web server is working by browsing the public-IP of your ec2 instance.

![](https://miro.medium.com/v2/resize:fit:875/1*5JZgpUqcr32TVKrOKxr8og.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*MM9Cli-hIRwOiQgBBQ2w7A.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*1Rlf1YJGTPR-uRapkmE2xg.png align="left")

# **Step 6: 📝 Set up the server and post your new WordPress app.**

Download and uncompressed the WordPress software by running the following commands in your terminal:

```plaintext
  wget https://wordpress.org/latest.tar.gz
  tar -xzf latest.tar.gz
```

![](https://miro.medium.com/v2/resize:fit:875/1*UJ0sYtj5sZ2PTE0u7peyEw.png align="left")

Now we will see a tar file and a directory called WordPress with the uncompressed contents using the ls command.

![](https://miro.medium.com/v2/resize:fit:875/1*YKFXx8ImraUSg3TrM0uVzg.png align="left")

Change the directory to the WordPress directory and create a copy of the default config file using the following commands

![](https://miro.medium.com/v2/resize:fit:875/1*pBgvlR07nTwDeZYx4aSaaA.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*gAmiqzjSXgfUkEa94zE3zw.png align="left")

Now create a copy of the config file and edit the wp-config.php file

```plaintext
  sudo cp wp-config-sample.php wp-config.php
  sudo vim wp-config.php
```

Edit the database configuration by changing the following lines:

![](https://miro.medium.com/v2/resize:fit:875/1*TzGyL1PIy_h21J-6GuQZDA.png align="left")

Authentication Unique Keys and Salts:

You can generate the content of this section from this link: [https://api.wordpress.org/secret-key/1.1/salt/](https://api.wordpress.org/secret-key/1.1/salt/).

Replace with the existing content.

![](https://miro.medium.com/v2/resize:fit:875/1*bNA4xkPnkaILS5rdTtjrUA.png align="left")

Install the application dependencies you need for WordPress. In your terminal, run the following command.

```plaintext
  sudo apt install php libapache2-mod-php php-mysql -y
```

![](https://miro.medium.com/v2/resize:fit:875/1*yttNr5wFFR0Y497dhYNRPw.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*uyNCdTud_bZj3oiI7hYAEA.png align="left")

Copy your WordPress application files into the /var/www/html directory used by Apache.

```plaintext
  sudo cp -r wordpress/* /var/www/html/
```

![](https://miro.medium.com/v2/resize:fit:875/1*kwBBACmLqz6qJR5eXyo4vQ.png align="left")

Finally, restart the Apache web server

```plaintext
  sudo systemctl restart apache2
```

Browse public-ipv4address/wp-admin/ you should see the WordPress welcome page.

```plaintext
http://Public_IPv4/wp-admin
```

![](https://miro.medium.com/v2/resize:fit:875/1*rGjrAUEO39pXEJfC-RcRNA.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*LW9T6Sji3Q_nfDgu-ayEag.png align="left")

And yay! You have your own WordPress website.

Now let’s step into the final section of this Project.

# **Step 7: 🌐 Explore the Newly Set Website and Clean Up**

Once you have explored, we need to clean up the resources so that we can avoid being charged.

Delete your EC2 instance first and then the RDS.

![](https://miro.medium.com/v2/resize:fit:875/1*O-3RjFWrGRlqqg7mb8S4aA.png align="left")

Delete the RDS instance now:

![](https://miro.medium.com/v2/resize:fit:875/1*yO8-kgV3VpYbqlbpLqBJEA.png align="left")

And we have no resources that we can be charged for.

In this blog, we’ve outlined a step-by-step guide to deploying a WordPress website on AWS. From launching an EC2 instance to exploring the final result, we’ve covered all the essential steps. Plus, by following this project, you can enhance your AWS skills and even add it to your resume.

Share your thoughts in the comments and connect with me on [LinkedIn(Mudit Mathur)](https://www.linkedin.com/in/mudit--mathur/) for suggestions and corrections. Stay tuned for more valuable content! #Day45 #90daysofdevops