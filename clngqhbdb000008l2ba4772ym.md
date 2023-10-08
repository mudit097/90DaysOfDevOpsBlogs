---
title: "AWS Important Interview Q&A"
datePublished: Sun Oct 08 2023 00:36:16 GMT+0000 (Coordinated Universal Time)
cuid: clngqhbdb000008l2ba4772ym
slug: aws-important-interview-qa
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696725260384/54c6290c-76b2-4d94-91ff-cad96b52305e.png
tags: interview, aws, devops, 90daysofdevops, trainwithshubham

---

# **What are the different types of cloud computing?**

* There are three main types of cloud computing: Infrastructure as a Service (IaaS), Platform as a Service (PaaS), and Software as a Service (SaaS).
    

1. IaaS: IaaS provides virtualized computing resources over the internet, such as virtual machines, storage, and networks. Users have control over the operating systems and applications they run on the infrastructure, allowing for greater flexibility and customization.
    
2. PaaS: PaaS offers a platform for developers to build, deploy, and manage applications without the need to manage the underlying infrastructure. It provides a pre-configured environment that includes development tools, databases, and runtime environments, enabling developers to focus on application development rather than infrastructure management.
    
3. SaaS: SaaS delivers software applications over the internet on a subscription basis. Users can access and use these applications without the need for installation or management. Examples of SaaS include email services, customer relationship management (CRM) software, and productivity tools like Google Workspace.
    

# **What benefits organizations will have in moving to cloud computing?**

1. Scalability: Cloud computing allows organizations to scale their infrastructure and resources up or down as needed, ensuring optimal performance and cost-efficiency.
    
2. Cost Savings: By eliminating the need for upfront infrastructure investments and shifting to a pay-as-you-go model, organizations can reduce hardware and maintenance costs, achieving cost savings.
    
3. Flexibility and Agility: Cloud computing enables quick deployment of resources and facilitates rapid application development, allowing organizations to respond faster to market demands and adapt to changing business needs.
    
4. Reliability and Availability: Cloud providers offer robust infrastructure and high availability, minimizing downtime and ensuring reliable access to applications and data.
    
5. Security: Cloud providers invest heavily in security measures, offering advanced security features and compliance certifications, enhancing data protection and mitigating risks.
    
6. Collaboration and Remote Work: Cloud-based collaboration tools enable seamless communication and collaboration among team members, supporting remote work and enhancing productivity.
    

# **Name 5 aws services you have used and what are the use cases?**

* Amazon S3 (Simple Storage Service): S3 is used for object storage, hosting static websites, backup and restore, data archiving, content distribution, and data lakes.
    
* Amazon EC2 (Elastic Compute Cloud): EC2 provides resizable compute capacity in the cloud and is used for various use cases such as hosting web applications, running backend servers, batch processing, and machine learning.
    
* Amazon RDS (Relational Database Service): RDS offers managed relational databases like MySQL, PostgreSQL, Oracle, and SQL Server. It is used for running applications, storing user data, analytics, and reporting.
    
* Amazon DynamoDB: DynamoDB is a NoSQL database service for fast and scalable applications that require low-latency data access, such as gaming, mobile, and IoT.
    
* AWS Lambda: Lambda is a serverless compute service used for running code without provisioning or managing servers. It is commonly used for event-driven architectures, microservices, and automating workflows.
    

# **What are the tools used to send logs to the cloud environment?**

* There are several tools available to send logs to the cloud environment. Some commonly used tools are:
    

1. AWS CloudWatch Logs: AWS CloudWatch Logs enables you to collect, monitor, and store log files from various sources, including AWS services, applications, and custom sources.
    
2. AWS CloudTrail: AWS CloudTrail captures and logs API activity and events in your AWS account, providing visibility into actions taken by users, services, or resources.
    
3. Elasticsearch: Elasticsearch is an open-source search and analytics engine that can be used to store, index, and analyze logs. It is often paired with Logstash and Kibana (ELK stack) for log management and analysis.
    
4. Fluentd: Fluentd is an open-source data collector that can collect logs from various sources and send them to multiple destinations, including cloud storage or analysis platforms.
    
5. Logstash: Logstash is part of the ELK stack and is used for collecting, parsing, and transforming logs before sending them to a storage or analytics platform.
    

# **What are IAM Roles? How do you create/manage them?**

IAM (Identity and Access Management) roles in AWS provide a way to grant permissions to entities (such as users, applications, or services) without the need for long-term access keys. Here’s a brief overview of IAM roles and how to create/manage them:

IAM Roles:

