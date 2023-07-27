---
title: "Day 4 of #90daysofdevops: Basic Linux Shell Scripting for DevOps Engineers"
datePublished: Thu Jul 27 2023 20:43:55 GMT+0000 (Coordinated Universal Time)
cuid: clklmh6pa000509l46hc6gcm2
slug: day-4-of-90daysofdevops-basic-linux-shell-scripting-for-devops-engineers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690490458411/1a81e1a2-a8be-419f-bda4-c4b5986065bc.webp
tags: blogging, devops, shell, 90daysofdevops, trainwithshubham

---

# **1\. What is Shell?**

Shell is a UNIX term for an interface between a user and an operating system service.

Shell provides users with an interface and accepts human-readable commands into the system and executes those commands which can run automatically and give the program’s output in a shell script.

# **2\. What is Kernel?**

A Kernel is at the nucleus of a computer. It makes the communication between the hardware and software possible. While the Kernel is the innermost part of an operating system, a shell is the outermost one.

![](https://miro.medium.com/v2/resize:fit:835/0*KKAOQjDH98EuQXo4 align="left")

# **3\. What is Linux Shell Scripting?**

Shell Scripting is an open-source computer program designed to be run by the Unix/Linux shell. Shell Scripting is a program to write a series of commands for the shell to execute.

It can combine lengthy and repetitive sequences of commands into a single and simple script that can be stored and executed anytime which, reduces programming efforts.

# **4\. How to write Shell Script in Linux**

Shell Scripts are written using text editors. On your Linux system, open a text editor program, and open a new file to begin typing a shell script or shell programming.

Then give the shell permission to execute your shell script that is it has all Read, Write, Execute permission enabled for the file or directory and put your script at the location from where the shell can find it.

Once it has all the permission, the color of file / dir has changed to green for execution.

**#!** is an operator called **shebang** which directs the script to the interpreter’s location. So, if we use **#! /bin/sh** the script gets directed to the bourne-shell.

in /bin/bash, bash is A.K.A **Bourne Again SHell** we can write instead of /bin/sh as both are directed to bash shell location.

# **5\. Task**

## **a) Write a Shell Script that prints “I will complete #90DaysOfDevOps challenge.”**

```basic
#!/bin/bash
echo "I will complete #90DaysOfDevOps challenge."
```

![](https://miro.medium.com/v2/resize:fit:875/1*ERrDdk9mqqNlTj53MIfnzA.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*_m3ipDPYYHo5tflUmTv7Mw.png align="left")

**b) Write a Shell Script to take user input, input from arguments, and print the variables.**

```basic
#!/bin/bash
echo "What is your name?"
read name
echo "What is $name"
```

![](https://miro.medium.com/v2/resize:fit:875/1*qXwOhXZ57fFnFzjZ5KEI9Q.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*53l7jbo50u-owNlxfIIzmQ.png align="left")

**c) Write an Example of If-Else in Shell Scripting by comparing two numbers.**

```basic
#!/bin/bash
# Read user input and store it in the varibale 'num1'
read -p "Enter the first number:" num1
# Read user input and store it in the variable 'num2'
read -p "Enter the second number" num2

# Compare the two numbers
if [ $num1 -eq $num2 ];then
        echo "Both numbers are equal."
elif [ $num1 -lt $num2 ]; then
        echo "$num1 is less than $num2."
else
        echo "$num1 is greater than $num2."
fi
```

![](https://miro.medium.com/v2/resize:fit:875/1*ud-nCMpGyRN9WxxG30-MWw.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*ddHvuMejPMe7y-fea0pbZg.png align="left")

Thank You

Mudit Mathur