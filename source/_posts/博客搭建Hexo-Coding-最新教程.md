---
title: 博客搭建Hexo+Coding(最新教程)
author: xiao xing
summary: 最新的Coding部署教程，搭建静态博客，可绑定私人域名
categories: 网站搭建
tags:
  - blog
  - hexo
abbrlink: 26283
date: 2020-04-22 10:56:51
---
# 1. Hexo搭建
## 1.nodejs，Git环境搭建： 

- [node.js搭建](https://blog.csdn.net/qq_43285335/article/details/90696126) 
- [git搭建](https://www.cnblogs.com/xueweisuoyong/p/11914045.html)- 
  [淘宝云配置](https://www.cnblogs.com/luyuandatabase/p/12145707.html) 

## 2.注册github 

1. 注册就不用我说了，创建仓库视频里有，然后这个也很简单，不会就百度（应该没人去百度
   的，太简单了）
2. 格式要求：gfyuan.github.io

## 3.快速利用hexo搭建博客：

 1.[Hexo脚本教程](https://hexoscript.gitbook.io/hexo-script/)  

 2.[主题安装及优化](https://github.com/blinkfox/hexo-theme-matery/blob/develop/README_CN.md)  
 # 2.Coding创建项目 
 ### 1.首先，去Coding[官网注册](coding.net)一个账号，接着，点击“+ 创建项目”,创建一个新项目。
 - 选择项目模板 
 ![](https://cdn.jsdelivr.net/gh/MoreInterests/CDN/P052211.jpg)
- 创建项目 
![](https://cdn.jsdelivr.net/gh/MoreInterests/CDN/P052212.jpg) 
### 2.同步本地hexo到coding上
把获取到了ssh配置在上面的`_config.yml`文件中的deploy下，
```
deploy:
   type: git
    repo: 
        github: git@github.com:你的用户名/你的仓库名.github.io.git
        coding: git@e.coding.net:你的用户名/你的仓库名.git
    branch: master
 ```  
如果是第一次使用coding的话，需要设置SSH公钥，生成的方法可以参考[coding帮助中心](https://help.coding.net/)   

当然这里直接使用之前部署github时已经生成的公钥。  
![](https://cdn.jsdelivr.net/gh/MoreInterests/CDN/P052213.jpg)    

添加后，在`git bash`命令输入：
```
ssh -T git@git.coding.net
```  
如果得到下面提示就表示公钥添加成功了：
```
Coding.net Tips : [Hello ! You've conected to Coding.net by SSH successfully! ]
```  

最后使用部署命令就能把博客同步到coding上面：
``` 
hexo g -d
```  

![](https://cdn.jsdelivr.net/gh/MoreInterests/CDN/P052214.jpg) 
  
# 3.pages服务方式部署  
- 你在你的仓库里是找不到pages页面的需要进行以下操作   
 ![](https://cdn.jsdelivr.net/gh/MoreInterests/CDN/P1.png)   
 - 勾选上持续部署和持续集成 
 ![](https://cdn.jsdelivr.net/gh/MoreInterests/CDN/P2.png) 
 ![](https://cdn.jsdelivr.net/gh/MoreInterests/CDN/P3.png)  
 ![](https://cdn.jsdelivr.net/gh/MoreInterests/CDN/P4.png)  
 ![](https://cdn.jsdelivr.net/gh/MoreInterests/CDN/P5.png)  
然后就可通过访问地址访问自己的博客啦！
  
- 如果你有自己的私人域名也可以绑定自己的域名  
![](https://cdn.jsdelivr.net/gh/MoreInterests/CDN/P6.png)  
![](https://cdn.jsdelivr.net/gh/MoreInterests/CDN/P7.png)  然后在你的域名服务台解析到你的博客访问地址即可通过域名访问博客。  
  
    
        
> <font color="ff0000">版权声明：本文为个人总结，欢迎转载，转载请注明出处，勿用于商业用途！</font>  
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=1443900438&auto=1&height=66"></iframe>