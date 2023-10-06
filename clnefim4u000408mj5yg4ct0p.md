---
title: "Set up CloudWatch alarms and SNS topics in AWS"
datePublished: Fri Oct 06 2023 09:53:48 GMT+0000 (Coordinated Universal Time)
cuid: clnefim4u000408mj5yg4ct0p
slug: set-up-cloudwatch-alarms-and-sns-topics-in-aws
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696585921146/bc8b5631-4d14-4bf3-a92c-a43100c27710.png
tags: blogging, aws, devops, 90daysofdevops, trainwithshubham

---

What if you get an AWS bill for 100$ tomorrow morning once you wake up? Wouldn’t that be horrifying? So we need to monitor our usage and set up an alarm that will inform us whenever the bill touches a threshold. In this blog, we will learn how to set up CloudWatch alarms and SNS topics in AWS.

# **Amazon CloudWatch**

Amazon CloudWatch is a monitoring and observability service provided by Amazon Web Services (AWS). It allows you to collect and track metrics, collect and monitor log files, and set alarms on the metrics and logs.

Here’s the link to the official documentation of [Amazon CloudWatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html).

# **How Amazon CloudWatch works?**

![](https://miro.medium.com/v2/resize:fit:755/0*B_NeVOrasG3cC0gJ.png align="left")

1. Collect data: CloudWatch collects data from a variety of sources, including metrics, logs, and events.
    
2. Store data: CloudWatch stores the data it collects in a time series database.
    
3. Analyze data: CloudWatch provides a variety of tools and features that you can use to analyze your data, including dashboards, alarms, and Metrics Insights.
    
4. Visualize data: CloudWatch allows you to visualize your data using a variety of charts and graphs.
    
5. Take action: CloudWatch can help you to take action to resolve problems by sending notifications, triggering alerts, and automating remediation workflows.
    

# **Concepts of Amazon CloudWatch**

Here are some concepts related to Amazon CloudWatch:

* [Namespaces](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Namespace): A *namespace* is a container for CloudWatch metrics. Metrics in different namespaces are isolated from each other so that metrics from different applications are not mistakenly aggregated into the same statistics.
    
* There is no default namespace. The AWS namespaces typically use the following naming convention: `AWS/service`. For example, Amazon EC2 uses the `AWS/EC2` namespace.
    
* For the list of AWS namespaces, see [AWS services that publish CloudWatch metrics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/aws-services-cloudwatch-metrics.html).
    
* [Metrics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Metric): Metrics are fundamental to CloudWatch. They represent numerical data points collected at a specific time and are used to monitor the behavior and performance of AWS resources, applications, and custom services.
    
* Examples of metrics include CPU utilization, network traffic, or request latency. CloudWatch provides a wide range of pre-defined metrics for AWS services, and you can also create custom metrics.
    
* [Dimensions](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Dimension): A *dimension* is a name/value pair that is part of the identity of a metric. You can assign up to 30 dimensions to a metric.
    
* [Resolution](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Resolution_definition): Each metric is one of the following:
    
* The standard resolution, with data having a one-minute granularity
    
* High resolution, with data at a granularity of one second
    
* [Statistics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Statistic): *Statistics* are metric data aggregations over specified periods. CloudWatch provides statistics based on the metric data points provided by your custom data or provided by other AWS services to CloudWatch
    
* [Percentiles](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Percentiles): A *percentile* indicates the relative standing of a value in a dataset. For example, the 95th percentile means that 95 percent of the data is lower than this value and 5 percent of the data is higher than this value. Percentiles help you get a better understanding of the distribution of your metric data.
    
* [Alarms](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#CloudWatchAlarms): Alarms allow you to set thresholds on metrics and define actions to be triggered when those thresholds are breached. When an alarm enters the ALARM state, it can initiate actions like sending notifications, scaling AWS resources, or executing an AWS Lambda function. Alarms help you proactively respond to incidents or take automated actions based on specific conditions.
    

# **Amazon SNS**

Amazon SNS (Simple Notification Service) is a fully managed messaging service provided by Amazon Web Services (AWS).

It enables you to send messages or notifications to various endpoints, such as email, SMS, mobile push notifications, or even HTTP endpoints, in a flexible and scalable manner.

![](https://miro.medium.com/v2/resize:fit:875/0*-lzZj1fA_pPup2of.png align="left")

# **Tasks**

# **Task 1: Create a CloudWatch alarm that monitors your billing and sends an email to you when it reaches $2.**

First, we will need to enable the Billing Preferences.

Go to AWS Management Console &gt; Search & Navigate to Billing Service &gt; In the left navigation pane, under Preferences click on Billing Preferences.

![](https://miro.medium.com/v2/resize:fit:393/0*O8IvhEP8tU19fruR align="left")

Under Invoice delivery preferences &gt; Click on edit &gt; Checkbox for PDF invoices delivered by email &gt; Click on Update &gt; Under Alert preferences &gt; Checkbox for Receive AWS Free Tier alerts and Receive CloudWatch billing alerts.

![](https://miro.medium.com/v2/resize:fit:875/0*KjdZUC_3_eL2mHaz align="left")

Now let us go ahead and create the CloudWatch alarm.

Go to AWS Management Console &gt; Search & Navigate to Cloudwatch Service &gt; In the left navigation pane, click on Alarms &gt; Click on Create Alarm.

![](https://miro.medium.com/v2/resize:fit:875/1*6PGwEFCODNuY7oZI_j4Aog.png align="left")

*Step 1: Select metric*

Select Metric &gt; Search “Billing” &gt; Select Total Estimated Charge

![](https://miro.medium.com/v2/resize:fit:875/0*9q9yHNRSUBjiw7F5 align="left")

Go to Graphed Metrics &gt; Set Statistic as Maximum &gt; For Period choose 6 hours

![](https://miro.medium.com/v2/resize:fit:875/0*OdyQ4yygP6QNfqYI align="left")

Under Conditions &gt; Select Threshold type as Static &gt; Select Whenever EstimatedCharges is… as Greater &gt; Give 2 USD for than… &gt; Click on Next.

![](https://miro.medium.com/v2/resize:fit:875/0*kCkd87CitDW15UYi align="left")

*Step 2: Configure actions*

Under Notifications:

For the Alarm state trigger select In alarm &gt; Create New Topic &gt; Create a topic with your mail ID and topic name.

![](https://miro.medium.com/v2/resize:fit:875/0*D--Yugntfx4waN8j align="left")

Click on Next.

*Step 3: Add name and description*

For the Alarm name give MyBillingAlarm &gt; Click on Next.

![](https://miro.medium.com/v2/resize:fit:875/0*k48Mg6gAw_C1rjab align="left")

*Step 4: Preview and create*

Preview the Alarm you have created and click on Create Alarm.

Confirm the subscription to receive the Amazon SNS.

![](https://miro.medium.com/v2/resize:fit:875/1*a6mERftVfKXAXfL_mnT2yQ.png align="left")

And yes! We have successfully set up the CloudWatch Service.

# **Task 2: Delete the billing Alarm that you created now.**

Go to AWS Management Console &gt; Navigate to the CloudWatch service &gt; In the left navigation pane, click on “Alarms” &gt; Select the Billing Alarm you want to delete &gt; Click on Actions &gt; And choose Delete.

![](https://miro.medium.com/v2/resize:fit:875/1*a6mERftVfKXAXfL_mnT2yQ.png align="left")

You can see that the Alarm was deleted successfully.

![](https://miro.medium.com/v2/resize:fit:875/0*t_enpXZMRNsEp1S9 align="left")

In this blog, I have discussed how to set up CloudWatch alarms and SNS topics in AWS. If you have any questions or want to share your experiences, please comment below. Don’t forget to read my blogs and connect with me on LinkedIn and let’s have a conversation.

To help me improve my blog and correct my mistakes, I am available on LinkedIn as [Mudit Mathur.](https://www.linkedin.com/in/mudit--mathur/) Do reach me and I am open to suggestions and corrections.

#Day46 #90daysofdevops