* IAM roles define a set of permissions that determine what actions an entity can perform within AWS services.
    
* Roles are used to grant temporary credentials to entities and facilitate secure access to AWS resources.
    
* Roles are commonly used by EC2 instances, AWS Lambda functions, and other services to access AWS resources securely.
    

Creating an IAM Role:

1. Navigate to the IAM Management Console in AWS.
    
2. Choose “Roles” and click “Create role.”
    
3. Select the trusted entity (service or another AWS account) that will assume the role.
    
4. Choose the permissions policy that defines the access level for the role.
    
5. Add any additional policies to grant more granular permissions if needed.
    
6. Define a name and optional description for the role.
    
7. Review the role configuration and create the role.
    

Managing IAM Roles:

* To manage IAM roles, you can modify the role’s permissions, add or remove policies, and change the trusted entities that can assume the role.
    
* You can also attach IAM policies directly to roles to grant additional permissions.
    
* IAM roles can be associated with EC2 instances, Lambda functions, or other services by assigning the role to the respective resource during the resource’s creation or configuration.
    
* IAM roles can be managed using the IAM Management Console, AWS CLI (Command Line Interface), or programmatically using AWS SDKs (Software Development Kits).
    

# **How to upgrade or downgrade a system with zero downtime?**

* Upgrading or downgrading a system with zero downtime can be achieved by implementing certain strategies and best practices. Here’s a high-level approach:
    

1. Load Balancer: Set up a load balancer to distribute traffic across multiple instances or nodes. This allows for seamless traffic redirection during the upgrade/downgrade process.
    
2. Multiple Environments: Create multiple environments (e.g., staging, production) to perform the upgrade/downgrade process. Direct traffic to the unaffected environment while upgrading/downgrading the other.
    
3. Blue/Green Deployment: Implement a blue/green deployment strategy where the new version (green) is deployed alongside the existing version (blue). Gradually switch traffic from the blue environment to the green environment.
    
4. Database Replication: Use database replication techniques to create a second instance with the upgraded/downgraded version. Sync the database changes and switch the application to use the updated database without downtime.
    
5. Rolling Upgrades: Perform rolling upgrades, where you update one instance or component at a time, ensuring the application remains available throughout the process.
    
6. Health Checks and Monitoring: Implement health checks to ensure the system’s availability and monitor the process closely for any issues. Roll back immediately if anomalies are detected.
    

# **What is infrastructure as code and how do you use it?**

* Infrastructure as Code (IaC) is the practice of managing and provisioning infrastructure resources using machine-readable configuration files or scripts, rather than manual processes. It treats infrastructure as software code, enabling version control, automation, and reproducibility.
    
* Definition: Infrastructure as Code involves writing configuration files or scripts (e.g., using tools like AWS CloudFormation, Terraform, or Ansible) that define the desired state of infrastructure resources.
    
* Automation: IaC enables automated provisioning and management of infrastructure, eliminating the need for manual configuration and reducing human errors.
    
* Version Control: Infrastructure code can be versioned and stored in a version control system, allowing teams to collaborate, track changes, and roll back to previous versions if needed.
    
* Reproducibility: With IaC, infrastructure can be easily replicated across different
    
* environments, ensuring consistency and reducing discrepancies between development, testing, and production.
    
* Scalability: IaC simplifies scaling infrastructure resources by defining parameters and policies that can be adjusted programmatically, accommodating changes in workload or demand.
    

# **What is a load balancer? Give scenarios of each kind of balancer based on your experience.**

A load balancer is a device or service that distributes incoming network traffic across multiple servers or instances to ensure efficient utilization, high availability, and scalability.

* Application Load Balancer (ALB): ALBs operate at the application layer (Layer 7) of the OSI model. They provide advanced routing capabilities, such as URL-based routing, content-based routing, and support for HTTP/HTTPS protocols.
    
* Network Load Balancer (NLB): NLBs operate at the transport layer (Layer 4) and are designed for handling high volumes of traffic with ultra-low latency. They are ideal for TCP, UDP, and TLS traffic, making them suitable for use cases like gaming applications, and IoT applications.
    
* Classic Load Balancer (CLB): CLBs are the legacy load balancers provided by AWS. They operate at both Layer 4 and Layer 7 and offer basic load-balancing functionalities.
    

# **What is CloudFormation and why is it used for?**

* AWS CloudFormation is a service that allows you to define and provision infrastructure resources in a declarative manner using templates. It provides a way to automate the creation, configuration, and management of AWS resources.
    
