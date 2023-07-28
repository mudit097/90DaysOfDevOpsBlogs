---
title: "Day 11 - Advanced Git & GitHub for DevOps Engineers Part 2"
datePublished: Fri Jul 28 2023 19:21:07 GMT+0000 (Coordinated Universal Time)
cuid: clkmyyjtz000009mf63oc5fcs
slug: day-11-advanced-git-github-for-devops-engineers-part-2
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690570395683/be548bda-5a57-44f5-acef-0339e34d5b44.png
tags: github, git, devops, cherry-pick, 90daysofdevops

---

# 🌟 Greetings, Adventurers! 🌟

Welcome back to Day 11 of our exhilarating #90DaysOfDevOps adventure! Today's expedition takes us deep into the realm of Git mastery, where we'll uncover the hidden treasures of Git Stash and Cherry-pick techniques. Moreover, we shall unravel the art of resolving merge conflicts, an invaluable skill for seamless collaboration in your quests. Prepare yourselves to grasp the secrets of Stashing and Applying Changes, attaining virtuosity in the Rebase command, and honing the craft of effective commit messages. As we traverse further, behold the wondrous magic of Cherry-picking and unleashing the full potential of features in your noble projects. Together, let's embark on this thrilling journey of version control, elevating your DevOps experience to unparalleled heights! 🚀😊"

# 🔒 What is Git Stash?

Imagine you are working on a coding project, and suddenly your team asks you to fix a critical bug in another part of the code. You don't want to commit your incomplete changes, as it might create issues in the main codebase. 🐛

Here comes Git Stash to the rescue! 🎉

Git Stash is a powerful feature that allows you to temporarily store your unfinished changes in a safe, hidden box. When you use the "git stash" command, Git saves your current changes and reverts your workspace to a clean state, as if you never started making those changes. 📦

This means you can switch to the bug fix task or any other task without worrying about your incomplete changes interfering with your work. The changes you stashed away are stored and can be easily retrieved later. Once you've fixed the bug or completed the other task, you can simply unstash your changes and continue where you left off, with all your work intact! 🧩

It's like having a secret compartment for your code changes, allowing you to work on multiple tasks simultaneously and keeping your codebase organized and free from half-baked changes. 🧹

# 🍒 What is Cherry-pick?

In Git, "cherry-pick" is a useful operation that allows you to select and apply specific commits from one branch to another.

Imagine you have two branches in your project, and there's a bug fix or a cool feature in one branch that you want to add to another branch without merging the whole branch. 🐞

Here's where cherry-pick comes to the rescue! 🎉

You can cherry-pick the specific commit from one branch and apply it to another branch. It's like plucking a cherry from one tree and placing it on another tree! 🍒🌳

Cherry-pick is a nifty tool to selectively bring in changes from one branch to another, making it easier to manage code and collaborate with your team. 👩‍💻👨‍💻

# 🔄 How to resolve merge Conflicts?

Merge conflicts can happen when you try to combine different branches, and Git doesn't know which changes to keep. This can occur when you're merging or rebasing branches that have gone in different directions.

When a conflict occurs, Git will let you know which files have conflicts. You can use the "git status" command to see the list of conflicted files. 😮

Next, you can use the "git diff" command to see the differences between the conflicting versions and understand what needs to be resolved. 👀

Now comes the fun part! You get to manually edit the conflicting parts in the files, choosing which changes to keep and which to discard. Once you've made the necessary adjustments, you use the "git add" command to tell Git that you've resolved the conflicts. 🛠️

After resolving all the conflicts, you can continue with the merge or rebase process with confidence! 🚀

By resolving merge conflicts, you can ensure that your code is in sync and ready to be shared with the rest of the team. 👩‍💻👨‍💻

# **📋 Task 1: Stashing and Applying Changes**

In this task, our focus will be on branches, and we'll explore how to utilize the "**git stash**" command to save changes temporarily without committing them. Simply follow these steps: 🌟

