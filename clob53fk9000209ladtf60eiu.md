---
title: "Grafana Installation"
datePublished: Sun Oct 29 2023 07:18:28 GMT+0000 (Coordinated Universal Time)
cuid: clob53fk9000209ladtf60eiu
slug: grafana-installation
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1698563848993/7146fbec-2c87-4a12-ad7f-a75598a3093b.png
tags: blogging, aws, monitoring, 90daysofdevops, trainwithshubham

---

In this section, we delve into the comprehensive process of deploying Grafana within an AWS EC2 instance. Grafana stands as an essential data visualization and monitoring tool, pivotal for interpreting and managing diverse datasets. Our guide offers a step-by-step walkthrough, allowing users to harness the potential of Grafana’s user-friendly interface for creating insightful dashboards and analyzing metrics effectively.

# **1\. Setup Grafana in your AWS EC2 Instance**

* Go to the AWS console and Launch an EC2 instance for Grafana.
    

![](https://miro.medium.com/v2/resize:fit:875/1*HLyTNOH22VjA6O18KpiyUA.png align="left")

* Once the instance is launched, you can SSH into the instance.
    

![](https://miro.medium.com/v2/resize:fit:875/1*ipOD27sdC5ZhjJmVABAl7Q.png align="left")

* To install the required packages and download the Grafana repository signing key, run the following commands: [Know More about Grafana Installation](https://grafana.com/docs/grafana/latest/setup-grafana/installation/)
    

```plaintext
  sudo apt-get install -y apt-transport-https
  sudo apt-get install -y software-properties-common wget

  # Getting the key
  sudo wget -q -O /usr/share/keyrings/grafana.key https://apt.grafana.com/gpg.key
```

![](https://miro.medium.com/v2/resize:fit:875/1*Dowb9MTWFgXY_uC_NVU6_g.png align="left")

* To add a repository for stable releases, run the following command:
    

```plaintext
  echo "deb [signed-by=/usr/share/keyrings/grafana.key] https://apt.grafana.com stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
```

![](https://miro.medium.com/v2/resize:fit:875/1*AiQjnSr1ZTXpVhFGHy5sgA.png align="left")

* To add a repository for beta releases, run the following command:
    

```plaintext
  echo "deb [signed-by=/usr/share/keyrings/grafana.key] https://apt.grafana.com beta main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
```

![](https://miro.medium.com/v2/resize:fit:875/1*LINeNJM7Ycjn0lY62j0gYw.png align="left")

* Run the following command to update the list of available packages:
    

```plaintext
  sudo apt-get update
```

![](https://miro.medium.com/v2/resize:fit:875/1*ynSYN_OCSaHGIhaI_KpIpw.png align="left")

* To install Grafana OSS, run the following command:
    

```plaintext
  sudo apt-get install grafana
```

![](https://miro.medium.com/v2/resize:fit:875/1*FPrP4yasONKs9RW5Z9ICWw.png align="left")

* Start and Enable the grafana-server
    

```plaintext
  #Start Grafana-Server
  sudo systemctl start grafana-server

  #Enable the Grafana-Server
  sudo systemctl enable grafana-server

  #Check the status of grafana
  sudo systemctl status grafana-server
```

![](https://miro.medium.com/v2/resize:fit:875/1*LcpK5-RtbsNMrtzn1sW97w.png align="left")

* Open port 3000 in your EC2 instance’s security group to allow external access to Grafana.
    

![](https://miro.medium.com/v2/resize:fit:875/1*pLo20kT-CqU1HPLxQeoX9Q.png align="left")

* Once the port is enabled you can access the Grafana Dashboard by using a public IPv4 address followed by Grafana port 3000.
    

![](https://miro.medium.com/v2/resize:fit:875/1*uGIytvZ76i_OPcUQLScZUA.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*qGsvK7tcOsWicQgZe_awdw.png align="left")

* By default, Grafana credentials are *username=admin and password=admin*. Using this password change prompt will come.
    

![](https://miro.medium.com/v2/resize:fit:875/1*cWnJv6LxQ_1ZIaZECajL6w.png align="left")

* Change the password, you will be logged into Grafana Dashboard
    

![](https://miro.medium.com/v2/resize:fit:875/1*D2octFRFZId6TKEPUJQE3A.png align="left")

* As the password has been changed you are now Logged In to Grafan HomePage.
    

![](https://miro.medium.com/v2/resize:fit:875/1*MeQBcdW_HWOsDV-CvpAk5A.png align="left")

Thank you for exploring the deployment process of Grafana on an AWS EC2 instance with us. Grafana’s significance in data visualization and monitoring is immense, and our guide provides a step-by-step approach for leveraging its user-friendly interface to create insightful dashboards and effectively analyze metrics. For any feedback or further discussions on improvement, I welcome you to connect with me on **LinkedIn** ([https://www.linkedin.com/in/mudit--mathur/](https://www.linkedin.com/in/mudit--mathur/)). Your input and experiences are valuable, and I’m open to continuous learning and growth together.