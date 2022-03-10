---
layout: post
title: 关于Unity中应通过自带的Inputfield Component而不是其下级Text组件的Text Component来修改Inputfield框中文本的笔记
date: 2022-03-10 10:23:00 +0800
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: 2022-03-10/unity-inputfield-text-component-relevant.png # Add image post (optional)
tags: [Jmeter, Regular Expression Extractor] # add tag

---

情况就如同标题一样啊

Unity中UI组件InputField下辖的子节点中有Text节点，且内容文本与Inputfield中输入的内容一致，所以就尝试通过代码对Text节点的text属性进行赋值，但无法成功

遂在官网文档中查找，其中一段说明，对于InputField的文本内容修改需要通过InputField本节点下的Text component( 注意是component, 跟InputField下的Text节点gameobject区分 )

![unity-inputfield-text-component-relevant]({{"/assets/img/2022-03-10/unity-inputfield-text-component-relevant.png"}}){:class="img-responsive"}

原文如下：“

Hints

- To obtain the text of the Input Field, use the text property on the InputField component itself, not the text property of the Text component that displays the text. The text property of the Text component may be cropped or may consist of asterisks for passwords. ”

## 

Ref:

https://docs.unity3d.com/Packages/com.unity.ugui@1.0/manual/script-InputField.html

https://docs.unity3d.com/2019.1/Documentation/Manual/script-InputField.html

https://www.cnblogs.com/jiahuafu/p/8670636.html