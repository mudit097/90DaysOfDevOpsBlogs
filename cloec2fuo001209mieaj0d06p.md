---
title: "Build a Grafana Dashboard"
datePublished: Tue Oct 31 2023 12:56:57 GMT+0000 (Coordinated Universal Time)
cuid: cloec2fuo001209mieaj0d06p
slug: build-a-grafana-dashboard
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1698756812049/e6882986-674c-4ed6-a4a9-7a7e7c8b2132.png
tags: blogging, aws, devops, 90daysofdevops, trainwithshubham

---

Welcome to an insightful journey exploring the essence and significance of dashboards in our technological landscape. Within this comprehensive blog, we delve into the vital role of dashboards, unraveling the underlying reasons for their necessity in today’s digital sphere. From dissecting the intrinsic need for dashboards to unveiling the myriad benefits of Grafana Dashboard, this compilation offers a comprehensive understanding of their pivotal role in modern systems.

Discover the immense value that Grafana Dashboards bring, as we navigate through their diverse benefits, understanding their power to transform and streamline data visualization. Uncover the intricacies of dashboard creation, and embark on a step-by-step guide to harness the full potential of Grafana in monitoring various elements such as error counts, Docker logs, Grafana logs, and Nginx logs. Join us in exploring how these dashboards serve as indispensable tools, providing insights and oversight critical to the smooth operation of complex systems.

# **1\. Why do we need Dashboard? 🤔**

1. **Data Visualization:** Dashboards present complex data sets visually, aiding comprehension and analysis.
    
2. **Real-Time Monitoring:** Dashboards provide up-to-date insights by connecting to live data sources, enabling proactive decision-making.
    
3. **Centralized Information:** They consolidate data from multiple sources into a single location, allowing easy access and monitoring of key metrics and KPIs.
    
4. **Data Exploration:** Dashboards offer interactive features for exploring and drilling down into data, revealing patterns and correlations.
    
5. **Performance Tracking:** They track performance against targets, benchmarks, or historical data, highlighting areas of success or improvement.
    
6. **Communication and Collaboration:** Dashboards facilitate sharing and discussion of data-driven insights, fostering collaboration and alignment.
    
7. **Decision-Making and Actionability:** Dashboards empower users to make informed decisions and take timely actions based on actionable insights derived from the data.
    

# **2\. Benefits of Grafana Dashboard 💡**

1. **Visual Variety:** Grafana provides a wide range of visualization options, allowing users to choose the most suitable type for their data.
    
2. **Customization:** Users can extensively customize their dashboards, adjusting colors, sizes, and labels to create personalized and branded visuals.
    
3. **Interactivity:** Grafana dashboards are highly interactive, enabling users to drill down, zoom in/out, and apply filters for detailed exploration.
    
4. **Real-Time Updates:** Dashboards can update in real time, providing immediate insights into changing data streams and time-sensitive metrics.
    
5. **Templating and Variables:** Users can use templates and variables for dynamic filtering and switching of data based on user-defined criteria.
    
6. **Alerting and Notifications:** Robust alerting capabilities help users set up thresholds and triggers, sending notifications for timely awareness of critical events.
    
7. **Plugin Ecosystem:** Grafana has a thriving community and plugin ecosystem, offering additional data sources, visualizations, and functionalities for enhanced dashboards.
    

# **3\. Dashboard Creation 🛠️**

1. Log in to Grafana and navigate to the dashboard section.
    
2. Click on “New Dashboard” to create a blank dashboard.
    
3. Add panels to your dashboard by clicking on “Add Panel” and selecting the desired visualization type.
    
4. Configure each panel by selecting the data source, defining queries, and customizing the visualization options.
    
5. Arrange the panels on the dashboard canvas to create the desired layout.
    
6. Customize the dashboard by adding titles, annotations, and variables.
    
7. Save the dashboard and give it a meaningful name.
    

# **4\. Monitor Error Count 🚨**

* Create a new Dashboard, now click on Add -&gt; Visualization -&gt;New Metrics add
    

