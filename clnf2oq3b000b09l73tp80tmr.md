---
title: "Test Knowledge on AWS"
datePublished: Fri Oct 06 2023 20:42:25 GMT+0000 (Coordinated Universal Time)
cuid: clnf2oq3b000b09l73tp80tmr
slug: test-knowledge-on-aws
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696624759175/653760c9-7033-4e65-b1c6-611527468acd.png
tags: blogging, aws, devops, 90daysofdevops, trainwithshubham

---

In this blog, we will be testing the AWS knowledge on services provided by AWS.

Let’s dive right into tasks.

# **Task 1: Launch an EC2 instance using the AWS Management Console and connect to it using SSH. Install a web server on the EC2 instance and deploy a simple web application. Monitor the EC2 instance using Amazon CloudWatch and troubleshoot any issues that arise.**

## **Launch an EC2 instance using the AWS Management Console and connect to it using SSH**

Go to AWS Management Console &gt; Search and navigate to EC2 &gt; Click on Launch Instances &gt; Give the name of your EC2 (here it is test-aws) &gt; Select the AMI (Ubuntu here)

![](https://miro.medium.com/v2/resize:fit:875/1*kF7cBFDCwi8i3KxY9EJRiA.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*Y4f5aueE3VdR_-wMU9iTJg.png align="left")

\\&gt; Let the Instance type be default &gt; Create new Key Pair if you don’t have or else select the one you have

![](https://miro.medium.com/v2/resize:fit:875/1*y1OnJFXkTg0lrBzDTCVixw.png align="left")

\\&gt; Under Network Settings check the box for both “Allow HTTPS traffic from the Internet” and “Allow HTTP traffic from the Internet” &gt; Under Summary click on Launch Instances.

![](https://miro.medium.com/v2/resize:fit:875/1*cHOz22aSSzpVpXWESy3lKg.png align="left")

You should be able to see the Instances in the EC2 instances console, up and running within 1 to 2 mins.

![](https://miro.medium.com/v2/resize:fit:875/1*_quwlzeMVK2selxJ52iN9Q.png align="left")

Select the instance and click on connect &gt; Go to the SSH Client tab & copy the command to connect to your instance via SSH &gt; In your command line, where your key-pair file is present run the command to get connected to the instance.

![](https://miro.medium.com/v2/resize:fit:875/1*cfnezTKQFd11Vth8RSJSqQ.png align="left")

# **Install a web server on the EC2 instance and deploy a simple web application.**

Update the instance with the latest packages and security patches, using:

```plaintext
sudo apt-get update -y
```

![](https://miro.medium.com/v2/resize:fit:875/1*v0Ggr_QFSV1sDRlKjfeCww.png align="left")

Let us install an Apache web server, using:

```plaintext
sudo apt-get install apache2 -y
```

![](https://miro.medium.com/v2/resize:fit:875/1*xIeKkBoxFdlBNV52oXzbFA.png align="left")

Let us start this service using:

```plaintext
sudo systemctl start apache2
sudo systemctl status apache2
```

![](https://miro.medium.com/v2/resize:fit:875/1*M2KPRrAv1xWL62n0QghguA.png align="left")

Let us try connecting to this Web server using the Public IPv4 of the instance.

![](https://miro.medium.com/v2/resize:fit:875/1*WUl0HJKgCfrDNNtiNcV8bw.png align="left")

And yes! We can connect to the server!

Let us deploy a sample application on this server.

Go to the /var/www/html directory where the index.html file is present.

```plaintext
cd /var/www/html
ls
```

![](https://miro.medium.com/v2/resize:fit:875/1*k4zeMzb4YHKRNqQCslEQmg.png align="left")

Replace the contents of the index.html file with:

```plaintext
<!DOCTYPE html>
<html>
<head>
<title>New Application - Apache</title>
</head>
<body>
<h1>Hello, world! This is my sample application</h1>
<h2>I am a DevOps Enthusiast</h2>
</body>
</html>
```

![](https://miro.medium.com/v2/resize:fit:875/1*pgBjd77O958sarxEkzusNA.png align="left")

Restart the web server using the:

```plaintext
sudo systemctl restart apache2
```

And using the Public IPv4 of the Instance, you can verify that you have successfully deployed:

![](https://miro.medium.com/v2/resize:fit:875/1*MKNcXq5a1THf8o9zxNNZqw.png align="left")

# **Monitor the EC2 instance using Amazon CloudWatch and troubleshoot any issues that arise**

To use the CloudWatch service, you should enable a few important things in the Billing preferences. Here’s the link on how to do the [same.](https://muditm12.hashnode.dev/set-up-cloudwatch-alarms-and-sns-topics-in-aws)

In your EC2 Console &gt; Select the Instance you want to monitor &gt; Go to the Monitoring Tab &gt; Click on Manage Detailed Monitoring.

![](https://miro.medium.com/v2/resize:fit:875/1*YLS9Y36XtUcuqp3m976o4w.png align="left")

Enable the Detailed Monitoring in the pop-up and click on Confirm.

![](https://miro.medium.com/v2/resize:fit:875/1*YpuNzDHvYuMZ5Z9D-4kWdQ.png align="left")

Once done, Navigate to CloudaWatch &gt; Metrics &gt; All Metrics &gt; Select EC2

![](https://miro.medium.com/v2/resize:fit:875/1*WITSa3nugnj-EwWez6GbVQ.png align="left")

Click on Per-Instance Metrics &gt; And select the Metrics you want to monitor &gt; I am selecting CPU Utilization.

![](https://miro.medium.com/v2/resize:fit:875/1*z8J_bsisIqKhkMBpGNfttg.png align="left")

Now let us create the Alarm.

Go to Alarms &gt; All Alarms &gt; Create Alarm &gt; Select Metric &gt; Select EC2 &gt; Select Per Instance Metrics &gt; Select the CPU Utilization &gt; Click on Select Metric

![](https://miro.medium.com/v2/resize:fit:875/1*87M9sg25K8A4ffi-mvlZfA.png align="left")

Under conditions, select the Threshold value to be greater than 50 &gt; Click on Next.

![](https://miro.medium.com/v2/resize:fit:875/0*Jl26ZTOcT1AmalRK align="left")

Set up the SNS topic and create an alarm. I am naming test-alarm.

![](https://miro.medium.com/v2/resize:fit:875/0*ZHpMcZa4XJ3XUo7F align="left")

So when you go beyond the threshold, you will receive an alarm.

# **Task 2: Create an Auto Scaling group using the AWS Management Console and configure it to launch EC2 instances in response to changes in demand. Use Amazon CloudWatch to monitor the performance of the Auto Scaling group and the EC2 instances and troubleshoot any issues that arise. Use the AWS CLI to view the state of the Auto Scaling group and the EC2 instances and verify that the correct number of instances are running.**

## **Create an Auto Scaling group using the AWS Management Console and configure it to launch EC2 instances in response to changes in demand**

Let us Create a Launch Template from our existing EC2 instance.

Go to EC2 Console &gt; Select the EC2 Instance &gt; Actions &gt; Image and templates &gt; Create a template from the instance.

![](https://miro.medium.com/v2/resize:fit:875/1*yjFJQWO_OUQYHCwPD_48GQ.png align="left")

Let the Launch template name be new-test-template &gt; Template version description be “Template test launch template” &gt; Click on Create launch template

![](https://miro.medium.com/v2/resize:fit:875/1*EJV8rZZBanfj2XxfA0mrXg.png align="left")

You can verify the template created when it appears in the dashboard:

![](https://miro.medium.com/v2/resize:fit:875/1*cDSrioT9J4D0teZg29LBNw.png align="left")

Go to your EC2 console &gt; Under Auto Scaling &gt; Select Auto Scaling Groups &gt; Create Auto Scaling Groups &gt;

Auto Scaling group name: test-ASG

Launch template: Select the launch template you created

![](https://miro.medium.com/v2/resize:fit:875/1*1maJL4w1w6-ZU1bK4QQi1A.png align="left")

Click on Next.

In the next section &gt; Select a couple of availability zones &gt; Click on Next &gt; Enable Monitoring &gt; Click on Next

![](https://miro.medium.com/v2/resize:fit:875/1*A3QidFwpzeuDTbYBbcSZjg.png align="left")

Set the Group size as per your requirement:

![](https://miro.medium.com/v2/resize:fit:875/1*3sgoqabfA3bkf_BZ_srddA.png align="left")

Select Target Tracking Policy &gt; Click on Next

![](https://miro.medium.com/v2/resize:fit:875/1*N4pfuYlakox-G2luNCzvyQ.png align="left")

Preview and Create the ASG.

![](https://miro.medium.com/v2/resize:fit:875/1*TZcRUyjRnMFP6asZSRjXlA.png align="left")

In the EC2 Instances dashboard, you can see that the number of instances is increased to three (as per your requirement).

![](https://miro.medium.com/v2/resize:fit:875/1*rLw-xPRv7M34HwKa1OEpRg.png align="left")

# **Use Amazon CloudWatch to monitor the performance of the Auto Scaling group and the EC2 instances and troubleshoot any issues that arise**

You can see that the Target tracking policy has created two more alarms:

![](https://miro.medium.com/v2/resize:fit:875/1*w2KE1YG5cD90VX268HEikg.png align="left")

Go to the ASG we created &gt; Enable ASG Metric.

![](https://miro.medium.com/v2/resize:fit:875/1*TZcRUyjRnMFP6asZSRjXlA.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*qTzjUHdxP7WbLDs9HeLpkA.png align="left")

Let us create an Alarm for the same ASG.

![](https://miro.medium.com/v2/resize:fit:450/0*s7faLC6nCBb_dPD0 align="left")

# **Use the AWS CLI to view the state of the Auto Scaling group and the EC2 instances and verify that the correct number of instances are running.**

SSH to your instance and install the AWS CLI using:

```plaintext
sudo apt update
sudo apt-get install awscli
aws --version
```

![](https://miro.medium.com/v2/resize:fit:875/1*rNe0OVd2dJmx6Oc4iHCScg.png align="left")

Configure your AWS CLI with Access Key ID and Secret Access Key.

```plaintext
aws configure
```

![](https://miro.medium.com/v2/resize:fit:875/1*KTPHhw-tBf9TRSht9FWZzg.png align="left")

Let us see the ASGs by using the:

```plaintext
aws autoscaling describe-auto-scaling-groups
```

![](https://miro.medium.com/v2/resize:fit:875/1*0AqfF9m1m5m2IN2iXGlZAQ.png align="left")

Let us verify the ec2 instances:

```plaintext
aws ec2 describe-instances
```

![](https://miro.medium.com/v2/resize:fit:875/1*n78kvjhax6t2XtoROq6kig.png align="left")

By running this command below, you can check the instances that are there:

```plaintext
aws ec2 describe-instances | grep -w "KeyName"
```

![](https://miro.medium.com/v2/resize:fit:875/1*ebWUT_7-dlmD8VIu-U0-FA.png align="left")

We can verify that there are 3 Instances from the EC2 console:

![](https://miro.medium.com/v2/resize:fit:875/1*zFgxFJRwH0-ujyi09VHiiA.png align="left")

In this blog, I have tested my knowledge of AWS services which I have used previously in the challenge. If you have any questions or want to share your experiences, please comment below. Don’t forget to read my blogs and connect with me on LinkedIn and let’s have a conversation.

To help me improve my blog and correct my mistakes, I am available on LinkedIn as [Mudit Mathur.](https://www.linkedin.com/in/mudit--mathur/) Do reach me and I am open to suggestions and corrections.

#Day47 #90daysofdevops