* CloudFormation templates are written in YAML or JSON and describe the desired state of the infrastructure. By using CloudFormation, you can version control your infrastructure, reproduce it across environments, and easily manage complex architectures.
    
* It enables consistent and repeatable infrastructure deployments, simplifies resource dependencies, and streamlines the overall management of AWS resources.
    

# **Difference between AWS CloudFormation and AWS Elastic Beanstalk?**

* AWS CloudFormation is an infrastructure as a code service that automates the provisioning and management of AWS resources. It provides fine-grained control over infrastructure stacks, allowing you to define resources and manage dependencies in detail.
    
* AWS Elastic Beanstalk, on the other hand, is a platform as a service (PaaS) offering that simplifies the deployment and management of applications. It abstracts away the underlying infrastructure and provides a managed environment for running applications, handling resource provisioning and autoscaling automatically.
    

# **List possible storage options for Amazon EC2 instance.**

1. Amazon Elastic Block Store (EBS)
    
2. Amazon EC2 Instance Store
    
3. Amazon Elastic File System (EFS)
    
4. Amazon Simple Storage Service (S3)
    
5. Amazon Glacier
    

# **What are the kinds of security attacks that can occur on the cloud? And how can we minimize them?**

* Several security attacks can occur in the cloud environment:
    

1. Unauthorized Access: Attackers may attempt to gain unauthorized access to cloud resources and data.
    
2. Data Breaches: Breaches can occur when sensitive data is exposed or stolen from cloud storage or databases.
    
3. Distributed Denial of Service (DDoS): Attackers flood the cloud infrastructure with excessive traffic, causing services to become unavailable.
    
4. Insecure APIs: Vulnerabilities in APIs can be exploited to gain unauthorized access or manipulate cloud resources.
    
5. Insider Threats: Malicious insiders with privileged access can misuse or leak sensitive information.
    

* To minimize these attacks, follow security best practices:
    

1. Implement strong access controls, including strong passwords, multi-factor authentication, and least privilege principles.
    
2. Encrypt sensitive data in transit and at rest.
    
3. Regularly update and patch software and systems.
    
4. Monitor and log activities to detect and respond to security incidents.
    
5. Implement network security measures like firewalls and intrusion detection/prevention systems.
    
6. Regularly perform security assessments and audits.
    
7. Train employees on security awareness and best practices.
    

# **Can we recover the EC2 instance when we have lost the key?**

* If you have lost the key pair used to authenticate with an EC2 instance, you cannot recover or regain access to the instance using that key.
    
* However, you can still regain access to the instance by creating a new key pair and associating it with the instance. This can be done by creating an AMI of the instance, launching a new instance from the AMI, and specifying the new key pair during the launch process.
    

# **What is a gateway?**

* A gateway is a networking device or service that acts as an entry point or interface between different networks, enabling communication and data transfer. It serves as a bridge or connector, connecting different networks with different protocols or architectures.
    
* Gateways can perform various functions, such as routing, protocol translation, security enforcement, and network traffic management. They enable connectivity and interoperability between networks, allowing data to flow seamlessly between them.
    
* Gateways are commonly used in the context of the Internet, where they facilitate communication between local networks and the wider Internet, providing access to external resources and services.
    

# **What is the difference between Amazon Rds, Dynamodb, and Redshift?**

* Amazon RDS (Relational Database Service) is a managed service that allows you to run and scale relational databases like MySQL, PostgreSQL, Oracle, and SQL Server. It offers automated backups, replication, and patch management.
    
* DynamoDB is a fully managed NoSQL database service that provides fast and seamless scalability, ideal for applications requiring low-latency data access. It offers flexible schema design and automatic scaling based on demand.
    
* Redshift is a fully managed data warehousing service optimized for online analytic processing (OLAP). It enables high-performance querying and analysis of large datasets. Redshift is designed for data warehousing and analytics workloads, supporting SQL-based queries on structured data.
    

# **Do you prefer to host a website on S3? What’s the reason if your answer is either yes or no?**

* Hosting a website on Amazon S3 (Simple Storage Service) can be a viable choice for static websites due to its simplicity, scalability, and cost-effectiveness.
    
* S3 provides high availability, durability, and content delivery capabilities. However, for dynamic websites with server-side processing or advanced functionality, other services like AWS EC2, AWS Elastic Beanstalk, or AWS Lightsail may be more appropriate.
    

# **What is AWS Lambda and how does it work?**

* AWS Lambda is a serverless computing service that allows you to run your code without provisioning or managing servers.
    
* It follows an event-driven model, where your code is executed in response to events from various AWS services or custom triggers.
    
