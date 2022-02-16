---
layout: post
title: 关于用Jmeter正则提取器提取数字给条件判断事务器用的笔记
date: 2022-01-28 15:46:00 +0800
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: 2022-01-28/调试后置处理器回显未查到.png # Add image post (optional)
tags: [Jmeter, Regular Expression Extractor] # add tag
---
因为一个需求要测抽奖的页面，所以打算做一个脚本时抽到以后，再执行后续的接口调用（比如捐款等，期望是类似生产实际场景
## 问题
### 1 正则问题 

首先是在取抽奖接口返回值的时候遇到了取不到一个判断值的数字问题，因为一开始抄的是通用的模板，在Jmeter的正则提取器Regular Expression参数一栏输入

```json
.*"count":"(.+?)".*
```

然后调试可以看到

![调试错误结果]({{ "/assets/img/2022-01-28/调试后置处理器回显未查到.png" }}){:class="img-responsive"}

```json
.*"count":"*?([0-9]+).*?".*
```

网上还有看到一个版本是

```json
<span>\D+(\d+)\D+<\/span>
```

啊，不过不是很会用，没验证还，参考链接已付

### 2 If  Controller问题

在If Controller中录入表达式

```json
${count} != 0
```

此时判断未生效（已确认返回值不为0）

然后使用Jmeter建议的

```json
${__jexl3(${count} != 0)}
```

此时判断控制器下的脚本正常执行

看别人写的很多例子上面一种应该也行才对，不知道为啥T^T

Ref:

https://stackoverflow.com/questions/35598164/jmeter-regular-expression-to-extract-a-number-having-varying-boundaries

https://jmeter.apache.org/usermanual/component_reference.html#If_Controller

https://tipsfordev.com/if-else-block-in-jmeter