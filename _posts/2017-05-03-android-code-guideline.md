---
layout:     post
title:      "Android 代码命名规范"
date:       2017-05-03 12:00:00
author:     "Samuel"
tags:
    - Android
    - 学习笔记
---

## 命名方法

1. 大驼峰式命名法
	
	每个单词的第一个字母都大写
   
2. 小驼峰式命名法

	除了第一个单词，每个单词的第一个字母都大写
   
3. 下划线命名法

	单词与单词间用下划线做间隔
   
4. 匈牙利命名法

	基本原则是：变量名=属性+类型+对象描述


## Android 命名规范

### 包命名规范

采用**反域名命名规则**，包名全部小写，连续的单词只是简单地连接起来，不使用下划线，一级包名为com，二级包名为xxx（可以是公司域名或者个人命名），三级包名根据应用进行命名，四级包名为模块名或层级名。如：

`com.isa.crm.activity`, `com.isa.crm.adapter`

### JAVA类命名规范

采用**大驼峰式命名法**，尽量避免缩写，除非该缩写是众所周知的，比如HTML，URL,如果类名称包含单词缩写，则单词缩写的每个字母均应大写。如：

`ProductListActivity`，`ProductListAdapter`，`JsonHTTPSRequest`

### 接口命名规范

命名规则与类一样采用**大驼峰命名法**，多以`able`或`ible`结尾。例如：

`interface Runable`，`interface Accessible`

### 成员变量命名规范

采用**小驼峰命名法**

1. 临时变量命名
   
   使用标准的Java命名方法，不推荐使用Google的m命名法。例如：
   
   `private String userName`
   
2. 常量命名
   
   常量使用全大写字母加下划线的方式命名，例如：
   
   `public static final String TAG = "tag”;`
   
3. 控件实例命名
   
   不少文章说，类中控件名称必须与xml布局id保持一致，个人对这条存疑，我是这么做的：
   
   布局文件中Button的id为`android:id="@+id/btn_pay_main”`(main是xml文件对应的Activity或其他）
   
   类中的对象名称则为`private Button btnPayMain`,这是Android Studio中的`Android Layout ID Converter`插件自动生成的。

### 方法命名规范

动词或动名词，采用小驼峰命名法。例如:

`run()`,`onCreate()`,`syncProducts()`

|方法|说明|
|----------- | ---------------------------------------- | 
|initXX()    | 初始化相关方法,使用init为前缀标识，如初始化布局initView()     | 
|isXX()      | checkXX()方法返回值为boolean型的请使用is或check为前缀标识 | 
|getXX()     | 返回某个值的方法，使用get为前缀标识                      | 
|processXX() | 对数据进行处理的方法，尽量使用process为前缀标识              | 
|displayXX() | 弹出提示框和提示信息，使用display为前缀标识                | 
|saveXX()    | 与保存数据相关的，使用save前缀标识                      | 
|resetXX()   | 对数据重组的，使用reset前缀标识                       | 
|clearXX()   | 清除数据相关的                                  | 
|removeXXX() | 清除数据相关的                                  | 
|drawXXX()   | 绘制数据或效果相关的，使用draw前缀标识                    | 

### 布局文件（`layout`）命名规范

全部小写，采用下划线命名法。

activity layout：`activity_main`

fragment layout: `fragment_shopping`

Dialog layout: `dialog_loading`

### 资源 ID 命名规范

（个人习惯）命名模式为：`{view_name}_{view 描述}_{xml关联的 Activity}`，例如：

`btn_send_main`

常见控件View与其缩写对照参考表如下:

| 控件             | 缩写     | 控件          | 缩写     | 
| -------------- | ------ | ----------- | ------ | 
| LinearLayout   | ll     | DatePicker  | dtPk   | 
| RelativeLayout | rl     | EditText    | edt    | 
| TextView       | tv     | TimePicker  | tmPk   | 
| Button         | btn    | ProgressBar | proBar | 
| ImageButton    | imgBtn | WdbView     | wv     | 
| ImageView      | iv     | Spinner     | spn    | 
| CheckBox       | cbx    | ScollView   | sv     | 
| RadioButton    | rBtn   | ListView    | lv     | 

### 图片资源文件命名

| 命名          | 说明                                | 
| ----------- | --------------------------------- | 
| bg\_xxx     | 这种图片一般那些比较大的图片，比如作为某个Activity的背景等 | 
| btn\_xxx    | 按钮，一般用于按钮，而且这种按钮没有其他状态            | 
| ic\_xxx     | 图标，一般用于单个图标，比如启动图片ic_launcher     | 
| bg\_描述\_状态  | 用于控件上的不同状态                        | 
| btn\_描述\_状态 | 用于按钮上的不同状态，比如normal，press         | 
| chx\_描述\_状态 | 选择框                               | 

## 代码风格

### 大括号风格

行尾和换行（IDE 一般都有代码自动格式化，可以自己修改）

### 空格

`if else`，`while`,`运算符`等后面需用空格隔开

### 方法参数

当方法参数数量过多时，需进行换行处理

### 注释

1. 必须要对所有实例变量、类常量进行注释说明
2. 必须对所有的类、接口进行注释说明
3. 必须对所有的方法进行注释说明


本文参考自：

>   [最佳实践之Android代码规范](http://www.androidchina.net/2141.html)
>  
>   [Android 命名规范 （提高代码可以读性）](http://blog.csdn.net/vipzjyno1/article/details/23542617)





   ​


