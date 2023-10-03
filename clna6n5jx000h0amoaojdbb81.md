---
title: "Relational Database Service | AWS"
datePublished: Tue Oct 03 2023 10:34:19 GMT+0000 (Coordinated Universal Time)
cuid: clna6n5jx000h0amoaojdbb81
slug: relational-database-service-aws
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696329162684/fa4f7567-5d82-4a27-9260-77b3cad92744.png
tags: blogging, aws, devops, 90daysofdevops, trainwithshubham

---

In previous blogs, we have dealt with the AWS CLI and accessing S3 and IAM programmatically through CLI. In this blog let us understand the RDS in AWS.

Here’s the official documentation for [Relational Database Service in AWS.](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html)

# **RDS (Relational Database Service) in AWS**

According to the official documentation, “Amazon Relational Database Service (Amazon RDS) is a web service that makes it easier to set up, operate, and scale a relational database in the AWS Cloud. It provides cost-efficient, resizable capacity for an industry-standard relational database and manages common database administration tasks.”

RDS offers six database engines:

* MySQL: A widely-used open-source relational database management system known for its stability, ease of use, and compatibility.
    
* MariaDB: A community-developed, open-source fork of MySQL, offering similar features and compatibility.
    
* PostgreSQL: An open-source object-relational database management system known for its robustness, extensibility, and support for advanced features.
    
* Oracle: A commercial relational database management system that provides enterprise-level features and capabilities.
    
* SQL Server: A commercial relational database management system developed by Microsoft, offering scalability, security, and integration with Microsoft products.
    
* Amazon Aurora: A MySQL and PostgreSQL-compatible database engine developed by AWS. It offers high performance, scalability, and durability. It is up to five times faster than MySQL.
    

Some more links that can help:

* [Creating and connecting to a MariaDB DB instance](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_GettingStarted.CreatingConnecting.MariaDB.html)
    
* [Creating and connecting to a Microsoft SQL Server DB instance](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_GettingStarted.CreatingConnecting.SQLServer.html)
    
* [Creating and connecting to a MySQL DB instance](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_GettingStarted.CreatingConnecting.MySQL.html)
    
* [Creating and connecting to an Oracle DB instance](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_GettingStarted.CreatingConnecting.Oracle.html)
    
* [Creating and connecting to a PostgreSQL DB instance](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_GettingStarted.CreatingConnecting.PostgreSQL.html)
    

Let us jump into today’s tasks to get our hands dirty and learn some fun things.

# **Task: Create a Free tier RDS instance of MySQL. Once the RDS instance is up and running, get the credentials and connect your EC2 instance using a MySQL client.**

*Create a Free tier RDS instance of MySQL*

Go to your AWS console &gt; Search RDS &gt; Choose Create database &gt; Select Standard Create &gt; Under “Engine options”, choose “MySQL”

