---

  Author: Peter Duddy
---
# Defra Data Science Centre of Excllence Git User Guide
This guide and corresponding GitHub repository is intended to help new and existing Defra team-members learn the fundamentals of using Git in the workplace. Please direct any further questions you may have to peter.duddy@defra.gov.uk.
Any and all feedback is encouraged!

## What is Git?
- Git is an open-source Version Control System (VCS) for code. It’s the most widely used VCS in the world and is considered the industry standard.
- Git allows multiple developers to work on their own local version of the same project simultaneously without affecting the remote “master” copy.
- If you’ve followed the [**SCE VM setup guide**](https://animated-system-bf6fb80a.pages.github.io/getting_started/sce.html#requesting-a-virtual-machine), then Git should already be installed on your virtual machine. If you haven't followed the guide, then please complete this essential first step.
![Image](https://github.com/user-attachments/assets/d392fb1f-30c0-49f5-91cd-17d3003795a8)
- As you can see from the diagram, working with Git involves creating a copy (branch) of the "master" code, making changes to the code, then having those changes incorporated (merged) into the "master" codebase. This both preserves the integrity of the "master" branch and allows the blue and orange user to work simultaneously without overwriting each other's work.
- We will cover how to do all of this shortly.

## What is GitHub?
- GitHub is one of many websites that can host Git  repositories online (remotely).
- GitHub provides an interface through which one can track and manage their repositories and all the changes team members may be proposing for said projects.

## How do I work using Git?

#### 1. Cloning
- This guide will demonstrate how to use Git on the command line using the [**Git_Guide**](https://github.com/Defra-Data-Science-Centre-of-Excellence/Git_Guide) repository as an example. 
- Various extensions and user interfaces for Git exist within VS code and R studio. However, the command line is where you can use the full scope of Git utility, so it is the best way to learn how Git works.
- The first step in working with any Git repository is to "clone" it. 
- Navigate to the [**Git_Guide**](https://github.com/Defra-Data-Science-Centre-of-Excellence/Git_Guide) repo, click on the green code button, and copy the SSH URL underneath where it says "Clone".
- Open PowerShell and turn on your VM.
```{code}
ssh boot
```
- Connect to your VM using the ssh tunnel created in the SCE set up guide.
```{code}
ssh vm
```
- Navigate to the folder in your linux VM where you would like to keep your Git repositories. If you are unfamiliar with Linux then you can find a basic introduction to linux navigation [**HERE**](https://www.geeksforgeeks.org/basic-linux-commands/).
- Clone the Git_Guide repository.
```{code}
git clone <ssh url>
```
- Now if you open VisualStudio Code and select file > open folder, you should be able to navigate to the Git_Guide repository.
- There is only a main.py, a README.md, and a Users folder in the repository. Once you've been added as a contributor to your team's Git repositories, try repeating the previous steps and look at the file structure of those repositories.

#### 2. Branching
- I'm sure at a certain point you will have created a copy of an excel sheet or a word document so that you can make changes to the file without risk of affecting the "master" version. This is exactly what git branches are meant for.
- Open a new terminal in VS Code.
```{code}
git branch
```
- In the terminal there will now be a list of the git branches in your local repository. So far there should only be one called "main".
```{code}
git branch <your_branch_name>
git branch
```
- Now you will see two branches listed: main, and your newly created branch. Note how "main" has an asterisk next to it. That indicates you are still on the main branch.
- Please note, it is never advisable to edit the main branch directly. We'll get onto how to make changes the proper way shortly.
```{code}
git checkout <your_branch_name>
git branch
```
- 
- You've now moved onto your new branch.
- Please note, it is best practice to give your branches short, informative names e.g. if you are working on data ingestion and cleaning in that branch, you might call it "data_ingest".
- Now navigate back to the remote [**Git_Guide**](https://github.com/Defra-Data-Science-Centre-of-Excellence/Git_Guide) repository.
- Underneath the title you will see a drop down menu with an icon that looks like the diagram on a manual car's gear lever. Click on it and you will see a branch called "pete_test". However, you will not see your newly created branch. This is because the branch you created is a **local** branch, whereas the branches listed here are **remote** branches. 


#### 3. Committing
- So far we have cloned the repo and created a branch to work on. Now we need to start using Git to track the work we will be doing.
- Navigate to your branch if you aren't already there.
- In the "Users" folder, create a python file, populate it with a basic print() statement, then save the file.
- You will notice that in VS code this newly created file is green and has a U next to it. This is because the new file is "untracked" which means that Git is unaware of its existence.
- Git's version control works by taking a series of uniquely identifiable snapshots (called commits) of the changes we make to our files. So let's take a snapshot of the changes we just made.
```{code}
git add <your_new_file_path/your_new_file.py>
git commit -m "<a descriptive message>"
```
- The terminal output shows you the commit ID in square brackets, the number of files changed and the number of lines of code that have been added/deleted.
- You will also notice that the file is no longer green and marked as un-tracked!
- Now add another print statement to your file and save it.
- This time the file has turned yellow with an M next to it. Git is aware of the file thanks to our last commit, but it isn't aware of the additions we just made.
- Repeat the previous steps for adding and committing the file and notice how the terminal output is different this time.
- Now that we've made some great new additions to the code base, it's time to get our colleagues to QA these changes.


#### 4. Pushing
- Having Git track our code changes through regular commits is very useful. If we were to alter our code beyond recognition in a flurry of "inspiration", we'd be able to revert back to an old commit from when the code actually worked. This can get you out of some tricky situations.
- The more significant benefit of committing our changes, however, is that it allows us to push our changes to the remote repository for our team to QA our work.
```{code}
git push --set-upstream origin <your_branch_name>
```
- This has created a branch in the remote repository with the same name as your local branch and pushed your changes to that branch.
- Note that the terminal output says a remote branch has been created to track your local branch.
- Now navigate back to the remote [**Git_Guide**](https://github.com/Defra-Data-Science-Centre-of-Excellence/Git_Guide) repository. 
- On the main page it should say that your branch has had recent pushes, and in the branch list you should see this remote branch you have just created.
- Now, in VS code, add another print statement to the file you created and repeat the previous steps of adding and committing those changes.
```{code}
git push
```
- Note that this time we didn't need to specify the upstream (remote) branch. This is because when we created the upstream branch previously, it was set up to track you local branch and all the changes you might push in future.
- Now navigate back to the remote [**Git_Guide**](https://github.com/Defra-Data-Science-Centre-of-Excellence/Git_Guide) repository.
- switch to the remote branch you created.
- Underneath the branch selection drop down menu, it should say that "This branch is x commits ahead of main". This means that your branch has x number of changes made to it that the main branch doesn't have just yet. It may also say that you are a number of commits **behind** main as well, but we'll get to that later.
- Click on the "x commits ahead of" hyperlink and you will see the changes you made with each commit, but most importantly, you can see a green button called "Create pull request".

#### 5. Pull Requests
- Git is an indispensable coding tool to protect your code base against unwanted changes, but at some point there will be changes made that deserve to be in the coveted main branch. This is where the pull request comes in.
- In the previous section we covered how you would go about pushing the code changes made on your local branch to a remote branch. Now we need to request that someone else pulls those changes into the remote branch into the main branch.
- As previously mentioned, if you open your remote branch in GitHub, you should see a hyperlink that says you are "x commits ahead of main". Click on this link and you will be able to see your commit history. Above that you will see two drop down menus, one that says "compare" and one that says "base". These indicate which branch is to be compared and merged with the other, but fortunately it will default to comparing our branch with the main branch. Lastly, there is a big green button called "create pull request".
- Click on "create pull request", add an informative title, as well as a longer description of the changes you've made.
- On the right hand side of the screen you will be able to choose reviewers and assignees for your pull request. The assignee will be the person to ultimately approve and merge your pull request, whereas a reviewer is just anyone who you think might want to have sight of your changes. For now select myself (Pete-2319) as the assignee and click the "create pull request" button beneath the description box.
- You've now covered all the key steps in working with Git. From cloning the repository to creating a pull request. The following sections will hopefully cover some scenarios you may encounter while working with Git and how to overcome them.
![Image](https://github.com/user-attachments/assets/ed26e039-0ad2-4a72-bab1-240b7ea43df6)
- The above graphic accurately summarises the overall Git workflow the you have just learned and will be following for your future projects.

## Common Scenarios?

#### Why am I four commits behind main?
- During the course of this guide, we made x number of commits, pushed those commits to a remote branch, then created a pull request. Merging that pull request into the main branch would mean that any colleague working in the same repo would now be x commits behind the main branch.
- To rectify this, at the start of any coding session on your local branch, run...
```{code}
git pull origin main
```
- This will pull any code changes that have been merged into the main branch and update the code in your local branch so that you are up to date.
- This shouldn't affect the code you've been working on, because it is good practice to coordinate the work you are doing with your colleagues, so that two people aren;t working on the same files at the same time.
#### What if I can't use SSH to clone my repository?

#### What if I commited some bad code?

#### What if I accidentally altered the main branch?

#### What if my feature branch has a typo in its name?
- To delete a local branch you have created run...
```{code}
git branch -d <typo_branch>
```

#### What if I want to clone all the remote branches, not just main?
- If you've just cloned a remote repository and only have the main branch in your local repository, you can run...
```{code}
git branch -r
```
- This will display all the remote branches. Once you know which one you need to work on, run...
```{code}
git checkout --track origin/<remote_branch_of_interest>
```
- This will bring the create a local branch of the same name from the remote branch of interest and bring in the che code changes.