1. Create a new branch 🌿 using the below command:
    
    ```basic
     git checkout -b dev
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690570956403/ecb91a55-e9f0-4c7f-87d8-38f2cdf5f942.png align="center")
    
    1. Make some changes to the files 📝 in **dev** branch.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690571089227/2a8433f5-417f-4fcc-80e1-891ea928e90e.png align="center")
        

1. In the middle of your work, your team urgently requests you to handle an important task in the main branch. To handle this situation without losing your progress, you can utilize the "**git stash**" command to save your changes without committing them.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690571128462/b8ad5679-bc3e-4ada-bd4a-2e8764685399.png align="center")

1. Use following the command to switch to the **main** branch and proceed with important tasks.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690571206685/49050d9b-a472-40ef-aa9d-819e6d1e5833.png align="center")

1. Now that our crucial task is completed, let's switch 🔙 to the dev branch to continue our work. We'll use the "git stash pop" command to retrieve the changes we stashed earlier and apply them on top of the new commits.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690571253591/6df2aa58-f79f-4804-8915-b8df0a17e885.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690571280043/3b0c4cac-efac-418e-89cb-cad8810213ab.png align="center")

# **📋 Task 2: Rebase and Commit Messages**

In this task, we'll be working on the day-10 version01.txt file in the development branch and carrying out a rebase operation. Follow these steps:

1. 📝 Open the `version01.txt` file in the development branch. add the line: "**After bug fixing, this is the new feature with minor alteration.**"
    
    Commit this change with the message: "**Added feature2.1 in the development branch.**"
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690571488066/7761da50-318d-40c4-b09d-35a1bd936c3c.png align="center")
    
2. 📝 Add another line in version01.txt: "**This is the advancement of the previous feature.**"
    
    Commit this change with the message: "**Added feature2.2 in development branch.**"
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690571527963/f808a0fb-8fb9-4c0c-9cc8-bd0dac4ce1cb.png align="center")
    
3. 📝 Add one more line in version01.txt: "**Feature 2 is completed and ready for release.**"
    
    Commit this change with the message: "**Feature2 completed.**"
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690571598004/e5df3c91-169c-469f-8035-2bbc51b525ff.png align="center")

1. 🚀 Create prod branch and use **git rebase** to include all the commits from the dev branch into the prod branch.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690571640381/779e793c-ff07-41b6-acc7-7f2932cbe926.png align="center")
    

# **📋 Task 3: Cherry-picking and Optimizing Features**

n this task, we'll learn about cherry-picking a specific commit from one branch to another and making additional changes to it. Follow these steps:

1. 🚀 Switch to the production branch. And cherry-pick the commit "Added feature2.2 in development branch" using the below command.
    
    ```basic
     git cherry-pick <commit-hash>
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690571740561/66366404-fa81-45ba-b43a-ffc09be09901.png align="center")
    
2. ✏️ Add the following lines after "This is the advancement of the previous feature" in version01.txt file:
    
    ```basic
      Added few more changes to make it more optimized.
    ```
    
    1. 📝 Commit this change with the message "Optimized the feature."
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690571875640/4a8c963c-79db-469e-8c5f-429b60da07df.png align="center")
        

# 🎉 Conclusion 🎉

Congratulations on successfully completing Day 11 of the #90DaysOfDevOps challenge! During this exciting session, we explored some advanced Git techniques, such as stashing, cherry-picking, and rebasing, and we're going to celebrate your accomplishments!

Git Stash proved to be an invaluable tool, allowing us to temporarily save changes without committing them. Cherry-Pick, on the other hand, empowered us to transfer selective commits between branches, making it a breeze to manage our codebase effectively. And let's not forget about mastering conflict resolution, a crucial skill that enhances collaboration and teamwork.

The comprehensive step-by-step guide covered everything you need to know about stashing and applying changes, as well as how to use rebase to maintain a clean and organized commit history. With the power of cherry-picking, we were able to optimize and fine-tune features, which undoubtedly will boost our development productivity.

By incorporating these powerful Git tools into our workflows, we can streamline processes and make collaboration among team members seamless and efficient.

As you continue on your DevOps journey, I encourage you to keep exploring and practicing with Git, as it holds immense potential for DevOps engineers like yourself. Stay excited and motivated, for there are more challenges ahead that will only help you grow stronger as a developer and a team player! 💪😊🚀