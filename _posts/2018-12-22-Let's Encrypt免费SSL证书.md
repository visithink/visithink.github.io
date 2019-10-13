---
title: 免费 https 证书(Let's Encrypt）
New field 1: 免费 https 证书(Let's Encrypt）
layout: post
date: '2018-12-22 10:00:00'
description: 免费 https 证书(Let's Encrypt）
tags: [SSL]
---

					
					
					
要知道要在自己的网站上使用HTTPS,需要我们从证书签发机构（CA）获取证书（一种文件）目前也有很多签发机构，但是价格不菲，对于我们这种有高度网络开源精神的人（穷）来说肯定不会就此屈服的，所以我选择了[Let's Encrypt](https://letsencrypt.org/)，Let’s Encrypt是一个免费的，自动化和开放的证书颁发机构（CA），为公众的利益服务。 它是由互联网安全研究组织（ISRG）提供的服务。Let’s Encrypt为用户提供所需的数字证书，以便用户能免费为网站启用HTTPS（SSL / TLS）。Let’s Encrypt这样做是想要创建一个更安全，更具隐私性的Web空间。

为了从Let's Encrypt获取您网站域名的证书，你必须证明对域名的控制权。使用Let's Encrypt，可以使用使用ACME协议的软件来执行此操作，该协议在你的Web主机上运行。

Certbot是一个部署Let's Encrypt证书的客户端（Let's Encrypt是一个证书发布机构CA，Let's Encrypt支持域名加密，即为域名启用https）。Certbot能够自动的在Web服务器（Apache，Nginx等）上部署从Let's Encrypt获取的证书，非常简单易用.


[Let's Encrypt](https://letsencrypt.org/)

1. 下载 certbot
    [Certbot](https://certbot.eff.org/)的工具让我们可以轻松的获得证书。

### github  

```

git clone https://github.com/certbot/certbot

cd certbot

./certbot-auto --help

```

 解压打开执行就会有相关提示

## 在CentOS7上安装Certbot有三种方式：

 #### 使用Certbot官方提供的对应平台的RPM包安装

 #### 使用Certbot官方的提供的certbot-auto安装
 
 #### 使用pip安装Certbot，因为Certbot是Python程序

 ## 1.1、推荐：使用Certbot官方提供的对应平台的RPM包安装Certbot
 ### 使用Certbot官方提供的对应平台的RPM包安装Certbot非常简单方便，进入[Certbot](https://certbot.eff.org/)官网，在下拉框中选择服务器和操作系统，然后会出现安装代码，如下为CentOS7 Apache nginx对应的代码：

- 1）安装EPEL软件源，Certbot软件包包含在EPEL软件源中

```
sudo yum install epel-release
```
- 2）安装Certbot，同时安装Certbot Apache插件
```
sudo yum install certbot-apache
```
或者安装Certbot Nginx插件
```
sudo yum install certbot-nginx
```
- 3）获取证书，并修改Apache服务器配置
```
sudo certbot --apache
```
获取证书，并修改Nginx服务器配置
```
sudo certbot --nginx
```
此处需要打开对应的端口确保外部能访问
-----
 ## 1.2、使用certbot-auto脚本安装Certbot
certbot-auto脚本会安装Certbot，并且能够自己解决RPM包和Python包依赖问题，同样非常方便。同时certbot-auto是对certbot的封装，即certbot-auto提供certbot的所有功能。在使用此方法安装Certbot后，运行certbot-auto命令获取证书。

- 1）获取certbot-auto脚本
```
wget https://dl.eff.org/certbot-auto
```
- 2）使certbot-auto脚本可执行
```
sudo chmod a+x ./certbot-auto
```
- 3）运行certbot-auto，安装Certbot
```
./certbot-auto
```
- 4）获取Let's Encrypt证书，certbot-auto是对脚本certbot的封装，并且已经更新到了最新版本，所以使用此脚本获取证书
```
./certbot-auto
```
-----
 ## 1.3、使用pip安装Certbot
此种方法比较简单，最好先创建一个Python虚拟环境，然后再安装Certbot

- 1）首先更新pip
```
pip install --upgrade pip
```
- 2）安装Certbot
```
pip install certbot
```
- 3）安装Certbot Apache插件
```
pip install certbot-apache
```
或者安装Certbot Nginx插件：
```
pip install certbot-nginx
```
- 4）在安装Certbot Apache插件时，如提示如下错误：
```
OSError: ctypes.util.find_library() did not manage to locate a library called 'augeas'
```
那是因为缺少augeas库文件，安装augeas库文件：
```
sudo yum install augeas-libs
```
然后就能成功安装Certbot Apache插件。

## 获取Let's Encrypt证书，同时配置Apache服务器
```
sudo certbot --apache
```
或者，同时配置Nginx服务器
```
sudo certbot --nginx
```
 ## ubuntu
```
sudo apt-get install -y software-properties-common
sudo add-apt-repository ppa:certbot/certbot
sudo apt-get update
sudo apt-get install -y python-certbot-nginx
```
Certbot 会询问有关该网站的信息。在执行 `sudo apt-get install -y python-certbot-nginx` 的时候会询问位置信息，我们选择 亚洲（也就是 `6. Asia`），时区选择 `69. Shanghai` 即可。

 #### 绑定nginx
```
sudo certbot --nginx
```
在执行 `sudo certbot --nginx` 的时候会询问你的邮箱，填写和你注册域名时相同的邮箱，其他询问同意即可。

 ### 开启证书自动续约
    我们的证书有效期是 3 个月，不过 certbot 很聪明，有一个自动续约的功能，执行以下命令即可：
```
sudo certbot renew --dry-run
```
