---
title: "Day 10 — Advanced Git & GitHub for DevOps Engineers Part 1"
datePublished: Thu Jul 27 2023 21:10:40 GMT+0000 (Coordinated Universal Time)
cuid: clklnfkz1000709mt2g8sdl6q
slug: day-10-advanced-git-github-for-devops-engineers-part-1
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690492120711/9feb5365-200d-46b1-9d69-880bc2ddf30e.webp
tags: github, git, devops, 90daysofdevops, trainwithshubham

---

# **1\. 🌟 Introduction 🌟**

Get ready to dive into the art of branch creation, committing changes, and gracefully rolling back code. We’ll also uncover the art of integrating our work flawlessly through merging and rebasing. Buckle up and join us on this enchanting Git adventure! 🧙‍♂️🔮✨

# **2\. 🌿 Git Branching and Its Strategy**

In a team working on a web application using Git, branching is a crucial aspect of managing the codebase efficiently. Let’s explore how Git branching works and its benefits:

1\. Default Branch:  
The default branch, typically named “master” or “main,” represents the stable version of the application. It is essential to keep this branch clean and functional, ensuring that it always contains a deployable version of the code.

2\. Creating a Feature Branch:  
When you need to add a new feature or work on a specific task, it’s best to create a new branch to isolate your changes from the main codebase. For example, if you want to add a user login system, you can create a new branch called “feature/login” using the following command:

```basic
git checkout -b feature/login
```

3\. Working Independently:  
With separate feature branches, you and your teammates can work independently on different tasks without interfering with each other’s code changes. For instance, another teammate working on adding search functionality can create a branch named “feature/search”:

```basic
git checkout -b feature/search
```

4\. Merging Features into the Main Branch:  
Once a feature is complete and thoroughly tested, it can be merged back into the main branch (“master” or “main”) to incorporate the changes into the stable codebase. To merge the “feature/login” branch into the “master” branch, you can use the following commands:

```basic
git checkout master
git merge feature/login
```

Similarly, your teammate can merge the “feature/search” branch into “master” once the search functionality is ready.

5\. Release Management:  
Git branching strategies also help in managing releases and bug fixes effectively. If a critical bug is found in the “master” branch, a hotfix branch can be created to address the issue without disrupting ongoing development. For example:

```basic
git checkout -b hotfix/bug-fix
```

6\. Merging Hotfixes:  
Once the bug is fixed in the hotfix branch, it can be merged back into the “master” branch and any other active branches that need the same fix:

```basic
git checkout master
git merge hotfix/bug-fix
```

By following this branching strategy, you can maintain a stable main branch while enabling seamless collaboration among team members. Git branching enhances development agility, reduces conflicts, and ensures that the codebase is always in a deployable state.

# **3\. 🔄 Git Revert and Reset**

Git Revert: 🔙 When you make a mistake in your code and want to undo a specific commit without erasing its history, you can use Git Revert. It creates a new commit that undoes the changes made in the specified commit. This means that the commit you want to revert will still exist in the history, but the changes it introduced will be removed in a new commit. It’s like going back in time and undoing a mistake without altering the past. 🕰️

Git Reset: 🔄 Git Reset, on the other hand, is a more powerful command that allows you to move the current branch to a specific commit. It has different modes like “soft,” “mixed,” and “hard.” The “soft” mode keeps the changes from the commits you reset as staged changes, the “mixed” mode keeps them as unstaged changes and the “hard” mode discards them completely. In simple terms, Git Reset helps you to reset the branch to a previous state and removes the commits after that point. 🌱

# **4\. 🔀 Git Merge and Rebase**

Git Merge: 🤝 Imagine you and your team are working on a group project. Each team member is responsible for a specific feature. Git Merge is like getting everyone’s work together at the end of the day and combining it into a single document. It takes the changes from different branches and brings them into the main branch, creating a cohesive codebase. It’s like teamwork, where everyone contributes their part, and the project becomes more complete and robust. 🌟👨‍💻👩‍💻

Git Rebase: 🚀 Think of Git Rebase as time travel! When you use Git Rebase, it’s like going back in time to the point where you branched off and replaying your changes on top of the latest work. It’s like updating your project to the most recent version and integrating your improvements smoothly. This keeps your commit history clean and organized, just like maintaining a clear timeline of project progress. But be cautious, as time travel can be tricky; you may encounter conflicts that need to be resolved. 🕰️

# **5\. 📋 Task 1: Branching, Committing, and Restoring**

🌟 In this task, we’ll explore how to create a new branch 🌿, make changes with various messages 📝, and restore a file to an earlier version ⏪. Just follow these simple steps:

1. 🚀 Create a new branch named “dev” from the main branch and verify the change using the command “git checkout dev”.
    

