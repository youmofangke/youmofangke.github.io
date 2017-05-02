---
title: Oracle高版本导入低版本数据 #文章页面上的显示名称，一般是中文
categories: 数据库 #分类
tags: [Oracle] #文章标签，可空，多标签请用格式，注意:后面有个空格
description: #附加一段文章摘要，字数最好在140字以内，会出现在meta的description里面
---
1.创建一个数据存储操作目录

![](http://upload-images.jianshu.io/upload_images/2981616-6fd455d370a45688.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2.system登录(登录方式用sqlplus与第三发工具都行)执行如下代码
`create directory expdp_dir as 'E:\oralce_backup\';`
3.给予数据库用户操作directory文件夹的读写权限
`grant read,write on directory expdp_dir to QIMS36SYS; `//QIMS36SYS是数据库其中的用户名

4.获取低版本的oracle版本号(只列出了一种方法)
`select * from v$version;`

![](http://upload-images.jianshu.io/upload_images/2981616-43dd4ffe8a129fc7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4.进入CMD窗口 直接输入 导出数据
`expdp SYSTEM/SYSTEM@QIMS36 directory=expdp_dir dumpfile =QIMS36SYS.dmp schemas=QIMS36SYS logfile=11.log version=10.2.0.4.0`

5.操作低版本数据库 重复1-3步骤
6.进入CMD窗口 直接输入 导入数据到低版本
`impdp userid='SYSTEM/SYSTEM@QIMS36 as sysdba' schemas=QIMS36SYS directory=expdp_dir dumpfile =QIMS36SYS.dmp  logfile=imp1.log`