---
layout: post
title: 关于Unity 2017.1~4 遇到卡Start界面问题一种情况
date: 2018-08-08 23:00:00 +0800
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: 2018-08-08/2018-08-08-Unity-Stuck-On-Starting.png # Add image post (optional)
tags: [Unity3D, License] # add tag

---
自从Unity更新2017以后，一直有用户报卡启动界面Bug。从论坛的反馈来看，各人的情况还略有不同，目前没看到相对通用的解决办法。这边记录下我的问题和解决。
## 问题
Unity启动时无限卡启动界面看不到项目目录，断网状态可以使用，修改host禁用Unity更新服务器地址无效  
UnityErrorLog主要部分如下(因截图时在尝试修复，固Log后别的内容略去)  
![UnityErrorLog]({{ "/assets/img/2018-08-08/2018-08-08-Unity-Stuck-On-Starting.png" | absolute_url }}){:class="img-responsive"}
大概能看到有字体内容读不到，回滚失败blabla，不是很懂Unity的报错规范。
然后查到这里[https://forum.unity.com/threads/unity-wont-start-up-and-keeps-flashing.503993/](https://forum.unity.com/threads/unity-wont-start-up-and-keeps-flashing.503993/)有类似的问题。
最终我的解决办法是删除了两个有关证书的文件。  
注意看上面这个帖子中的10楼，macOS下 “~/Library/Application Support”指的是“/Users/your username/Library/Application Support”,而 “/Library/Application Support/Unity” 是从“Macintosh HD”或“Root"进入的，在删除后者中的相关文件后，重启Unity。此时Unity能够正常Loading到账号密码绑定License的界面，重新绑定后可正常使用。  
但此版本系从论坛等地的未解决Issue看，依旧存在官方尚未修复的其他无法登陆Bug 
[bla](https://forum.unity.com/threads/cannot-open-projects-in-online-mode.497855/) ~
[bla](https://answers.unity.com/questions/1305457/unity-editor-wont-open-project.html) ~ 
[bla](https://forum.unity.com/threads/unity-doesnt-open-from-unity-hub.524320/) ~ 
[bla](https://forum.unity.com/threads/unity-launching-fail.497989/)