![](https://miro.medium.com/v2/resize:fit:875/1*mvkAp77Cii4i0qlokGPwgQ.png align="left")

Select the Free tier

![](https://miro.medium.com/v2/resize:fit:875/1*bHb7UXur94j7fq37ebfTTw.png align="left")

Under Settings, I am providing the following details:

> *DB instance identifier: database-example-rd-1*
> 
> *Credentials Settings:*
> 
> *Master username: admin*
> 
> *And provide the password of your choice according to the constraints mentioned.*
> 
> *Configure other settings like storage, backups, VPC, and security groups according to your requirements. Review the configuration and click “Create Database”.*

RDS creation takes a few minutes.

![](https://miro.medium.com/v2/resize:fit:875/1*BxnpF8pYzoRNLhzV-1SYDw.png align="left")

*Create an EC2 instance*

I am creating an instance named rds-ec2-instance.

![](https://miro.medium.com/v2/resize:fit:875/1*jwewOqG8WBYpllgkBkgGmw.png align="left")

I am configuring the security group to allow inbound traffic on the MySQL port (default is 3306).

![](https://miro.medium.com/v2/resize:fit:875/1*0aJZ1QChxJ5gFzXYNEXcJQ.png align="left")

*Create an IAM role with RDS access. Assign the role to EC2 so that your EC2 Instance can connect with RDS.*

Go to IAM Dashboard &gt; Click on Roles &gt; Create Role &gt; Select the EC2 service for the trusted entity &gt; In permission policies, attach the permission [AmazonRDSFullAccess](https://us-east-1.console.aws.amazon.com/iamv2/home?region=ap-south-1#/policies/details/arn%3Aaws%3Aiam%3A%3Aaws%3Apolicy%2FAmazonRDSFullAccess) &gt; Name the role as “rds-ec2” &gt; Create Role.

The role is created.

![](https://miro.medium.com/v2/resize:fit:875/1*ob_L-63qA8_5i5qarXBsXg.png align="left")

Let’s assign this role to our EC2 which we created.

Go to your EC2 Management Console &gt; Actions &gt; Security &gt; Modify IAM Roles

![](https://miro.medium.com/v2/resize:fit:875/1*jwewOqG8WBYpllgkBkgGmw.png align="left")

Select the role we created for this task.

![](https://miro.medium.com/v2/resize:fit:875/1*8EYArHZnQctAoiyj1X9htg.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*aJo0TSkEv-1YLcasj2YFDQ.png align="left")

*Once the RDS instance is up and running, get the credentials and connect your EC2 instance using a MySQL client.*

Go to RDS Dashboard &gt; Select the Database you created &gt; Copy the endpoint, port, and master username.

> *Under Connectivity & security:*
> 
> *Endpoint:* [*database-example-rd-1.cg9zuoghw8tf.ap-south-1rds.amazonaws.com*](http://database-example-rd-1.cg9zuoghw8tf.ap-south-1rds.amazonaws.com)
> 
> *Port: 3306*
> 
> *Scroll down to Connected compute resources:*
> 
> *Click on Set up EC2 connection. Select the instance which we created for this purpose.*

![](https://miro.medium.com/v2/resize:fit:875/1*6fA01DqqL8Vg_24ufuRYlg.png align="left")

*And this can be verified under the same tab:*

![](https://miro.medium.com/v2/resize:fit:875/1*nFe2T-v0JKo57MuwXmId6A.png align="left")

> *Under Configuration:*
> 
> *Master username: admin*

Let’s connect to the EC2 instance using SSH.

And then install the MySQL client in the instance:

```plaintext
sudo apt-get update
sudo apt-get install mysql-client
mysql --version
```

![](https://miro.medium.com/v2/resize:fit:875/1*hk231QmCFmRRdIE3CMerOw.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*PN10Uhx-HJy1QXoGd_4KYg.png align="left")

To connect to the RDS instance using the MySQL client and the endpoint address, username, and password, we use the following command:

```plaintext
mysql -h <RDS_ENDPOINT> -P <RDS_PORT> -u <MASTER_USERNAME> -p
#The below details we copied when we created the RDS instance:
#<RDS_ENDPOINT> with the endpoint of your RDS instance
#<RDS_PORT> with the port number (default is 3306)
#<MASTER_USERNAME> with the master username
# '-h' is used to specify the endpoint of MySQL server to which we want to connect (basically the host)
```

My command will look like this:

```plaintext
mysql -h database-example-rd-1.cg9zuoghw8tf.ap-south-1rds.amazonaws.com -P 3306 -u admin -p
```

After running this command, you will be prompted for the password. Give the password you created while creating RDS:

![](https://miro.medium.com/v2/resize:fit:875/1*MH5KgJ-PRl2F-rTUEBjFOA.png align="left")

Now you can verify the CRUD operations confirming the MYSQL is working properly.

![](https://miro.medium.com/v2/resize:fit:411/1*Rkq3H8QEHbFkaqqNWenYoA.png align="left")

And Yay! We have created a Free tier RDS instance of MySQL, an EC2 instance, assigned an IAM role with RDS access to the EC2 instance, and connected to the RDS instance from the EC2 instance using a MySQL client.

In this blog, I have discussed Relational Database Services in AWS. If you have any questions or want to share your experiences, please comment below. Don’t forget to read my blogs and connect with me on LinkedIn and let’s have a conversation.

To help me improve my blog and correct my mistakes, I am available on LinkedIn as [Mudit Mathur](https://www.linkedin.com/in/mudit--mathur/). Do reach me and I am open to suggestions and corrections.

#Day44 #90daysofdevops