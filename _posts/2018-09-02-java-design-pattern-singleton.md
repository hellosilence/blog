---
layout:     post
title:      "Java设计模式笔记（1）—— 单例模式"
date:       2018-09-02 12:00:00
author:     "Samuel"
tags:
    - 设计模式
    - Java
---


## 定义
确保某一个类只有一个实例，而且自行实例化并向这个系统提供这个实例
## 使用场景
确保某个类有且只有一个对象的场景，避免产生多个对象消耗过多的资源，或者某种类型的对象只应该有且只有一个。例如，创建一个对象需要消耗的资源过多，如要访问 IO 和数据库等资源，这时就要考虑使用单例模式了

## UML 类图
<img src="{{ site.baseurl }}/img/design-pattern-singleton-uml.png" alt="UML类图">

## 实现
### 懒汉模式

```java

public class Singleton {
    private static Singleton instance;

    private Singleton() {
    }

    public static synchronized Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

+ 优点：在使用时才会被实例化，节约资源
+ 缺点：第一次加载时需要进行实例化，反应稍慢，最大的问题是每次调用 getInstance 都进行同步，造成不必要的同步开销

### Double Check Lock(DCL)实现单例
```java
public class Singleton {
    private static Singleton mInstance;

    private Singleton() {
    }

    public static Singleton getInstance() {
        if (mInstance == null) {
            synchronized (Singleton.class) {
                if (mInstance == null) {
                    mInstance = new Singleton();
                }
            }
        }
        return mInstance;
    }
}
```

+ 优点：第一次执行 getInstance 单例对象才会被实例化，效率高
+ 缺点：第一次加载时反应稍慢，也由于 Java 内存模型的原因偶尔会失败

### 静态内部类
```java
public class Singleton {
    private Singleton() {
    }

    public static Singleton getInstance() {
        return SingletonHolder.sInstance;
    }

    private static class SingletonHolder {
        private static final Singleton sInstance = new Singleton();
    }
}
```

+ 既能确保线程安全，也能保证单例对象的唯一性

### 其他
+ 枚举单例
+ 使用容器实现单例