* Lambda functions can be written in several programming languages and can be designed to handle specific events or perform specific tasks.
    
* Lambda functions scale automatically and can run in parallel, ensuring high availability and efficient resource utilization. With Lambda, you pay only for the compute time consumed by your code.
    

# **Explain VPC (Virtual Private Cloud) and its components.**

VPC is a virtual network dedicated to your AWS account, providing a logically isolated section of the AWS cloud. It allows you to define a virtual network environment, including IP addressing, subnets, routing tables, security groups, and network gateways. The key components of a VPC include:

* Subnets: Segments of IP addresses within the VPC where resources can be provisioned.
    
* Route Tables: Define the rules for routing network traffic between subnets and the internet.
    
* Internet Gateway: Allows communication between instances in the VPC and the internet.
    
* NAT Gateway: Enables instances within private subnets to access the internet while remaining secure.
    
* Security Groups: Act as virtual firewalls to control inbound and outbound traffic to instances.
    
* Network Access Control Lists (NACLs): Additional layer of network security at the subnet level.
    

# **Explain AWS DevOps tools to build and deploy software in the cloud.**

* AWS Cloud Development Kit: It is an open-source software development framework for modeling and provisioning cloud application resources with popular programming languages.
    
* AWS CodeBuild: It is a continuous integration service that processes multiple builds and tests code with continuous scaling.
    
* AWS CodeDeploy: It helps to automate software deployments to any of the on-premises servers to choose from such as Amazon EC2, AWS Fargate, AWS Lambda, etc.
    
* AWS CodePipeline: It automates code received through continuous delivery for rapid and accurate updates.
    
* AWS CodeStar: It is a user interface that helps the DevOps team to develop, build, and deploy applications on AWS.
    
* AWS Device Farm: It works as a testing platform to test applications on different mobile devices and browsers.
    

# **What is offered under Migration services by Amazon?**

* Amazon Database Migration Service (DMS) is a tool for migrating data extremely fast from an on-premise database to Amazon Web Services cloud. DMS supports RDBMS systems like Oracle, SQL Server, MySQL, and PostgreSQL in on-premises and the cloud.
    
* Amazon Server Migration Services (SMS) helps in migrating on-premises workloads to Amazon web services cloud. SMS migrates the client’s server VMWare to cloud-based Amazon Machine Images (AMIs),
    
* Amazon Snowball is a data transport solution for data collection, machine learning, processing, and storage in low-connectivity environments.
    

# **What is offered under Messaging services by Amazon?**

* Amazon Simple Notification Service (SNS) is a fully managed, secured, available messaging service by AWS that helps decouple serverless applications, micro-services, and distributed systems. SNS can be started within minutes from either the AWS management console, command-line interface, or software development kit.
    
* Amazon Simple Queue Service (SQS) is a fully managed message queue for serverless applications, micro-services, and distributed systems. The advantage of SQS FIFO guarantees single-time processing and exact order sent by this kind of messaging service.
    
* Amazon Simple Email Service (SES) offers sending and receiving email services for informal, notify, and marketing correspondence via email for their cloud customers through the SMTP interface.
    

# **What is the purpose of making subnets?**

Subnets are designed to divide a large network into smaller networks. It will help reduce congestion by routing traffic which increases substantially.

# **A subnet is created and an EC2 instance is launched in the subnet with default settings, Explain, which options would be ready to use on the EC2 instance as soon as it is launched.**

* The best option would be Private IP which gets assigned as soon as it is launched.
    
* Public IP needs Internet Gateway and for new VPC, Gateway should be designed. Elastic IP will require manual setup.
    

# **What is Elastic Beanstalk?**

* Elastic Beanstalk is an orchestration service by AWS, used in various AWS applications such as EC2, S3, Simple Notification Service, CloudWatch, autoscaling, and Elastic Load Balancers.
    
* It is the fastest and simplest way to deploy your application on AWS using either AWS Management Console, a Git repository, or an integrated development environment (IDE).
    

# **What is Geo Restriction in CloudFront?**

Geo restriction, also known as geoblocking, prevents users in specific geographic locations from accessing content you’re distributing through a CloudFront web distribution.

# **What is the use of Amazon ElastiCache?**

Amazon ElastiCache is a web service that makes it easy to deploy, operate, and scale an in-memory data store or cache in the cloud.

# **Differentiate between stopping and terminating an instance.**

* When an instance is stopped, the instance performs a normal shutdown and then transitions to a stopped state.
    
* When an instance is terminated, the instance performs a normal shutdown. Then the attached Amazon EBS volumes are deleted unless the volume’s deleteOnTermination attribute is set to false.
    

