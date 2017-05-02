---
title: Oracle 卸载 不干净 彻底删除 #文章页面上的显示名称，一般是中文
categories: 数据库 #分类
tags: [Oracle] #文章标签，可空，多标签请用格式，注意:后面有个空格
description: #附加一段文章摘要，字数最好在140字以内，会出现在meta的description里面
---
①关闭oracle相关的服务
②注册表删除(可能因为oracle及windows的版本不同注册表信息也有**些差异**):
③开始è输入regedit打开注册表编辑器删除下面的目录
```HKEY_CLASSES_ROOT```目录下所有以``Ora``、```Oracle```、```Orcl```或```EnumOra```为前缀的键。
```HKEY_CURRENT_USER/SOFTWARE/Microsoft/windows/CurrentVersion/Explorer/MenuOrder/Start Menu/Programs```中所有以```oracle``` 开头的键。
```HKEY_LOCAL_MACHINE\SOFTWARE```中以```oracle```字样开头的文件
```HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\ Services```中以```oracle ```字样开头的文件
```HKEY_LOCAL_MACHINE\SYSTEM\ControlSet002\ Services```中以```oracle``` 字样开头的文件
```HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services```中以```oracle``` 字样开头的文件
```HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\EventLog\Application```中以```oracle```字样开头的文件
```HKDY_LOCAL_MACHINE/SOFTWARE/ODBC/ODBCINST.INI```中除```Microsoft ODBC for Oracle```注册表键以外的所有含有```Oracle```的键。
④删除环境变量path中关于oracle的内容,鼠标右键右单击"我的电脑属性高级环境变量PATH 变量(删除之前最好先备份一份到文本中)
删除环境变量中的```PATHT CLASSPATH```中包含Oracle的值。
删除“开始”/“程序”中所有Oracle的组和图标。
删除所有与Oracle相关的目录，包括：（1）、c:\Program file\Oracle目录。 （2）、ORACLE_BASE目录。（3）、c:\Documents and Settings\系统用户名、LocalSettings\Temp目录下的临时文件
⑤重启电脑将```C:\Program Files (x86)\Oracle ```, C:\Program Files\Oracle与 C:\app (此为oracle安装目录)及其子文件等oracle安装目录文件全部删除
到此oracle就删除了,如果还是不行==>重新装系统了