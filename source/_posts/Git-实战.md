---
title: Git-实战
top: false
cover: false
toc: true
mathjax: false
author: xing xiao
tags: Git
categories: 仓库
abbrlink: 53724
date: 2020-07-02 23:23:16
img:
coverImg:
password:
summary:
---

# Git实战

## 安装

使用普通用户登录到虚拟机

```bash
sudo apt install git
```

## 配置

Git在使用之前需要配置用户名和电子邮箱地址，否则不能提交代码。

```bash
# 配置用户名
git config --global user.name "刘煜"
# 配置email
git config --global user.email "liuy_xa@hqyj.com"
```

--global 表示全局配置，对当前用户的所有代码库生效。

查看配置

```bash
git config --list
```

## 基本概念

工作目录（working directory）：放代码的目录，在此目录下编辑代码。

代码库（repository）：保存代码的版本数据库。

提交（commit）：将工作目录中的代码保存到代码库。

检出（checkout）：将代码从代码库恢复到工作目录中。

暂存区（staging area）：相当于购物车，因为一次提交的内容必须是完整的，涉及一个问题或特性修改的所有文件，可以将修改的文件先保存到暂存区，然后统一提交到代码库。

## 保存代码

```bash
# 创建工作目录
mkdir smart_speaker

# 进入工作目录
cd smart_speaker

# 创建本地代码库
git init
```

工作目录中的`.git`目录就是本地代码库。

注意：Linux中以句点开头的目录或文件是隐藏的，需要用`ls -a`显示。

```bash
# 查看工作区状态
git status
```

未跟踪文件：工作目录中没有保存到代码库的文件。

```bash
# 将文件修改保存到暂存区
git add 文件名/目录名
```

注意：空目录不能添加到暂存区。

```bash
# 将暂存区的修改提交到代码库
git commit
```

git commit命令会调用GNU Nano文本编辑器，用户需要在编辑器中填写提交日志，否则不能提交。

```bash
# 不打开文本编辑器，通过git命令行指定提交日志
git commit -m "提交日志"
```

提交日志中一般写问题或新特性的编号和名称。

## 比较差异

```bash
# 查看提交历史记录
git log
# 比较版本之间的差异
git diff 提交ID

```

提交ID可以使用HEAD别名代替，也可以使用ID的前7字符代替。

HEAD表示代码库中的最新版本

HEAD^ 表示最新版本的上一个版本

HEAD^2 表示最新版本的上2个版本

## 恢复

```bash
# 将工作目录中的文件恢复为代码库中的最新版本
git checkout HEAD .

```

句点表示要恢复所有文件，如果只恢复一个文件可以把句点换成要恢复的文件名。

## 文件重命名和删除

```bash
# 重命名工作目录中的文件
git mv 原文件名 新文件名
git commit -m "提交日志"

# 删除工作目录中的文件
git rm 文件名
git commit -m "提交日志"

```

## 远程代码库

注册码云账号：https://gitee.com



## 下载远程代码库

进入码云的代码库主页，点击`克隆/下载`按钮，复制远程代码库地址。

![](https://cdn.jsdelivr.net/gh/MoreInterests/CDN/PInkedimage-20200630145414459_LI.jpg)

使用`git clone`命令下载代码库到本地，会在当前目录下创建同名工作目录和本地代码库。

```bash
git clone https://gitee.com/hqyjxa/XPU-SmartSpeaker-Lab2020.6.git

```

注意：PuTTY中选中文本即复制，鼠标右键粘贴。

## 同步本地代码库到远程

在本地工作目录中执行

```bash
git push

```

## 同步远程代码库到本地

```bash
git pull

```

## 关注和点赞

用户可以关注某个代码库（点击代码库主页上的watch按钮），对此代码库的所有修改会通知此用户。

用户可以给代码库点赞（点击代码库主页上的star按钮），此代码库地址会记录到用户的收藏夹中。

![](https://cdn.jsdelivr.net/gh/MoreInterests/CDN/PInkedimage-20200630151130034_LI.jpg)

## 提交PR（Pull Request）

Git代码库一般使用Fork-PR流程实现团队开发。

1. 点击代码库库主页上的Fork按钮，复制远程代码库到自己的账号。

![](https://cdn.jsdelivr.net/gh/MoreInterests/CDN/Pimage-20200630151712465.png)

2. 用户修改副本代码库中的内容。
   1. 克隆副本代码库到本地（git clone）
   2. 修改工作目录中的文件
   3. 将工作目录中的修改提交到本地代码库（git add/git commit）
   4. 将本地代码库的修改同步到远程副本代码库中（git push），注意需要输入码云的账号和密码，密码不会回显。
3. 创建PR（Pull Request）

相当于给主代码库的管理员发送邮件，请求将自己的修改合并到主代码库中。

![image-20200630152843700](F:/%E4%B9%A6%E7%B1%8D/%E4%B8%93%E4%B8%9A/%E7%94%9F%E4%BA%A7%E5%AE%9E%E4%B9%A0/%E5%8D%8E%E6%B8%85%E8%BF%9C%E8%A7%81%E5%AE%9E%E4%B9%A0%E6%97%A5%E5%BF%97/XPU-SmartSpeaker-Lab2020.6/notes/Git%E5%AE%9E%E6%88%98.assets/image-20200630152843700.png)

填写PR的标题，描述，然后点击`创建`按钮。

![](https://cdn.jsdelivr.net/gh/MoreInterests/CDN/Pimage-20200630153329594.png)

PR创建后，可以在主代码库的PR列表中看到。

![](https://cdn.jsdelivr.net/gh/MoreInterests/CDN/PInkedimage-20200630153834708_LI.jpg)

![](https://cdn.jsdelivr.net/gh/MoreInterests/CDN/PInkedimage-20200630153926248_LI.jpg)

4. 主代码库管理员，点击`合并`按钮后，就可以将副本代码库中的修改合并到主代码库中。



![](https://cdn.jsdelivr.net/gh/MoreInterests/CDN/Pimage-20200630154126462.png)

