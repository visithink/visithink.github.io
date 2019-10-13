---
title: CentOS 7 yum 安装 Nginx
layout: post
New field 2: CentOS 7 yum 安装 Nginx
date: '2018-12-23 09:30:00'
description: linux nginx
tags: [linux,nginx]
---

 # 1.添加Nginx到YUM源
添加CentOS 7 Nginx yum资源库,打开终端,使用以下命令:
```base
sudo rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
```

 # 2.安装Nginx
在你的CentOS 7 服务器中使用yum命令从Nginx源服务器中获取来安装Nginx：
```base
sudo yum install -y nginx
```
Nginx将完成安装在你的CentOS 7 服务器中。

# 3.启动Nginx
刚安装的Nginx不会自行启动。运行Nginx:
```
sudo systemctl start nginx.service
```
如果一切进展顺利的话，现在你可以通过你的域名或IP来访问你的Web页面来预览一下Nginx的默认页面；

# 4.CentOS 7 开机启动Nginx
```
sudo systemctl enable nginx.service
```
更多systemctl命令可查看[《systemctl命令用法》](http://www.9696e.com/archives/1253)

Nginx配置信息
网站文件存放默认目录
```base
/usr/share/nginx/html
```
网站默认站点配置
```base
/etc/nginx/conf.d/default.conf
```
自定义Nginx站点配置文件存放目录
```base
/etc/nginx/conf.d/
```
Nginx全局配置
```base
/etc/nginx/nginx.conf
```
Nginx启动
```base
nginx -c nginx.conf
```
在这里你可以改变设置用户运行Nginx守护程序进程一样,和工作进程的数量得到了Nginx正在运行,等等。
Linux查看公网IP
您可以运行以下命令来显示你的服务器的公共IP地址:
```base
ip addr show eth0 | grep inet | awk '{ print $2; }' | sed 's/\/.*$//'
```