---
title: "Day 3 of #90daysofdevops:Basic Linux Commands"
datePublished: Thu Jul 27 2023 20:40:01 GMT+0000 (Coordinated Universal Time)
cuid: clklmc5tw000r09m9aiuk67ob
slug: day-3-of-90daysofdevopsbasic-linux-commands
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690490284481/c6c59fdb-f616-4e59-979d-5a16286f278a.jpeg
tags: linux, devops, devops-articles, 90daysofdevops, trainwithshubham

---

# **Introduction**

Welcome back to Day 3 of the thrilling **#90DaysOfDevOps** challenge! Today, we’ll explore the wonders of Linux commands, like magical keys unlocking every DevOps engineer’s potential! Navigating your Linux system becomes as easy as exploring a map with these tools. Get ready for a tech-packed journey! Together, we’ll unravel the mysteries of essential Linux commands, discovering hidden treasures that elevate your skills. Excitement fills the air as we dive into this epic DevOps adventure! Let’s go!

# **1\. To view what’s written in a file**

To view the contents of a file in Linux, you can use the **cat** command. For example, let’s say you have a file named **example.txt** To view what’s written in this file, open your terminal and write **cat example.txt:**

![](https://miro.medium.com/v2/resize:fit:875/1*zbKz8wIhjF9WkXs6ANVqNw.png align="left")

Also, we can use “less” or “more” instead of “cat” to view files as they offer better text navigation. “Cat” shows all content at once, while “less” and “more” allow scrolling and analyzing large files more easily.

# **2\. To change the access permissions of files**

Changing the access permissions of files in Linux is done using the “chmod” command, which stands for “change mode.” 🚪

In Linux, every file has three types of permissions: read (r), write (w), and execute (x). These permissions can be set for three different categories of users: the file’s owner (u), the group (g) the file belongs to, and others (o) who are not the owner or part of the group.

To change the permissions, we use a combination of letters and symbols. For example:

* **“chmod u+rwx example.txt”** grants read, write, and execute permissions to the file owner.
    
* **“chmod go-r example.txt”** revokes read permission from the group and others.
    

Here’s an example:

Let’s say we have a script file named “[script.sh](http://script.sh)” that we want to make executable only for the owner and read-only for others. We would use the following command:

```basic
chmod u+x,go-w script.sh
```

In this command:

* **“u+x”** adds execute permission to the owner.
    
* **“go-w”** removes written permission from the group and others.
    

After running this command, the owner of “[script.sh](http://script.sh)” will be able to execute it, while the group and others will only have read access.

# **3\. To check which commands you have run till now**

To check the commands you have run in the current terminal session in Linux, you can use the “history” command. 📜

![](https://miro.medium.com/v2/resize:fit:875/1*_YGQLf-xh-MYcC3YbUJm8A.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*CloHkfkS7jfR4A7aOqNSiA.png align="left")

# **4\. To remove a directory/ Folder**

Removing a directory or folder in Linux is done using the **“rmdir” or “rm”** command.

The **“rmdir”** command is used specifically to remove empty directories. For example:

![](https://miro.medium.com/v2/resize:fit:875/1*7cayt-qTY3qSwOWNZhFv9g.png align="left")

The **“rmdir”** removes an empty **“example”** directory, while **“rm -r”** deletes directories with content and files. For example

![](https://miro.medium.com/v2/resize:fit:875/1*CbC4AN-Knkk1vtLCsGwd9Q.png align="left")

Be cautious with “rm -r” to delete “demo” and its contents without confirmation, leading to permanent data removal. Double-check directories to avoid accidental data loss. Use commands responsibly!

# **5\. To create a fruits.txt file and view the content**

To create a “fruits.txt” file in Linux, you can use the “touch” command. 📄

For example:

![](https://miro.medium.com/v2/resize:fit:875/1*I9os8cO0lURdcc8IKoH94Q.png align="left")

This command will create an empty file named “fruits.txt” in the current directory.

Next, to view the content of the “fruits.txt” file, you can use the “cat” command.

For example:

![](https://miro.medium.com/v2/resize:fit:875/1*eG0ec7_bHjBYD-Nh_q2daA.png align="left")

# **6\. Add content in fruits.txt (One in each line) — Apple, Mango, Banana, Cherry, Kiwi, Orange, Guava**

To add content to the “fruits.txt” file, you can use a text editor or the “echo” command to append each fruit on a new line. Here’s an example using the “echo” command:

![](https://miro.medium.com/v2/resize:fit:875/1*3I0I05qmnM3jEZh_11SsMw.png align="left")

This command adds each fruit on a separate line in the “fruits.txt” file. You can then use the “cat” command to view the contents of the file:

![](https://miro.medium.com/v2/resize:fit:875/1*HI-nBZrImpXFMGahEW1dqg.png align="left")

Now your “fruits.txt” file is filled with delicious fruits! Enjoy!

# **7\. To Show only the top three fruits from the file**

To display only the top three fruits from the “fruits.txt” file, you can use the “head” command with the “-n” option, specifying the number of lines you want to see. In this case, we want to see the first three lines, which represent the top three fruits in the file.

![](https://miro.medium.com/v2/resize:fit:875/1*Dz3qesdKjJn73Ur5nsHymQ.png align="left")

# **8\. To Show only the bottom three fruits from the file**

To display only the bottom three fruits from the “fruits.txt” file, you can use the “tail” command with the “-n” option, specifying the number of lines you want to see from the end of the file. In this case, we want to see the last three lines, which represent the bottom three fruits in the file.

![](https://miro.medium.com/v2/resize:fit:875/1*nUHG8svGwwmYwb4J_2LBwg.png align="left")

# **9\. To create another file Colors.txt and to view the content**

To create a new file called “Colors.txt” in Linux, you can use the “touch” command followed by the desired filename. This command will create an empty file named “Colors.txt” in the current directory. Now, to view the content of the file, you can use the “cat” command:

![](https://miro.medium.com/v2/resize:fit:875/1*JpzXqGjOQfviuIbmu6DkLg.png align="left")

# **10\. Add content in Colors.txt (One in each line) — Red, Pink, White, Black, Blue, Orange, Purple, Grey**

To add the specified content to the “Colors.txt” file with each color on a separate line, you can use the following command:

![](https://miro.medium.com/v2/resize:fit:875/1*YrgL4jxPICzsjgs0waCoOQ.png align="left")

This command will add the colors Red, Pink, White, Black, Blue, Orange, Purple, and Grey to the “Colors.txt” file, with each color on its line. If you view the content of the file using the `cat` command:

![](https://miro.medium.com/v2/resize:fit:875/1*a7-hCTuvk1-5V7e30lqCXA.png align="left")

# **11\. To find the difference between fruits.txt and Colors.txt file**

To find the difference between the contents of two files, such as “fruits.txt” and “Colors.txt,” you can use the “diff” command. Here’s an example:

![](https://miro.medium.com/v2/resize:fit:875/1*cGy5A0Pdn8JeQcBGdV4rzQ.png align="left")

This command will compare the contents of the “fruits.txt” and “Colors.txt” files. If there are any differences between the two files, the `diff` the command will show them in the output.

With the `diff` command, you can easily spot the variations between two files and manage your data more efficiently.

# **Conclusion**

Congratulations on mastering essential Linux commands! You’ve gained valuable skills in file interactions, permissions, and command analysis. From creating files to exploring their contents, you’ve become proficient in various Linux aspects. By using commands like “ls,” “chmod,” and “rm,” you’re now a Linux command-line pro! “Less” and “more” help you read files effortlessly. You’ve even created “fruits.txt” and “Colors.txt” and learned to display top and bottom items with “head” and “tail.” The “diff” command aids in identifying file differences. Keep practicing and exploring as your Linux adventure thrives! Embrace the command line’s power and discover new possibilities in the vast Linux world. Happy DevOps exploring!

Stay in the loop with my latest insights and articles on cloud ☁️ and DevOps by following me on Medium, LinkedIn [(](https://www.linkedin.com/in/mudit--mathur/)[https://www.linkedin.com/in/mudit--mathur/](https://www.linkedin.com/in/mudit--mathur/)[)](https://www.linkedin.com/in/mudit--mathur/), and GitHub [(](https://github.com/mudit097)[https://github.com/mudit097](https://github.com/mudit097)[)](https://github.com/mudit097).

Thank you for reading! Your support means the world to me. Let’s keep learning, growing, and making a positive impact in the tech world together.