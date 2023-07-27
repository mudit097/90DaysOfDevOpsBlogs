---
title: "Day 8 of #90daysofdevops Basic Git & GitHub for DevOps Engineers"
datePublished: Thu Jul 27 2023 20:54:41 GMT+0000 (Coordinated Universal Time)
cuid: clklmv0m8000409mtgkszadgk
slug: day-8-of-90daysofdevops-basic-git-github-for-devops-engineers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690491181418/1c65a986-f279-4ed2-a608-be99354252e7.webp
tags: github, version-control, git, devops, 90daysofdevops

---

# **1\. Introduction**

Welcome to Day 8 of our exhilarating #90DaysOfDevOps journey! Today, we’re venturing into the dynamic realm of Git and GitHub. 🚀 Get ready to harness the true potential of version control as we delve into the magic of Git and its profound impact on software development. Unveil the wonders of GitHub, where collaboration and knowledge-sharing converge in a single platform. 📚 Throughout this blog, we’ll unlock the essence of distributed version control and its remarkable advantages over traditional centralized systems. So, roll up your sleeves as we take a hands-on approach, installing Git, creating a GitHub account, and mastering the art of repository creation and cloning. 💻🐙 Are you prepared to elevate your DevOps expedition with the powerful tools of Git and GitHub? Let’s set forth on this incredible journey together! 🌟

## **1.1 What is Git?**

Git, a distributed version control system, is an essential tool for software development, acting like a time machine that lets you save snapshots of your project at various stages. This allows you to revisit any previous state, facilitating error recovery and code history analysis. Let’s illustrate the advantages of Git with a real-time scenario:

Imagine you and your team are working on a group project, with each member responsible for different parts of the codebase. Without Git, you encounter several challenges:

1\. Overwriting Changes: As multiple team members work concurrently, there’s a risk of overwriting each other’s changes. This could lead to conflicts and data loss, making it difficult to reconcile different versions of the code. 😬🔄

2\. Tracking Changes: Without a version control system like Git, it becomes challenging to keep track of who made which changes and when. This lack of visibility hampers progress tracking, bug identification, and accountability. 📝🔍

3\. Collaboration Complexity: With a shared codebase, coordinating changes and updates can become overwhelming. Without a systematic way to merge and manage code, the development process may become chaotic. 🤝🗂️

Now, let’s see how Git resolves these issues:

1\. Branching: Git allows each developer to work on their code in separate branches. This way, changes are isolated from the main codebase until they are tested and ready to be merged. This prevents overwriting and conflicts, as changes can be carefully integrated. 🌿🔄

2\. History Tracking: Git maintains a detailed history of all changes made to the project. Developers can see who made which changes, along with commit messages explaining the purpose of those changes. This transparency facilitates bug tracking, accountability, and collaboration. 🕰️📝

3\. Merging and Pull Requests: Git offers a streamlined process for integrating changes from different branches into the main codebase. Pull requests allow team members to review each other’s code before merging, reducing the risk of errors and ensuring better collaboration. 🔄🤝

In summary, Git’s ability to streamline collaboration, track changes effortlessly, and manage code history makes it an indispensable tool for developers and projects of all scales. With Git’s features, you and your team can work more efficiently, avoid conflicts, and maintain a reliable and well-documented codebase. 🚀💻

## **1.2 What is GitHub?**

GitHub is an online service and platform designed to facilitate seamless collaboration among developers, making it easier to work together on coding projects and manage source code effectively.

Key aspects of GitHub include:

1\. Code Repositories: GitHub organizes code into “repositories” (or “repos”). These repositories act as folders where developers store their code and project files, enabling organized and structured code management. 🗂️

2\. Collaboration: The platform fosters collaboration by allowing multiple developers to work on the same project simultaneously. By “cloning” the repository to their local machines, developers can make changes and then “push” these modifications back to GitHub, ensuring a centralized and up-to-date codebase. 👥

3\. Version Control: GitHub employs the powerful version control system called “Git,” which enables precise tracking of code changes. Developers can easily revert to previous versions if required and trace the authors of specific modifications. 🔀📜

4\. Issues and Pull Requests: Communication and project improvement are facilitated through “issues” and “pull requests.” Developers can report problems, suggest changes, or propose enhancements to the codebase, thereby promoting effective problem-solving and teamwork. 📝✉️

5\. Community and Learning: GitHub serves as more than just a code-sharing platform; it is a vibrant community. Developers can learn from each other’s code, participate in open-source projects, and collaborate on exciting initiatives. The platform encourages a culture of knowledge sharing and mutual growth. 🌐🤝

## **1.3 What is Version Control? What types of version controls**

I’ve described version control systems accurately! Both Centralized Version Control system (CVCS) and Distributed Version Control System (DVCS) serve the purpose of keeping track of changes in files over time and enabling collaboration among developers. However, they differ in their approach and architecture.

