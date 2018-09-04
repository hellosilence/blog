---
layout:     post
title:      "Java设计模式笔记（2）—— Builder模式"
date:       2018-09-03 12:00:00
author:     "Samuel"
tags:
    - 设计模式
    - 笔记
    - Java
---


## 定义
将一个复杂对象的构建与它的表示分离，使得同样的构建过程可以创建不同的表示

## 使用场景
+ 相同的方法，不同的执行顺序，产生不同的事件结果时
+ 多个部件或零件，都可以装配到一个对象中，但是产生的运行结果又不相同时
+ 产品类非常复杂，或者产品类中的调用顺序不同产生了不同的作用
+ 当初始化一个对象特别复杂，如参数多，且很多参数都具有默认值时

## UML 类图
<img src="{{ site.baseurl }}/img/design-pattern-builder-uml.png" alt="UML类图">

## 实现

```java
public class Computer {

    //required parameters
    private String HDD;
    private String RAM;

    //optional parameters
    private boolean isGraphicsCardEnabled;
    private boolean isBluetoothEnabled;


    public String getHDD() {
        return HDD;
    }

    public String getRAM() {
        return RAM;
    }

    public boolean isGraphicsCardEnabled() {
        return isGraphicsCardEnabled;
    }

    public boolean isBluetoothEnabled() {
        return isBluetoothEnabled;
    }

    private Computer(ComputerBuilder builder) {
        this.HDD = builder.HDD;
        this.RAM = builder.RAM;
        this.isGraphicsCardEnabled = builder.isGraphicsCardEnabled;
        this.isBluetoothEnabled = builder.isBluetoothEnabled;
    }

    //Builder Class
    public static class ComputerBuilder {

        // required parameters
        private String HDD;
        private String RAM;

        // optional parameters
        private boolean isGraphicsCardEnabled;
        private boolean isBluetoothEnabled;

        public ComputerBuilder(String hdd, String ram) {
            this.HDD = hdd;
            this.RAM = ram;
        }

        public ComputerBuilder setGraphicsCardEnabled(boolean isGraphicsCardEnabled) {
            this.isGraphicsCardEnabled = isGraphicsCardEnabled;
            return this;
        }

        public ComputerBuilder setBluetoothEnabled(boolean isBluetoothEnabled) {
            this.isBluetoothEnabled = isBluetoothEnabled;
            return this;
        }

        public Computer build() {
            return new Computer(this);
        }

    }

}

```

```java

public class TestBuilderPattern {
    public static void main(String[] args) {
        Computer comp = new Computer.ComputerBuilder("500 GB", "2 GB")
                .setBluetoothEnabled(true)
                .setGraphicsCardEnabled(true)
                .build();
    }
}

```


### 总结

+ 优点
1. 良好的封装性，使用建造者模式可以使客户端不必知道产品内部组成的细节
2. 建造者独立，容易扩展

+ 确定
1. 会产生多余的Builder对象以及Director对象





