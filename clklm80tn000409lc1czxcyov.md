---
title: "Day 2 of #90daysofdevops: Mastering Ubuntu Commands for Success"
datePublished: Thu Jul 27 2023 20:36:48 GMT+0000 (Coordinated Universal Time)
cuid: clklm80tn000409lc1czxcyov
slug: day-2-of-90daysofdevops-mastering-ubuntu-commands-for-success
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690490095684/19922cf5-8abc-409d-a0ed-6edd68f5b5bb.png
tags: ubuntu, linux, command-line, shell, 90daysofdevops

---

# **1\. Linux**

Linux is a remarkable operating system renowned for its stability, security, and adaptability. Initially created by Linus Torvalds in 1991, Linux has grown to become one of the most popular and widely used OS options worldwide.

The strength of Linux lies in its open-source nature, based on the Unix operating system. Being open-source means that the entire source code is accessible to the public, allowing users to modify, distribute, and utilize it freely. This unique characteristic has spurred the formation of a thriving and dynamic community of developers who actively contribute to the evolution of various Linux distributions, commonly referred to as “distros.” These distributions are tailored to cater to different use cases and user preferences, ensuring that Linux can be effectively utilized across diverse devices and environments.

Linux’s versatility has led to its widespread adoption across an array of devices, including servers, desktop computers, smartphones, embedded systems, and more. Its stability and robust security features make it a preferred choice for servers, where reliable performance and protection against potential threats are paramount.

Furthermore, Linux’s flexibility and customizable nature have encouraged its use in numerous specialized applications and scenarios. Its adaptability has allowed it to power embedded systems in various industries, such as IoT devices, industrial equipment, and networking hardware.

# **2\. History**

In 1991, Linus Torvalds, then a student at the University of Helsinki, Finland, embarked on a project to create a freely accessible academic version of Unix. This project evolved into the Linux kernel, the core component of the Linux operating system. Initially released under Linus Torvalds’ own license with restrictions on commercial use, the turning point came in 1992 when he made the momentous decision to switch to the GNU General Public License (GNU GPL).

This licensing change revolutionized Linux, ensuring its open-source nature, and granting users the freedom to modify, distribute, and use the code without limitations. As Linux progressed, it incorporated essential tools from the GNU software ecosystem, released under the GNU copyright, creating a powerful and adaptable OS. The combination of the Linux kernel’s origins, the adoption of the GNU GPL, and the collaboration of a vibrant global community have propelled Linux to become a widely used, stable, and versatile operating system on various devices and platforms worldwide.

# **3\. Architecture**

The architecture of Linux mainly Contains Applications, Shell, Kernel, and Hardware.

![](https://miro.medium.com/v2/resize:fit:644/0*wICjN2LC847nIP0e align="left")

1. **Terminal:** In Linux, the terminal is a command-line interface (CLI) where you can enter text commands to interact with the operating system.
    
2. **Kernel:** A kernel is the critical component of an operating system. It works as a bridge between the applications and data processing at the hardware level with the help of its interprocess communication and system calls.
    
3. **Shell:** The shell is a command interpreter that interprets the commands entered in the terminal and communicates with the Linux kernel to execute them. Popular shells in Linux are Bash, Zsh.
    

# **4\. File System Hierarchy**

![](https://miro.medium.com/v2/resize:fit:875/0*i5xTFlnhnWTeKDNo align="left")

1. **/ —** The base of the Linux directory is root, this is the starting point of FSH.
    
2. **/root** — It is the home directory for the root user.
    
3. **/bin -&gt;User Binaries** — It contains Commands used by all users.
    
4. **/sbin -&gt;System Binary** — It contains commands used by only root user
    
5. **/dev -&gt;Device Files** — It contains hardware device files.
    
6. **/var -&gt;Variable Files** — The variable data files such as log files are located in the /var directory.
    
7. **/mnt -&gt;Mount Directory** — This directory is used to mount a file system temporarily.
    
8. **/media -&gt; Removable Media Devices** — The /media directory contains a sub-directory where removable media devices inserted into the computer are mounted.
    
9. **/usr** — By default software is installed in this directory.
    
10. **/etc** — It contains all configuration files.
    
11. **/boot** — It contains bootable files for Linux.
    
12. **/home** — home directory for other users.
    
13. **/tmp -&gt; Temporary Files** — It contains temporary files created by systems and users and deleted when the system is rebooted.
    
14. **/opt** — Optional Application software packages.
    
15. **/dev** — Essential Device files. This includes terminal devices, USB, or any device attached to the system.
    

# **5\. Common Linux Commands and Utilities**

1. Command to use the present working directory :  
    The **pwd** command stands for **print working directory**. It is used to display the full path of the current working directory.
    
2. Command to list files and directories with hidden files: **ls** is a command that is used to list the files and directories in a directory.
    
3. Command to create a nested directory **A/B/C/D/E:** The command to create a nested directory is **mkdir -p A/B/C/D/E**. The -p switch creates parents’ directories.
    

![](https://miro.medium.com/v2/resize:fit:875/1*sFKjqHAY4MFW1xd-SIGEag.png align="left")