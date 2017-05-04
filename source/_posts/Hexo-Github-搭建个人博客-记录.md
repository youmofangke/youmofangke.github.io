---
title: Hexo & Github 搭建个人博客 记录
date: 2017-05-04 19:57:07
tags: [hexo,GitHub]
---
# 什么是hexo?
hexo 是博客框架，将支持的类型的文件转换成静态Web页面(html+css+JavaScript).
# 什么是 nmp?
表示 Node.js 的开放式模块登记和管理系统: npmjs.org  
表示 Node.js 默认的模块管理器, 可用于下载、安装和管理 Node 模块  
注:npm随node安装无需其他操作
# hexo环境搭建(Windows) 
$符号不要复制  
1. 下载node.js及git并且安装好(默认安装就好了)  
②如果您的电脑中已经安装上述必备程序，那么恭喜您！接下来打开终端(cmd),只需要使用 npm 即可完成 Hexo 的安装。  
```
$ npm config set registry https://registry.npm.taobao.org npm info underscore //更改npm源为淘宝,可以加快hexo下载  
$ npm install -g hexo-cli  //全局安装hexo环境
```
2. 在D盘新建个 blog 博客文件夹  
3. blog文件下右击选择 `Git Bash Here` 执行如下指令   
```
$ hexo init //初始化
$ npm install 
$ npm install hexo-deployer-git --save //安装  git部署插件
```
4. hexo主题安装(下面安装的是next主题)
```
$ git clone https://github.com/iissnan/hexo-theme-next themes/next
```
5. 测试是否成功部署
```
$ hexo clean //清理缓存
$ hexo g //生成静态网页
$ hexo s //开启服务
```
[浏览器输入http://localhost:4000看是否有界面显示](localhost:4000),有就表示部署成功!

## GitHub环境设置
1. 注册一个GitHub账号
2. 新建一个仓库(New repository),仓库命名格式必须为`GitHub用户名`.github.io  
3. 新建仓库时选择公共的(默认是选中的) `public` 
4. 创建好后,进入设置(settings),选择一个主题(Choose a theme)设置完成
##  GitHub与hexo关联
1. 设置Git的user name和email：(第一次配置的话)
```
$ git config --global user.name "GitHub用户名"
$ git config --global user.email "GitHub注册邮箱地址"
```
2. 给本地生成SSH-KEY秘钥
```
$ ssh-keygen -t rsa -C "GitHub邮箱地址"
```
3. 验证SSH-KEY秘钥是否成功
```
$ ssh -T git@github.com //输入此指令后选择yes,然后一直回车.有access字样表示OK了  
```

3. 生成的秘钥默认存在`C:\Users\Administrator\.ssh`中的`id_rsa.pub`文件中,以记事本打开添加到GitHub中去.(怎么添加自行百度)
4. 配置Deployment
站点配置文件`_config.yml`(在blog根目录下),打开找到`Deployment`修改如下:
```
deploy:
  type: git  
  repository: git@github.com:GitHub用户名/GitHub用户名.github.io.git  
  branch: master  
```
## 进阶(更换电脑或更换系统下继续更新博客)
### 前提
1. 现在已经在一台电脑上搭建好hexo，并且已经部署到github pages，可以成功的发布博客
新建分支提交原始文件
2. 初始化
在本地博客根目录输入`git init`，为整个hexo目录初始化git环境
3. 添加远程库
将本地与github上的仓库建立关联
```
$ git remote add origin git@github.com:GitHub用户名/GitHub用户名.github.io.git
```
4. 新建分支hexo并切换到hexo分支
```
$ git checkout -b hexo
```
5. 将hexo生成网站原始的文件提交到hexo分支
```
$ git add -A
$ git commit -m "原始文件"
```
6. 将hexo分支推送到远程库
```
$ git push origin hexo  //现在已经成功备份到hexo分支
```
### 换系统或者换电脑之后的hexo数据恢复
1. 配置环境
首先在新环境下安装Node 、Git
2. 将本地SSH key添加到github
3. 最后不要忘记这两行命令
```
$ git config --global user.name "GitHub用户名"
$ git config --global user.email "GitHub邮箱地址"
```
4. 数据恢复
克隆仓库
```
$ git clone https://github.com/GitHub用户名/GitHub用户名.github.io.git
```
5. 切换到hexo分支
```
$ git checkout hexo
```
6. 安装hexo
```
$ npm install -g hexo-cli
```
7. 安装依赖包
```
$ npm install
```
8. 安装git部署插件
```
$ npm install hexo-deployer-git
```
9. 不需要hexo init这条指令

10. 测试
```
$ hexo g
$ hexo s
```
11. 将博客源文件放到`hexo`分支下,
在hexo分支下写好新博客后执行以下操作
```
$ git add .
$ git commit -m "源文件"
$ git push origin hexo
```
12. 发布网站到master分支上
```
$ hexo g -d
```
13. [原文地址](http://magicroc.com/2017/02/05/%E5%88%A9%E7%94%A8github%E5%88%86%E6%94%AF%E5%A4%9A%E7%94%B5%E8%84%91%E7%BB%B4%E6%8A%A4hexo/)
# 结尾
1. 如果要将博客源文件上传到`hexo'分支下就必须执行如下:
```
$ git add .
$ git commit -m "源文件"
$ git push origin hexo
```
2. 如果只是发布则执行如下:
```
$ hexo g -d
```
3. 可能会出现 failed to push some refs to .. 的错误
>这是因为git仓库中已经有一部分代码，所以它不允许>你直接把你的代码覆盖上去
>可以使用强推，即利用强覆盖方式用你本地的代码替>>代git仓库内的内容
```
$ git push -f origin hexo 
```
>或者先把git的东西fetch到你本地然后merge后再push
```
$ git fetch
$ git merge
```