# **Is it possible to change the private IP addresses of an EC2 while it is running/stopped in a VPC?**

The primary private IP address cannot be changed. Secondary private addresses can be unassigned, assigned, or moved between interfaces or instances at any point.

# **What is Sharding?**

* Sharding or horizontal partitioning is a scale-out technique for relational databases.
    
* This technique puts that data into smaller subsets and distributes them across physically separated database servers, where every server is called a database shard.
    
* These database shards have the same hardware, database engine, and data structure so that a similar level of performance is generated.
    

# **Which AWS services will you use to collect and process e-commerce data for near real-time analysis?**

Following are the AWS services that will be used to collect and process e-commerce data for near real-time analysis:

* Amazon DynamoDB
    
* Amazon ElastiCache
    
* Amazon Elastic MapReduce
    
* Amazon Redshift
    

# **What are the popular DevOps tools?**

The popular DevOps tools are:

* Chef, Puppet, Ansible, and SaltStack — Deployment and Configuration Management Tools
    
* Docker — Containerization Tool
    
* Git — Version Control System Tool
    
* Jenkins — Continuous Integration Tool
    
* Nagios — Continuous Monitoring Tool
    
* Selenium — Continuous Testing Tool
    

# **What are the features of Amazon Cloud search?**

Amazon Cloud search features:

* AutoComplete advice
    
* Boolean Searches
    
* Entire text search
    
* Faceting term boosting
    
* Highlighting
    
* Prefix Searches
    
* Range searches
    

# **How do you access the data on EBS in AWS?**

* Data cannot be accessible on EBS directly by a graphical interface in AWS. This process includes assigning the EBS volume to an EC2 instance.
    
* Here, when the volume is connected to any of the instances, either Windows or Unix, you can write or read on it. First, you can take a screenshot from the volumes with data and build unique volumes with the help of screenshots. Here, each EBS volume can be attached to only a single instance.
    

# **What are lifecycle hooks in AWS autoscaling?**

Lifecycle hooks can be added to the autoscaling group. It enables you to perform custom actions by pausing instances where the autoscaling group terminates and launches them. Every auto-scaling group consists of multiple lifecycle hooks.

# **What is a Hypervisor?**

A Hypervisor is a software used to create and run virtual machines. It integrates physical hardware resources into a platform distributed virtually to each user. Hypervisor includes Oracle Virtual Box, Oracle VM for x86, VMware Fusion, VMware Workstation, and Solaris Zones.

# **Explain the role of AWS CloudTrail.**

AWS CloudTrail is a service designed for monitoring and auditing actions of API calls. With AWS CloudTrail, the user can monitor and retain account activity connected with actions covering the AWS infrastructure.

# **Explain Amazon Route 53.**

Amazon Route 53 is defined as a scalable and highly available Domain Name System (DNS). It is created for the benefit of developers and companies to route end users to internet applications by translating names which is the most reliable and cost-effective process.

# **What are the parameters for S3 pricing?**

The following are the parameters for S3 pricing:

* Transfer acceleration
    
* Number of requests you make
    
* Storage management
    
* Data transfer
    
* Storage used
    

# **Name the different types of instances.**

Following are the different types of instances:

* Memory-optimized
    
* Accelerated computing
    
* Computer-optimized
    
* General-purpose
    
* Storage optimize
    

# **Name the database types in RDS.**

The following are the types of databases in RDS:

* MYSQL server
    
* Postgresql
    
* SQL Server
    
* Aurora
    
* Oracle
    
* MariaDB
    

# **What is CloudWatch?**

Amazon CloudWatch is a metrics repository. It allows you to monitor the complete stack, including applications, infrastructure, and services. You can also use alarms, logs, and event data to take automated actions and reduce the mean time to resolution (MTTR).

# **What are Key-Pairs in AWS?**

A key pair consists of a public key and a private key and is the secure login information for your virtual machines. Amazon EC2 stores the public key, and you can have the private key.

# **How many Subnets can you have per VPC?**

There are 200 Subnets per VPC.

In this blog, we’ve provided a comprehensive list of AWS interview questions and answers, covering key topics like cloud computing, AWS services, security, networking, and DevOps tools. These questions serve as a valuable resource for interview preparation.

If you have any questions or wish to share your experiences, please comment below. Don’t forget to connect with me on LinkedIn [Mudit Mathur.](https://www.linkedin.com/in/mudit--mathur/) for further discussions and corrections. #qna #interviewquestions #AWS #cloudcomputing #DevOps #technology #90daysofdevops