```basic
 git checkout -b dev
```

![](https://miro.medium.com/v2/resize:fit:875/1*I0Vlcvo0mp2TwyIwSECdxQ.png align="left")

2\. 📝 Create a new text file named version01.txt and fill it with the following content:

```basic
  "This is the first feature of our application."
```

![](https://miro.medium.com/v2/resize:fit:875/1*odxDaBLeqOJexDkR3JJwXw.png align="left")

3\. 📂 Use the “git add” command followed by the file names to prepare the tracking changes. Then commit this change with the message “Added new feature.”

![](https://miro.medium.com/v2/resize:fit:875/1*4SW9yJbSJW3aXGs6O0hlsA.png align="left")

4\. 📤 Push the `dev` branch to the remote repository using the command:

```basic
  git push origin dev
```

![](https://miro.medium.com/v2/resize:fit:875/1*epLCOzfdwn8H-KImIKgtpQ.png align="left")

5\. 🔄 Make additional commits to the dev branch by updating the version01.txt file and commit this change with the message “Making the following changes: …”.

```basic
  This is the bug fix in the development branch
```

![](https://miro.medium.com/v2/resize:fit:875/1*xCQZWWWbR9CfWJr-cPC3hw.png align="left")

6\. 🔄 Perform this step two additional times, including the provided content, and commit each change with relevant messages.

```basic
This is gadbad code.
```

![](https://miro.medium.com/v2/resize:fit:875/1*8E3JwSpyALb6usSin_HZKw.png align="left")

7\. Again for adding feature4

```basic
 This feature will goodbad everything from now.
```

![](https://miro.medium.com/v2/resize:fit:875/1*bYSsWF-x7g1bU5GkMWUkPQ.png align="left")

8\. Adding feature 5

![](https://miro.medium.com/v2/resize:fit:875/1*RCyAvtg7OJ5DhQP10vFtSQ.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*wlI-0C_zcjck2EA334yhcw.png align="left")

9\. 🔙 Revert the version01.txt file to a previous state with the content “This is the bug fix in the development branch.”

10\. 📜 Using the “git log — oneline” command, find the &lt;commit&gt; information and identify the commit you want to reset to.

![](https://miro.medium.com/v2/resize:fit:875/1*am95KL4ot0JuhFQe09-XcQ.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*g7CefBjV007QPuZLsu-z4w.png align="left")

# **6\. 📋 Task 2: Branching, Merging, and Rebasing**

In this task, we will explore the concepts of branches, merging, and rebasing. To get started, follow these steps:

1. 🚀 Let’s merge the “dev” branch with the “main” branch. First, check the commits on the “dev” branch by using “git checkout dev” 👩‍💻. Then, switch back to the “main” branch and check its commits as well 🌿. Now, execute the “git merge dev” command to combine the commits and observe the results.
    

![](https://miro.medium.com/v2/resize:fit:875/1*oSN03X8aLtkHNAKVKLntUw.png align="left")

2\. Now, execute the “git merge dev” command to combine the commits and observe the results.

![](https://miro.medium.com/v2/resize:fit:875/1*oSN03X8aLtkHNAKVKLntUw.png align="left")

3\. 🔄 As a practice, perform a `git rebase` operation to see the difference it makes. Describe the differences you observe 🔄.

![](https://miro.medium.com/v2/resize:fit:875/1*XkQAVdFn3ohhNvQdjCC2Pw.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*HHTPP0o88hj-qr65YSvuCg.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*VNhXpt5L42qt0sWgWEN5sw.png align="left")

![](https://miro.medium.com/v2/resize:fit:875/1*eFwmJCw2DVqZ42HdRPUvOg.png align="left")

In this sequence of commands, developers start by checking out the “dev” branch in Git. They then create a new text file called “version01.txt” with specific content. The changes to this file are staged and committed with an appropriate commit message. After inspecting the commit history on the “dev” branch, they switch to the “main” branch and perform a rebase.

During the rebase, the commits from the “dev” branch are moved on top of the existing commits in the “main” branch, resulting in an updated, linear commit history on the “main” branch. This process demonstrates how branches interact, and how Git’s merge and rebase commands can be used to manage code development seamlessly.

Note: Git merge combines changes and preserves the original commit history, while Git rebase moves commits to create a cleaner, linear commit-graph, making project tracking easier.

# **7\. 🎉 Conclusion 🎉**

Congratulations on completing Day 10 of the #90DaysOfDevOps challenge! Today, we explored advanced Git techniques such as branching, merging, and reverting, essential for efficient collaboration and version control in software projects. Get ready for Day 11, where we’ll dive deeper into Git and GitHub for DevOps Engineers in the second part of this topic. Stay tuned for more exciting learning ahead! 🚀👩‍💻