![](https://miro.medium.com/v2/resize:fit:875/1*coTtxZrwGIllfWCQi-gYqQ.png align="left")

* In the Query editor below the graph, enter the details of the label and add a suitable title for the Panel.
    

```plaintext
  Labesl Filter ~> Job = varlogs
  line contains ~> error
  Rate ~> Count over time
```

![](https://miro.medium.com/v2/resize:fit:875/1*Cew-8-3I152GCZES9ICGqQ.png align="left")

* As all the details are filled in, click on “Run Queries” and then add the panel to the dashboard.
    

![](https://miro.medium.com/v2/resize:fit:875/1*tu9NdlVfbFHrzPn3tTrCUQ.png align="left")

# **5\. Monitor Docker Logs 🐳**

* For creating a panel for the Docker log, in the Query editor below the graph, enter the details of the label and add a suitable title for the Panel.
    

```plaintext
  Labesl Filter ~> Job = varlogs
  line contains ~> docker
```

![](https://miro.medium.com/v2/resize:fit:875/1*AgyO4GF8vk-t0mzBF-f_KQ.png align="left")

* As all the details are filled in, click on “Run Queries” and then add the panel to the dashboard.
    

# **6\. Monitor Grafana Logs 📊**

* To monitor the Grafana log so we have to add the Grafana directory path in the promtail configuration file.
    
* In the promtail-config.yaml add the Grafana job and log file location.
    

```plaintext
  - job_name: grafanalogs
    static_configs:
    - targets:
        - localhost
      labels:
        job: grafanalogs
        __path__: /var/log/grafana/*log
```

![](https://miro.medium.com/v2/resize:fit:875/1*mAXfzI_VO7T5Nn57xrJmYg.png align="left")

* Now restart the promtail container using the following Docker Command.
    

```plaintext
  docker ps

  docker restart <container_ID>
```

![](https://miro.medium.com/v2/resize:fit:875/1*XO_vO__5j_kU3sIyzfCN8g.png align="left")

* Now add the items in the Query for getting Grafana Logs enter the details of the label and add a suitable title for the Panel.
    

```plaintext
  Labesl Filter ~> Job = grafanalogs
  line contains ~> Request Completed
  Rate ~> Count over time

  # For getting Grafana error count chnage the line contains to "errors"
```

![](https://miro.medium.com/v2/resize:fit:875/1*mkP07acSi-4Up4538n58Kw.png align="left")

* As all the details are filled in, click on “Run Queries” and then add the panel to the dashboard.
    

![](https://miro.medium.com/v2/resize:fit:875/1*4nScHYv09NbdPSpHdFOqtw.png align="left")

# **7\. Monitor Nginx Logs 📜**

* To monitor the Nginx log so we have to add the Nginx directory path in the promtail configuration file.
    
* In the promtail-config.yaml add the Nginx job and log file location.
    

```plaintext
  - job_name: nginx
    static_configs:
    - targets:
        - localhost
      labels:
        job: nginxlogs
        __path__: /var/log/nginx/*log
```

![](https://miro.medium.com/v2/resize:fit:875/1*v0_kdVNdLJozGZJvgNprbA.png align="left")

* Now restart the Promtail container using the following Docker command:
    

```plaintext
  docker ps

  docker restart <container_ID>
```

* Now add the items in the Query for getting Nginx Logs enter the details of the label and add a suitable title for the Panel.
    

```plaintext
  Labesl Filter ~> Job = nginxlogs
  line contains ~> 404
  Rate ~> Count over time
```

![](https://miro.medium.com/v2/resize:fit:875/1*36E16OQchKdib5YgDl2iRA.png align="left")

* As all the details are filled in, click on “Run Queries” and then add the panel to the dashboard.
    
* There is no error from the Nginx server so “No Data” is showing up. Once there is a log containing a “404” error the count will be shown here in the Dashboard.
    

![](https://miro.medium.com/v2/resize:fit:875/1*y8_S0L73Wz4VhPdPLhjWyg.png align="left")

# **8\. Conclusion🌟**

In this blog, we’ve explored the world of dashboards and the power of Grafana. From understanding why dashboards are essential to the practical benefits of Grafana, we’ve equipped you with the knowledge to create your own dashboard and monitor error counts, Docker logs, Grafana logs, and Nginx logs effectively.

Now, armed with Grafana, you’re ready to become a monitoring expert. Experiment, fine-tune, and use Grafana to make data-driven decisions that enhance your systems and applications. If you have questions or need help, we’re here for you. Stay curious, stay vigilant, and keep monitoring with Grafana for smoother systems, better applications, and more insightful data.