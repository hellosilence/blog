---
layout:     post
title:      "macOS crontab 定时任务配置"
date:       2017-12-04 12:00:00
author:     "Samuel"
tags:
    - macOS
    - linux
---

## 开启 crontab
+ 查看 crontab 是否启动

	`sudo launchctl list | grep cron`
+ 检查需要的文件

	`ls -al /etc/crontab`

+ 如果 crontab 文件不存在则创建

	`sudo touch /etc/crontab`

## crontab 命令参数
+ -u user：用来设定某个用户的crontab服务；
+ file：file是命令文件的名字,表示将file做为crontab的任务列表文件并载入crontab。如果在命令行中没有指定这个文件，crontab命令将接受标准输入（键盘）上键入的命令，并将它们载入crontab。
+ -e：编辑某个用户的crontab文件内容。如果不指定用户，则表示编辑当前用户的crontab文件。
+ -l：显示某个用户的crontab文件内容，如果不指定用户，则表示显示当前用户的crontab文件内容。
+ -r：从/var/spool/cron目录中删除某个用户的crontab文件，如果不指定用户，则默认删除当前用户的crontab文件。
+ -i：在删除用户的crontab文件时给确认提示。

> 在使用crontab执行脚本时，如果没有执行任务，请查看crontab和脚本是否开启执行权限
>
> eg: */1 * * * * /bin/date >> /User/Username(你的用户名)/time.txt表示每分钟输出当前时间到time.txt上
>


如果出现以下问题


```
[hayek@mac:/www/] 02:33:22 PM: crontab -e
crontab: no crontab for hayek - using an empty one
crontab: "/usr/bin/vi" exited with status 1
```

1. 方法1：`EDITOR=vim crontab -e` 直接编辑，以后直接`crontab -e`直接打开就行。
2. 方法2：export EDITOR=vim
3. 方法3：向cron进程提交一个crontab文件之前，首先要设置环境变量EDITOR。cron进程根据它来确定使用哪个编辑器编辑crontab文件。9 9 %的UNIX和LINUX用户都使用vi，如果你也是这样，那么你就编辑$HOME目录下的. profile文件，在其中加入这样一行:`EDITOR=vi; export EDITOR`


## crontab的文件格式
+ 第1列：分钟，0～59
+ 第2列：小时，0～23（0表示子夜）
+ 第3列：日期，1～31
+ 第4列：月份，1～12
+ 第5列：星期，0～7（0和7表示星期天）
+ 第6列：要运行的命令（如果有多个命令用 && 隔开）

### 特殊字符

+ 星号（*）：代表所有可能的值，例如month字段如果是星号，则表示在满足其它字段的制约条件后每月都执行该命令操作。
+ 逗号（,）：可以用逗号隔开的值指定一个列表范围，例如，“1,2,5,7,8,9”
+ 中杠（-）：可以用整数之间的中杠表示一个整数范围，例如“2-6”表示“2,3,4,5,6”
+ 正斜线（/）：可以用正斜线指定时间的间隔频率，例如“0-23/2”表示每两小时执行一次。同时正斜线可以和星号一起使用，例如*/10，如果用在minute字段，表示每十分钟执行一次。


### 实例
1. 每1分钟执行一次

	*/1 * * * *
2. 每小时的第3和第15分钟执行

	3,15 * * * *
3. 每隔两天的上午8点到11点的第3和第15分钟执行

	3,15 8-11 */2 * *
4. 每个星期一的上午8点到11点的第3和第15分钟执行

	3,15 8-11 * * 1

## 备份/恢复 crontab

```
备份
crontab -l > $HOME/.mycron
恢复
crontab $HOME/.mycron
```



## crontab服务的重启关闭，开启

+ mac系统下

	```
	sudo /usr/sbin/cron start
	sudo /usr/sbin/cron restart
	sudo /usr/sbin/cron stop
	```

+ ubuntu:

	```
	sudo /etc/init.d/cron start
	sudo /etc/init.d/cron stop
	sudo /etc/init.d/cron restart
	```

## 日志
+ 默认

	不做任何处理，日志会发送到/var/mail/Username

+ 重定向

	```
	* * * * * command >> /Users/Samuel/Desktop/command.log 2>&1
	```
	2>&1 表示把标准错误输出重定向到与标准输出一致，即command.log

+ 月份重命名

	```
	0 12 * * * command >> "/Users/Samuel/Desktop/$(date +"\%Y-\%m").log" 2>&1
	```
+ 星期重命名

	```
	0 12 * * * command >> "/Users/Samuel/Desktop/$(date +"\%Y-W\%W").log" 2>&1
	```
+ 小时重命名

	```
	0 12 * * * command >> "/Users/Samuel/Desktop/$(date +"\%Y-\%m-\%d_\%H").log" 2>&1
	```

## 其他
+ 环境变量问题，尽量使用绝对路径
+ python编码问题

	`export LANG=zh_CN.UTF-8`
