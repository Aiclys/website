+++
title = 'Contributing to open source projects with git'
author = 'Nyrs'
tags = ["how-to", "programming"]
date = 2024-03-20T12:30:33+01:00
+++

#### This is a step by step guide on how to contribute to open source projects with git. It also acts as a cheatsheet for me as I always forget how to do it. Before telling you how you can contribute, I will tell you why you should even consider it.

## Why you should consider contributing to open source projects
#### By contributing to public open source projects you can gain a lot of real-world experiencce and skills. It is also a very rewarding way to learn and teach. By writing code that is reviewed and corrected by other people you learn how to write clean and ideally bug-free code which can be used and deployed on a larger scale than your usual personal project. Furthermore, it can be a great way to find people who are willing to help you improve and share your skills. You also never know how it could benefit your future self, maybe it will help you tremendously to have contributed to a certain project as it could be that your future employer find the code you have written. Another huge benefit is that you most likely will learn how to do proper documentation. Most middle sized to large projects require their contributors to precisely document the changes they made. This way, you dohn't only learn to write cleaner code, you also learn how to describe it so that anyone else can understand it. Moreover, most contributors start their journey by fixing issues in the code of others or helping people who have issues using the app. This can help you spot errors and in turn help you avoid them.

## How to contribute
#### This guide will be focused on Github-based contributions but the steps are basically the same on Codeberg, Gitlab, Gitea, Sourcehut and other source forges.

### Step 1: Installing and configuring git
#### To install git use the command based on your OS:
#### Debian-based: 
```
sudo apt install git
```
#### Arch-based:
```
sudo pacman -S git
```
#### Fedora and other RPM-based distros:
```
sudo dnf install git
```

#### After installing git, you need to set up a username and email. To do so use the following command where username is you Github username and useremail is your email:
```
git --global user.name "username"
git --global user.email "useremail"
```
#### To check if everything worked correctly. type the following commands:
```
git --global user.name
git --global user.email
```
#### There is a lot more configuring you can do. Visit the [git website](https://git-scm.com/book/en/v2/) and the [GitHub website](https://docs.github.com/en/get-started/getting-started-with-git/) for more information.

### Step 2: Fork and clone the desired project
#### Before making any changes to a project you first need to create a fork and clone it into your local machine. To do so use the following commands:
```

```
