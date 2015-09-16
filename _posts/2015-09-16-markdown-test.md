---
layout:     post
title:      "是时候认识一位新朋友了——认识 markdown"
date:       2015-09-16 12:00:00
author:     "Samuel"
tags:
    - markdown
---

# 目录

1. [前言](#前言)
   
2. [编辑器出体验](#编辑器初体验)
   
3. [语法](#语法)
   
   ​

## 前言

总会有相见恨晚的时候，markdown 就给了我这种感觉。

了解 markdown 之后，才发现文字能够以如此简单的方式变得优雅。对写作者和设计者来说，对文字排版有更高的要求；但对于一般人，markdown 足以满足需要了。而且markdown 还有程序员喜欢的代码高亮功能。

因此，掌握了 markdown 的语法后，我就开始寻找一款得心应手的工具。不过很遗憾，目前完全满足我要求的 markdown 编辑器还没有发现。仅就我体验过的编辑器来说，Typora 和 Alternote 是其中的佼佼者。

## 编辑器初体验

我使用软件的习惯是，在正式使用之前，体验所有类似功能的软件，寻找最好/适合的软件，然后一直用下去（当然，需求增加导致更换软件也挺正常的），markdown 也一样。我理想中的 markdown 编辑器应该是这样的：

1. markdown 语法支持
2. 界面美观，操作简便
3. 有文档管理功能

怀着这样的期许，开始了漫漫寻觅之路。

1. Mou/MacDown：Mou 其实挺不错的，不少人在用，但是没有代码高亮功能。原作者已经出售了该软件，目前1.0正式版还没有完全发售。MacDown 的作者参考了 Mou 的设计，也有代码高亮功能。但是和 Mou 一样没有文档管理功能。
2. 作业部落：体验过一段时间，功能很丰富，但是没有我想要的。（弱水三千，只取一瓢呀）。它的文档管理不直观，而且很依赖网络。虽然已经出了客户端，但是功能很简陋。此外，所有在线类的编辑器有一个潜在的缺点是：数据安全。个人或者小团队写的软件，可能会因为各种原因导致软件挂了。即使是大公司的产品也不一定非常可靠，比如Google Code. 所以要么文件存储在本地，要么有可靠的云服务。
3. 马克飞象：前面说到数据安全。马克飞象就是专门为印象笔记打造的编辑器。缺点在于文件或者图片稍多，软件会卡顿，同步很慢。
4. Alternote：也是和印象笔记同步的软件。文档管理就是我想要的，而且界面美观！如果markdown 支持得更完善就好了。官网说后续版本会支持，期待中。  
5. Typora：我现在用的 markdown 编辑器，特点是所见所得，而不是一般编辑器的两栏设计（编辑和预览）。还有就是美观，自从使用了 Mac 后，美观的重要性排到第一了（和实用性并列）。

所以，目前电脑上的 markdown 编辑器有三个：Typora，Alternote，MacDown.

接下来测试一下 redcarpet 显示效果。



## 语法

### 标题一

#### 标题二

##### 标题三

### 加粗和倾斜

**加粗**

*倾斜*

### 无序列表

- 苹果
- 香蕉
- 橙子

### 有序列表

1. 第一个
2. 第二个
3. 第三个

### 代码块

``` java

public class IPDemo {
    public static void main(String[] args) throws UnknownHostException {
        InetAddress address = InetAddress.getLocalHost();
        System.out.println(address.toString());
        System.out.println("address "+address.getHostAddress());
        System.out.println("name "+address.getHostName());

        InetAddress address1 = InetAddress.getByName("www.baidu.com");
        System.out.println("address "+address1.getHostAddress());
        System.out.println("name " + address1.getHostName());

        InetAddress[] address2 = InetAddress.getAllByName("www.baidu.com");
        for (int i = 0; i < address2.length; i++) {
            System.out.println("address "+i+" "+address2[i].getHostAddress());

            System.out.println("name "+i+" "+address2[i].getHostName());
        }

    }
}
```

### 行内代码块

`html` `markdown` `我是行内代码块`

### 表格

| Tables        |      Are      |  Cool | 
| ------------- | :-----------: | ----: | 
| col 3 is      | right-aligned | $1600 | 
| col 2 is      |   centered    |   $12 | 
| zebra stripes |   are neat    |    $1 | 

### 引用

> 床前明月光
> 
> 疑似地上霜
> 
> 举头望明月
> 
> 低头思故乡

### 链接

[Google](http://www.google.com) 

### 插入图片

<a href="#">

<img src="{{ site.baseurl }}/img/eagle.jpg" alt="Post Sample Image">

</a>