---
title: "Sending Docker Logs to Grafana"
datePublished: Sun Oct 29 2023 07:57:58 GMT+0000 (Coordinated Universal Time)
cuid: clob6i8b500040akzd6bdeikc
slug: sending-docker-logs-to-grafana
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1698566213660/633f0ab8-f85e-4ff5-98e1-b3b4513f9bf4.png
tags: blogging, aws, devops, 90daysofdevops, trainwithshubham

---

In this blog, we embarked on an illuminating journey into Grafana and Loki, discovering their installation, setup, and integration for robust monitoring and visualization.

We learned how to install and start Grafana, set up Loki and Promtail via Docker, and configure Loki as a data source in Grafana.

Armed with these insights, you’re now well-prepared to navigate the world of efficient data visualization and comprehensive system monitoring. Stay tuned for more exciting explorations in our upcoming blogs!

# **Install & Start Grafana**

For the installation of Grafana, please follow my Day 73,74 Blog “Grafana Installation.” [Grafana Installation](https://muditm12.hashnode.dev/grafana-installation)

# **Install Loki & Promtail using Docker**

* Before installing Loki & Promtail make sure you have docker installed in your instance.
    

```plaintext
  sudo apt-get update
  sudo apt-get install docker.io -y

  # Giving docker permission to current user
  sudo usermod -aG docker $USER
  sudo reboot

  # Verify Docker version
  docker --version
```

![](https://miro.medium.com/v2/resize:fit:875/1*83NMQI3Dv-DCHV4MTqgu6w.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*zCo58jiM1H8_OMtqaSkIng.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*y3RUpF2JzqCb9k1EqnMaKA.png align="left")

* Download the Loki Config file into your current directory.
    

```plaintext
wget https://raw.githubusercontent.com/grafana/loki/v2.8.0/cmd/loki/loki-local-config.yaml -O loki-config.yaml
```

![](https://miro.medium.com/v2/resize:fit:875/1*xQdTB6OE70a-VHFLVfjG3A.png align="left")

* Run the Loki container using the following Docker command.
    

```plaintext
docker run -d --name loki -v $(pwd):/mnt/config -p 3100:3100 grafana/loki:2.8.0 --config.file=/mnt/config/loki-config.yaml
```

![](https://miro.medium.com/v2/resize:fit:875/1*30FxYFpjZposcCd1kRl3Ng.png align="left")

* We can verify Loki is running using the docker container by using the following Docker command :
    

```plaintext
  docker ps
```

![](https://miro.medium.com/v2/resize:fit:875/1*2MYwlVjAfeUNa5pu2K1uvg.png align="left")

* Now to access Loki, Go to the Security Group of your EC2 instance and add port 3100.
    

![](https://miro.medium.com/v2/resize:fit:875/1*rxEwBbYC98O_jc3TWxpyUw.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*zdh4Es87CVcGXHfku3BOeA.png align="left")

* We can see Loki’s metrics using the IPv4 address followed by port 3100 and metrics.
    

```plaintext
  http://<public_ipV4>:3100/metrics
```

![](https://miro.medium.com/v2/resize:fit:875/1*lGrAGUUNoj0ti9juhAMRSQ.png align="left")

* To verify whether Loki is ready or not, access the IPv4 address followed by port 3100 and ready.
    

```plaintext
  http://public_ipV4:3100/ready
```

![](https://miro.medium.com/v2/resize:fit:875/1*XoYgs0EXXRDx--F9N-QU4Q.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*zDvMSUd25R_3ogU6I-h8Jw.png align="left")

* Now download the Promtail Config yaml file into your directory by using the following command:
    

```plaintext
wget https://raw.githubusercontent.com/grafana/loki/v2.8.0/clients/cmd/promtail/promtail-docker-config.yaml -O promtail-config.yaml
```

![](https://miro.medium.com/v2/resize:fit:875/1*AvLiab7_65wXtu9po_TuaQ.png align="left")

* We can verify Promtail configuration file is there in the directory by using the following command:
    

```plaintext
  ls

  cat promtail-config.yaml
```

![](https://miro.medium.com/v2/resize:fit:875/1*elttG-N7Tg00NQ1Qtzl2ew.png align="left")

* Now execute the Promtail container by using the following Docker command:
    

```plaintext
  docker run -d --name promtail -v $(pwd):/mnt/config -v /var/log:/var/log --link loki grafana/promtail:2.8.0 --config.file=/mnt/config/promtail-config.yaml
```

![](https://miro.medium.com/v2/resize:fit:875/1*-klNpav8_9maRMSr78MWHw.png align="left")

* We can verify both Loki and Promtail are running using `docker ps` command.
    

![](https://miro.medium.com/v2/resize:fit:875/1*1K7Hhg_Bae8sXNs1R8neag.png align="left")

# **Configure Loki as a Data Source**

* Once both Loki and Promtail are configured in the instance, Login to the Grafana Home Page
    

![](https://miro.medium.com/v2/resize:fit:875/1*BuNeSKlX6jTRDBIqEUnDWQ.png align="left")

* In the navigation drawer either there is DataSource click on it or you can get it by clicking on the left hamburger menu, hovering over there is a gear icon (second last one) and clicking on “Data Sources”.
    

![](https://miro.medium.com/v2/resize:fit:476/0*lEVrm9WeCOMznJtl align="left")

* Click on “Add data source” and search for “Loki”. Click on it.
    

![](https://miro.medium.com/v2/resize:fit:875/1*JAhH3U3dzjgfTprkO77-_Q.png align="left")

* As the Loki prompt is opened fill in the details like Name and in the HTTP provide the URL i.e, [http://127.0.0.1:3100](http://127.0.0.1:3100)
    

![](https://miro.medium.com/v2/resize:fit:875/1*Y3wmp1fYiQvmXEjnCKFCZw.png align="left")

* Click on “Save and Test”. You will get a prompt saying “Data Source Successfully Connted” so you can conclude that your connection to Grafana using Loki and Promtail is successful.
    
* Now click on Explore to create metrics.
    

![](https://miro.medium.com/v2/resize:fit:875/1*Y3wmp1fYiQvmXEjnCKFCZw.png align="left")

* We will create metrics that will show logs containing Docker in it.
    

```plaintext
  Name -> System Generated Logs
  Label Filters -> jobs, varlogs
  Line Contains -> docker
```

![](https://miro.medium.com/v2/resize:fit:875/1*R-fr-AidowmHUsALzZNB2g.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*-FGrzyvzdNiYt72ia3WTsA.png align="left")

* Once you get the output we can put the result into a new dashboard, before that named it.
    

![](https://miro.medium.com/v2/resize:fit:875/1*4Bu6DCpwiws1PoF-Z18i3g.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*WrjunO-TjkERm-XAB0Ck3w.png align="left")

Thanks for delving into Grafana, Loki, and Promtail through Docker installation! Now equipped with powerful monitoring tools, from Grafana setup to Loki and Promtail configuration, you’re ready for efficient system monitoring and visualization. Let’s stay connected on ([https://www.linkedin.com/in/mudit--mathur/](https://www.linkedin.com/in/mudit--mathur/)) for more insights, discussions, and your valuable feedback as we explore further topics. Keep exploring, keep monitoring, and keep innovating!