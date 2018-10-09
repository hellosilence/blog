---
layout:     post
title:      "Java设计模式笔记（3）—— 原型模式"
date:       2018-09-04 12:00:00
author:     "Samuel"
tags:
    - 设计模式
    - Java
---


## 定义
用原型实例指定创建对象的种类，并通过拷贝这些原型创建新的对象

## 使用场景
+ 类初始化需要消耗非常多的资源，通过原型拷贝避免这些消耗
+ 通过 new 产生一个对象需要非常繁琐的数据准备或访问权限
+ 一个对象需要提供给其他对象访问，而且各个调用者可能都需要修改其值时，可以考虑使用原型模式拷贝，即保护性拷贝
+ 需要注意的是，通过实现 Cloneable 接口的原型模式在调用 clone 函数构造实例时并不一定比通过 new 操作速度快。只有当通过 new 构造对象较为耗时或者说成本较高时，通过 clone 方法才能获得效率上的提升。

## UML 类图
<img src="{{ site.baseurl }}/img/design-pattern-prototype-uml.png" alt="UML类图">

## 实现

```java
public class WordDocument implements Cloneable {
    private String mText;
    private ArrayList<String> mImages = new ArrayList<>();

    public WordDocument() {
        System.out.println("------- WordDocument 构造函数 -------");
    }

    @Override
    protected WordDocument clone() throws CloneNotSupportedException {
        try {
            WordDocument document = (WordDocument) super.clone();
            document.mText = this.mText;
            document.mImages = this.mImages;
            return document;
        } catch (Exception e) {

        }
        return null;
    }

    public String getText() {
        return mText;
    }

    public void setText(String text) {
        mText = text;
    }

    public ArrayList<String> getImages() {
        return mImages;
    }

    public void addImage(String img) {
        this.mImages.add(img);
    }

    public void showDocument() {
        System.out.println("----- Word content start -----");
        System.out.println("Text: " + mText);
        System.out.println("Images list: ");
        for (String image : mImages) {
            System.out.println("image name: " + image);
        }
        System.out.println("----- Word content end -----");
        System.out.println(" ");

    }
}

```

```java
public class PrototypeTest {
    public static void main(String[] args) {
        WordDocument originDoc = new WordDocument();
        originDoc.setText("This is first document");
        originDoc.addImage("Image 1");
        originDoc.addImage("Image 2");
        originDoc.addImage("Image 3");
        originDoc.showDocument();

        WordDocument doc2 = null;
        try {
            doc2 = originDoc.clone();
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
        doc2.showDocument();

        doc2.setText("This is second document");
        doc2.addImage("Image 4");
        doc2.showDocument();

        originDoc.showDocument();
    }
}

```


### 总结
> 原型模式本质上就是对象拷贝，容易出现的问题时是深拷贝和浅拷贝。使用原型模式可以解决构建复杂对象的资源消耗问题，能够在某些场景下提升创建对象的效率。还有一个重要的用途时保护性拷贝，也就是某个对象对外是只读的，为了防止外部对这个只读对象修改，通常可以通过返回一个对象拷贝的形式实现只读的限制

+ 优点
1. 原型模式是在内存中二进制流的拷贝，要比直接 new 一个对象性能要好很多，特别时要在一个循环体内产生大量对象时，原型模式可以更好地体现其优点

+ 缺点
1. 这既是它的优点也是缺点，直接在内存中拷贝，构造函数不会执行，在实际开发中应该注意这个潜在的问题





