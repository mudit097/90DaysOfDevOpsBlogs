---
title: "Day 5 of #90daysofdevops Advanced Linux Shell Scripting for DevOps Engineers with User Management"
datePublished: Thu Jul 27 2023 20:47:42 GMT+0000 (Coordinated Universal Time)
cuid: clklmm1ue000u09m9gxm6g1l9
slug: day-5-of-90daysofdevops-advanced-linux-shell-scripting-for-devops-engineers-with-user-management
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690490712575/171a6714-be82-4fe0-83e9-6531cd925f56.png
tags: blogging, devops, shell, user-management, 90daysofdevops

---

# **1\. Write a bash script to create directories. sh that when the script is executed with three given arguments (one is the directory name and second is the start number of directories and the third is the end number of directories ) it creates a specified number of directories with a dynamic directory name.**

```basic
#!/bin/bash
#############################################################
#Purpose: This script will create 90 directories at once
#############################################################

#Intializing variables
Name_of_dir=$1
start_no=$2
end_no=$3
#Command to create directories
eval mkdir $Name_of_dir{$start_no..$end_no}
```

Here, the “eval” command takes arguments as input to the command and stores it as one single command.

Execution,

```basic
./directories.sh day 1 90
```

Here,

day, — First argument

1, — Second argument

2, — Third Argument

![](https://miro.medium.com/v2/resize:fit:875/0*e4oRElPjABwZpgx8 align="left")

# **2\. create a Script to backup all your work done till now**

```basic
##########################################################################
#Purpose: This script will take backup
##########################################################################

#Creating Variables 
src=/home/ubuntu/day5
dest=/home/ubuntu/backups
time=$(date +"%Y-%m-%d-%H-%M-%S")
backupfile=$dest/$time.tgz

#Taking Backup
echo "Taking backup on $time"
tar zcvf $backupfile --absolute-names $src

if [ ${?} -eq 0 ]
then
        echo "Backup Complete"
else
        exit 1
fi
```

Above, the script will take backups.

![](https://miro.medium.com/v2/resize:fit:608/0*vkDguKCU_y_3Zm9q align="left")

# **3\. Read About Cron and Crontab, to automate the backup Script**

```basic
crontab -e
```

Enter the below code in the last line of crontab,

```basic
* * * * * sh /home/ubuntu/day5/backup.sh
```

![](https://miro.medium.com/v2/resize:fit:833/0*0uNov9i8uxRLlKDg align="left")

first \*, — represents minutes

second \*, — represents hours

third \*, — represents the day of the month

fourth \*, — represents month

fith \*, — day of week

# **4\. Read about User Management**

User management is a very important part of a DevOps engineer’s journey.

User management includes some basic tasks, like

* Creating Users
    
* Deleting Users
    
* Password reset
    
* Adding a user to a group
    

# **5\. Create 2 users and just display their Usernames**

```basic
##########################################################################
#Purpose: This script will take two argument as username and create user
##########################################################################
#Creating variables
user1=$1
user2=$2
#Creating Users
echo "Adding Users $user1 and $user2"
useradd -p test -m $user1
useradd -p test -m $user2
if [ ${?} -eq 0 ]
then
        echo "Users added successfully"
else
        exit 1
fi
```

![](https://miro.medium.com/v2/resize:fit:688/0*GN1_MgRe4zGX1OEo align="left")