1\. Centralized Version Control System (CVCS):  
In a CVCS, all the project’s files and their respective versions are stored on a central server. Developers need to connect to this central server to check out the files they want to work on. After making changes, they check the modified files back into the central repository. Other team members can then update their local working copies by fetching the changes from the central server. This model relies heavily on the availability of the central server for day-to-day operations.

2\. Distributed Version Control System (DVCS):  
On the other hand, a DVCS allows each developer to have their own local copy of the entire project repository, including its complete history. This means that developers can work independently, even without an active network connection. They can commit changes to their local repository and later synchronize those changes with the main central repository or share them directly with others. DVCS systems are more decentralized and provide greater flexibility for individual developers.

The most popular DVCS is Git, which has become the standard version control system for many projects due to its efficiency, speed, and robustness. It allows developers to create branches, merge changes, and collaborate seamlessly.

In summary, CVCS and DVCS have their merits, but DVCS has gained more popularity due to its decentralized nature, enabling developers to work more efficiently and effectively in distributed teams.

## **1.4 Why do we use distributed version control over centralized version control?**

We use Distributed Version Control Systems (DVCS) over Centralized Version Control Systems (CVCS) for several reasons:

1\. Offline Work:  
DVCS enables developers to work offline, which means they can continue making changes to the code even without a constant internet connection. This is particularly beneficial for developers who are on the go or in areas with limited internet access. They can commit changes to their local repository and later synchronize with the central repository once they have an internet connection. This capability enhances productivity and allows for uninterrupted development even in challenging connectivity situations. 📶💻

2\. Faster Performance:  
DVCS performs most version control operations locally, without relying heavily on a central server. Since developers have a local copy of the entire repository, actions like commit, diff, and history exploration are generally faster compared to CVCS, where these operations involve interactions with the central server. Faster performance results in a smoother and more efficient development process, leading to increased productivity. ⚡🚀

3\. Enhanced Collaboration:  
One of the major advantages of DVCS is that each developer has a complete copy of the project and its history on their local machine. This fosters better collaboration among team members because they can work independently and concurrently on their own copies. Developers can create and switch between branches, experiment with new features, and work on bug fixes without interfering with the main codebase. Once they complete their work, they can merge their changes back into the central repository, promoting seamless collaboration. 🤝🔄

4\. More Flexibility:  
DVCS allows for greater flexibility in managing code branches. Developers can create multiple branches to work on different features or experiments simultaneously. These branches can be shared with specific team members for collaboration or can be kept private until they are ready to be merged. This flexibility encourages agile development practices and facilitates the easy implementation of new features without disrupting the main development line. 🌿💡

5\. Increased Security:  
The distributed nature of DVCS provides an inherent advantage in terms of security. With DVCS, the entire project history is stored on multiple servers and the local machines of each developer. This redundancy makes the project more resistant to data loss. In contrast, CVCS relies heavily on the central server, and if it fails or experiences data corruption, it could lead to significant data loss. DVCS’s redundancy and decentralized storage enhance data security and reliability. 🔒🔐

6\. Decentralization:  
Unlike CVCS, which relies on a central server as a single point of failure, DVCS does not have such a dependency. In DVCS, each developer’s repository is a complete and independent copy of the project. This decentralization offers more autonomy to developers and teams. Even if the central server experiences downtime or technical issues, developers can continue working with their local repositories. This aspect provides greater reliability and stability to the development process. 🌐🏛️

In conclusion, the advantages of using DVCS over CVCS lie in its ability to provide offline work capabilities, faster performance, enhanced collaboration through distributed repositories, increased flexibility with branching, improved data security through redundancy, and overall decentralization, which adds resilience to the development process. As a result, DVCS has become a preferred choice for many development teams seeking efficient and modern software development workflows. 🌟👥🛡️

# **2\. Task 1: Install Git**

To get started, we’ll install Git on your computer. Git works on Windows, macOS, and Linux. Follow these simple steps:

