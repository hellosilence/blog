---
layout:     post
title:      "markdown语法测试3"
date:       2015-09-09
author:     "Samuel"
tags:
    - markdown
    - test
---

[Google](http://www.google.com) 这是链接

这是表格

| 1    | 1    | 1    | 
| ---- | ---- | ---- | 
| 2    | 2    | 2    | 
| 3    | 3    | 3    | 
| 4    | 4    | 4    | 


| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |

```java
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


引用

> 床前明月光
> 
> 疑似地上霜
> 
> 举头望明月
> 
> 低头思故乡

插入图片
<a href="#">
    <img src="{{ site.baseurl }}/img/macapp.png" alt="Post Sample Image">
</a>





