---
layout: post
title: Jekyll中的非拉丁字母梗概自适配问题
date: 2018-08-09 19:18:00 +0800
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: 2018-08-09/2018-08-09-JekyllPage.png # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Jekyll, Liquid]
---
写上一篇的时候发现主页面总是模板范例的文章和我自己写的高度不同。查post的css，写的是100%宽度和最低高度11rem, 但是高度会被truncatewords读取的单词数撑开, 格式为英文空格断开的单词数目。  
遂各种谷歌百度必应之
### 方法一 Truncate
用truncate控制显示的梗概字数，这种方法不精确不完美，但是很简便。这也是目前我这个新手使用的方法，本例中配合修改最低高度为13rem，设置“truncate: 70”可确保两者高度肉眼基本一致，如果你看起来不一致可能我眼神不好吧。  
reference: [jekyll/jekyll: How to make "truncatewords" work for non-English characters #732](https://github.com/jekyll/jekyll/issues/732)~

### 方法二 内置标签
在文章post内容中插入自定义的标签以标记梗概的截取位置，具体参考如下  
reference: [Kingauthur's Blog](http://kingauthur.info/2013/01/20/the-paginator-and-excerpt-in-jekyll/)~  

### 方法三 自定义判断长度逻辑
Ruby下判断输入的截取长度，修正见[Fix for [liquid] Make "truncatewords" and "truncate" work for non-English characters (#166) #183](https://github.com/Shopify/liquid/pull/183/commits/80eacde8b03697de0e44aaf442052fb2fc15377f)
    # Truncate a string down to x characters
    def truncate(input, length = 50, truncate_string = "...")
      if input.nil? then return end
      l = length.to_i - truncate_string.length
      l = 0 if l < 0
      a=0
      input.length > length.to_i ? input.chars.take_while{|c| (a += c.bytes.to_a.length) <= length }.join + truncate_string : input
    end

    def truncatewords(input, words = 15, truncate_string = "...")
      if input.nil? then return end
      wordlist = input.to_s.split
      l = words.to_i - 1
      l = 0 if l < 0
      wordlist.length > l ? wordlist[0..l].join(" ") + truncate_string : input
    end  

全部代码见[petetak/liquid/lib/liquid/standardfilters.rb](https://github.com/petetak/liquid/blob/80eacde8b03697de0e44aaf442052fb2fc15377f/lib/liquid/standardfilters.rb)  
reference: [Shopify/liquid: Make "truncatewords" and "truncate" work for non-English characters #166](https://github.com/Shopify/liquid/issues/166)~  

本人一点都不懂Liquid和Ruby, 只能改改模板的水平把，所以我躺下了。  
对，后面俩都没验证呢
