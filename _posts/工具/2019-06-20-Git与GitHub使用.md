---
layout: post
title:  "Git与GitHub的使用"
categories: 工具
tags: Git GitHub 版本控制
author: 希夷小道
---

* content
{:toc}

主要介绍版本控制工具Git的使用和常用命令，以及与之相关的GitHub的基本操作。都是最基本的操作，详情请查阅相关文档。



## 一、版本控制
### 为什么需要版本控制
一句话概括，时代在发展，单打独斗，闭门造车的时代早已过去。  
从纵向看，个人开发者在开发软件的过程中可能需要回退到以前的版本，单纯的复制文件备份加时间戳的方式已经不太现实，需要一个能够记录变化或历史的系统以便我们随时查看变化信息和回退到任何想去的地方。  
从横向看，靠个人开发一个大型软件的时代已经过去，我们需要的是分工协作，团队开发，在这个过程中，同步以及合并各个开发者的工作，记录提交的内容和提交者的信息显得尤为重要。Git的诞生正说明了后者。
### 什么是版本控制
简单地说，版本控制是一种记录文件内容变化，以便后期查阅的系统。它的功能主要是后期我们可以回退到需要的版本，并在此基础上带来的团队协作功能，这些都大大方便了我们的开发。
### 常用的版本控制工具   
当下主流的版本控制工具分为两类，集中式和分布式。
* 集中化的版本控制系统（Centralized Version Control Systems，简称 CVCS），诸如 CVS、Subversion 以及Perforce 等，特点是有一个集中管理的服务器，保存所有文件的修订版本。各开发者通过客户端连接到服务器，提交或者更新文件。缺点是服务器故障会带来很大影响，轻则宕机时无法提交信息，重则数据丢失。  
* 分布式版本控制系统（Distributed Version Control System，简称 DVCS），诸如`Git`、Mercurial、Bazaar 以及 Darcs 等，特点是客户端把代码仓库完整地克隆下来。 服务器故障后都可以用任何一个克隆的镜像恢复。因为每一次的克隆操作，实际上都是一次对代码仓库的完整备份。


## 二、Git入门
### Git简介
(强烈推荐Git官网的[教程](https://git-scm.com/book/zh/v2/)，有包含简体中文在内的各种语言翻译，并且可以下载pdf，epub，mobi形式的文档方便本地阅读。)  
 Git的作者是Linus Torvalds，没错，就是写了Linux最初内核的大神，当然，同Linux一样，作为一个开源免费的项目，后期也有无数人为之奉献。  
 Git的诞生的缘由是2005 年，BitKeeper作为一个商业的版本控制工具不在为Linux 开源社区提供免费使用的权力，于是Linus Torvalds决定写一个自己的版本控制工具。   
 Git现在有多牛，基本上是最流行的版本控制工具了。看下官网上的介绍，
  > Git is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency.
 
 > Git is easy to learn and has a tiny footprint with lightning fast performance. It outclasses SCM tools like Subversion, CVS, Perforce, and ClearCase with features like cheap local branching, convenient staging areas, and multiple workflows. 
 
 大意是开源免费的版本控制工具Git，小巧便捷，适用于从小型到大型项目，已然超越了Subversion, CVS等。   
 部分使用了Git的公司：  
![使用Git的部分公司](https://github.com/xiyixiaodao/xiyixiaodao.github.io/blob/master/_posts/工具/.2019-06-20-Git与GitHub使用_images/eb19aec9.png?raw=true)

### Git基本操作
#### 安装与配置
##### 安装
根据不同操作系统，在[官网](https://git-scm.com/downloads)下载最新版git。   Windows为例：双击下一步，，，，直到完成。  
安装完成后，右键单击，出现Git Bash Here 即表示安装成功，可以在此窗口中输入各种git命令（当然，配置好环境变量也可以直接使用Windows自带的cmd窗口）。
![右键弹出git命令输入](https://github.com/xiyixiaodao/xiyixiaodao.github.io/blob/master/_posts/工具/.2019-06-20-Git与GitHub使用_images/babba2af.png?raw=true)
![git bash命令窗口](https://github.com/xiyixiaodao/xiyixiaodao.github.io/blob/master/_posts/工具/.2019-06-20-Git与GitHub使用_images/69fa9e15.png?raw=true)
##### 升级
以Windows为例：  
2.17.1之前用`git update`  
2.17.1之后用`git update-git-for-windows`  
![git升级](https://github.com/xiyixiaodao/xiyixiaodao.github.io/blob/master/_posts/工具/.2019-06-20-Git与GitHub使用_images/7647a4a2.png?raw=true)
##### 配置
初次使用git，需要配置用户名和邮箱，以便后期每次提交记录提交者的信息。
```java
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
```
也可查看配置的信息
```java
git config --list
```

#### 创建仓库
##### 本地创建
```java
git init
```
在本地新建一个文件夹，进入文件夹，运行`git init`命令，这个文件夹之中的内容便交由git版本管理。之后新的文件或修改便可以通过add,commit的方式进行版本控制。   
切记，版本控制实际上有两部分内容，一是普通的文件，另一部分是版本变化的记录内容，以一个隐藏的`.git`文件夹形式存在，所以这个文件夹切记不可删除。

##### 远程克隆
```java
git clong [url]
```
url通过GitHub获取，一般有https和ssh版本，使用ssh需要配置ssh key。例如
![](https://github.com/xiyixiaodao/xiyixiaodao.github.io/blob/master/_posts/工具/.2019-06-20-Git与GitHub使用_images/c53d732b.png?raw=true)   

#### 文件提交
提交文件可以分为三个步骤，新建或修改一个文件后依次需要add->commit->push，才能把文件交由版本控制并推送至远程服务器。
##### add
新建或修改一个文件后并不会直接被git接管，首先需要将文件添加到git的缓存区，这一步骤使用的是`git add`命令。 (以下所说的文件名都包含文件的扩展名)   
- 添加单个文件  
```java
git add file1
```
- 添加多个文件  
 ```java
git add file1 file2 file3       
```
- 添加所有新建或修改的文件（注意：此处`add`和`.`之间有空格）   
```java
git add .    
```
##### commit
##### push

### Git分支
#### 创建与切换分支
#### 合并分支

## 三、GitHub
[GitHub入门官网](https://guides.github.com/activities/hello-world/)  
GitHub is a code hosting platform for version control and collaboration. It lets you and others work together on projects from anywhere.




[https://git-scm.com/book/zh/v2/]: https://git-scm.com/book/zh/v2/