1. Go to [git-scm.com/downloads](http://git-scm.com/downloads), the official Git website.
    
2. Download the installer that matches your operating system.
    
3. Run the installer and follow the on-screen instructions to finish the installation.
    
4. Once the installation is done, open a terminal or command prompt, and type git — version to make sure Git is installed correctly. You should see the version number displayed.
    

![](https://miro.medium.com/v2/resize:fit:875/1*GuNMZzSObBGtZ51kGqI1MQ.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*zP7_cygnyvYQ5apPJLrLog.png align="left")

```basic
sudo apt-get update && sudo apt-get install git 
git --version
```

# **3\. Task 2: Create a GitHub Account**

GitHub is a popular platform where people store their Git projects and work together on them. If you don’t have a GitHub account yet, here’s how you can create one:

1. Open your web browser and go to [github.com](http://github.com).
    
2. On the GitHub homepage, click on the “Sign up” button.
    
3. Fill in the required information, like your username, email, and password.
    
4. Choose a plan that suits you (Free or one of the paid options) based on your needs.
    
5. Complete the verification process, which might include solving a CAPTCHA or confirming your email.
    

Once you finish these steps, congratulations! You’ve successfully made your GitHub account. Now, you can start sharing and collaborating on your projects. 🌟🤝

# **4\. Exercise 1: Create a New Repository on GitHub**

Let’s get started by creating a new repository on GitHub, where we’ll keep and organize our code. Follow these simple steps:

1. Open your web browser and visit [github.com](http://github.com).
    
2. Log in to your GitHub account.
    
3. On the GitHub homepage, click the “+” button at the top-right corner, then select “New repository” from the menu.
    

![](https://miro.medium.com/v2/resize:fit:875/1*jQVxEH3FpJH7awaUXUQPzg.png align="left")

4\. Give your repository a meaningful name.

5\. You can also add a description to give more details about your repository.

6\. Choose whether you want the repository to be public or private, depending on your needs.

![](https://miro.medium.com/v2/resize:fit:875/1*Vj5KZJtv5QaWwyD4Syy4Mg.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*qW-b2l984CdeNUneuYoITA.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*JYjbq-2laM1lxV7K65LeFg.png align="left")

7\. Finally, click the “Create repository” button to create your new repository. That’s it! Your central code storage is ready to go. 🎉

# **5\. Exercise 2: Clone the Repository to Your Local Machine**

Our repository is created on GitHub. You can now use the “git clone” command to duplicate the central repository onto your local machine’s repository. Here’s how you can do it in simple steps:

1. Go to your repository page on GitHub and click on the “Code” button.
    
2. Copy the repository URL.
    
3. Open the terminal or command prompt on your computer.
    
4. Navigate to the directory where you want to save the repository.
    
5. Use the command “git clone” followed by the repository URL you copied. For example git clone [github.com/your-username/your-repository.git](http://github.com/your-username/your-repository.git)
    
6. Press Enter, and the repository will be cloned to your local machine.
    

![](https://miro.medium.com/v2/resize:fit:875/1*0MUjFe-S6yCuV2_KzqpOPg.png align="left")

Great job! 👏 You have successfully cloned the repository to your local machine. Let’s proceed to the next exercise. 🚀

# **6\. Exercise 3: Make Changes, Commit, and Push**

Now that you have the repository copied to your computer, you can make changes to the files and keep track of those changes. Follow these simple steps:

1. 🚶‍♂️ Move to the repository directory.
    

![](https://miro.medium.com/v2/resize:fit:875/1*VP-M99GM88YgxVnTAfvjtA.png align="left")

2\. 📄 Create two files using the touch command.

![](https://miro.medium.com/v2/resize:fit:875/1*EZuEts8HXIrGcsvFYLTDMQ.png align="left")

3\. 🔍 Use the command “git status” to see the changes you made. It will show the modified files.

![](https://miro.medium.com/v2/resize:fit:875/1*pVbAvKros8xoHnxDC4UAhQ.png align="left")

4\. ➕ Use the command “git add” followed by the file names to prepare the tracking changes. For example: “git add filename.txt” or “git add .” to track all changes. Now check the status and our file is now tracked.

![](https://miro.medium.com/v2/resize:fit:875/1*te7dlmPkOxQhq9kNxmGrFQ.png align="left")

5\. 💼 Use the command “git commit” to save the changes with a meaningful message describing the modifications. For example git commit -m ‘add two files’

![](https://miro.medium.com/v2/resize:fit:875/1*WYYct3F-ybI_4uTQdxjl0w.png align="left")

6\. 🚀 Finally, use the command “git push” to upload the committed changes back to the repository on GitHub. For example: “git push origin main” or “git push origin master,” depending on the branch name.

![](https://miro.medium.com/v2/resize:fit:875/1*KTLRgHG2zsgwGQBWcrdehA.png align="left")

By following these steps, you’ll successfully make changes to your GitHub repository, commit the changes, and push them back to the remote repository. This process ensures that your code is version-controlled and accessible to collaborators on GitHub. 🚀

![](https://miro.medium.com/v2/resize:fit:875/1*QLCSM8yBGgwcXe2P_gb5Kw.png align="left")

# **7\. Conclusion**

Congratulations! You’ve completed Day 8 of the #90DaysOfDevOps challenge. Today, you gained a solid understanding of Git and GitHub, covering tasks like creating repositories, cloning them locally, making changes, committing, and pushing back to GitHub. These core exercises are crucial for version control and collaborative software development. Keep up the fantastic work! 🎉🚀