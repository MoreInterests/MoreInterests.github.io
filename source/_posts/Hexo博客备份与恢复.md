---
title: Hexo博客备份与恢复
top: false
cover: false
toc: true
mathjax: false
author: xiao xing
summary: 保存和备份是非常重要的，所以务必养成随手保存和存有备份的习惯了。
tags: 
    - hexo 
    - github
categories: 网站搭建
abbrlink: 27743
date: 2020-05-01 17:54:18
img: https://cdn.jsdelivr.net/gh/MoreInterests/CDN/P05231.jpg
coverImg:
password:
---
--- 
# 备份  
1、在你的博客仓库创建一个分支`hexo`（这个命名随意）；

2、设置`hexo`为默认分支（不知道怎么设的可以百度）；
( <font color="ff0000">第一步和第二步都在[github](https://github.com/)网站中操作</font>)  

3、将博客仓库`hexo分支`clone至本地，  
在本地新建一个文件夹`hexo`，并在此文件夹中右击鼠标打开`git bash`,执行命令  
```  
git clone git@github.com:Username/Username.github.io.git  
```    
(<font color="ff0000">`Username`为你自己的名字</font>)    
克隆完之后在`hexo`文件夹中会出现新的Username.github.io文件夹，将其中的文件全部删除，只保留`.git\`文件夹。

将之前的博客根目录文件夹中的
`_config.yml`，`themes/`，`source`，`scffolds/`，`package.json`，`.gitignore`复制到Username.github.io文件夹；（`Username`是你自己的用户名）

4、将themes/next/(是NexT主题)中的`.git/`删除，否则无法将主题文件夹`push`；( <font color="ff0000">`matery`主题中没有这个文件夹，应该就不用删除了</font>)

5、在Username.github.io文件夹执行`git add .`，`git commit -m "提交文件"`，`git push origin hexo`来提交hexo网站源文件；( <font color="ff0000">命令中的`hexo`为你创建的分支的名字</font>)    

6、执行`hexo g -d `生成静态网页部署到github上。
这样，Username.github.io仓库就有master分支保存静态网页，hexo分支保存源文件。  
到这里备份就完成了。  
  
# 写博客   
## ( <font color="ff0000">此后所有的博客操作都在Username.github.io文件夹中进行</font>)   

### 在本地对博客修改（包括修改主题样式、发布新文章等）后在Username.github.io文件夹中依次执行命令  
```  
git add .  
git commit -m "提交文件  
git push origin hexo  
hexo g -d  
```  
即在每次修改完本地博客后重复执行5、6步来完成来提交hexo网站源文件和生成静态网页部署到github上。  
# 恢复博客  
  
换电脑想改博客：  

1、安装git；  

2、安装Nodejs和npm；  

3、使用克隆命令`git clone git@github.com:Username/Username.github.io.git`将仓库拷贝至本地；  

4、在文件夹内执行命令`npm install hexo-cli -g`、`npm install`、`npm install hexo-deployer-git`；

## 添加ssh-keys
在终端下运行：`ssh-keygen -t rsa -C "yourname@email.com"`，一路回车；
会在.ssh目录生成`id_rsa`、`id_rsa.pub`两个文件，这就是密钥对，`id_rsa`是私钥，千万不能泄漏出去；  

登录[Github](https://github.com/)，打开「Settings」-->「SSH and GPG keys」，然后点击「new SSH key」，填上任意Title，在Key文本框里粘贴公钥`id_rsa.pub`文件的内容，注意不要粘贴成`id_rsa`，最后点击「Add SSH Key」。

 > <font color="ff0000">版权声明：本文为个人总结，欢迎转载，转载请注明出处，勿用于商业用途！</font>   
    
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=1449991947&auto=1&height=66"></iframe>
