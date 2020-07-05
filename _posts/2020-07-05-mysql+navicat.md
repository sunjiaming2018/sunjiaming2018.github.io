---
layout: post
title: "ubuntu18.04安装Mysql+navicat"
date: 2020-07-05
description: "ubuntu18.04,Mysql,navicat"
tag: 工具
---

### 安装Mysql

最近需要学习Mysql,下面记录在ubuntu18.04环境安装Mysql的过程。

### 1.下载安装包

[官网](https://dev.mysql.com/downloads/mysql/)

* 选择ubuntu18.04,64位；
* 下载地址，选择下图企鹅左边的DownloadsNow。

<img src="/images/post/2020-07-05-mysql+navicat/MySQL下载.png">

### 2.安装

* 输入命令
```
sudo dpkg -i mysql-apt-config_0.8.20-1_all.deb
sudo apt update
sudo apt install mysql-server
```
* 输入root密码

<img src="/images/post/2020-07-05-mysql+navicat/root密码.png">

* 选择默认加密

### 3.测试
输入命令
```
mysql -u root -p

```
如下图示，则安装成功。
<img src="/images/post/2020-07-05-mysql+navicat/MySQL-text.png">


### 安装navicat

#### 1.相关工具
* navicat15-premium-cs.AppImage：Navicat 15 premium 官方简体中文试用版
* navicat-patcher：补丁
* navicat-keygen ：注册机
* appimagetool-x86_64.AppImage：Linux 独立运行软件打包工具

[百度网盘下载地址](https://pan.baidu.com/s/12zSYWC_CgaNZVxESTdg8zA)
提取码：9rqw

#### 2.环境配置
##### 安装 capstone
```
sudo apt-get install libcapstone-dev
```
##### 安装 keystone
```
sudo apt-get install cmake
git clone https://github.com/keystone-engine/keystone.git
cd keystone
mkdir build
cd build
../make-share.sh
sudo make install
sudo ldconfig
```
##### 安装 rapidjson
```
sudo apt-get install rapidjson-dev
```
#### 3.操作步骤
##### 1.赋予执行权限
```
chmod +x appimagetool-x86_64.AppImage
chmod +x navicat-patcher
chmod +x navicat-keygen
```
##### 2.解压官方包
```
mkdir navicat15
mount -o loop navicat15-premium-cs.AppImage navicat15
cp -r navicat15 navicat15-patched
```
##### 3.运行补丁
```
mkdir navicat15
mount -o loop navicat15-premium-cs.AppImage navicat15
cp -r navicat15 navicat15-patched
```
##### 4.打包成独立运行软件
```
./appimagetool-x86_64.Appimage navicat15-pathed navicat15-premium-cs-pathed.AppImage
```
##### 5.运行补丁后软件包
```
chmod +x navicat15-premium-cs-pathed.AppImage
./navicat15-premium-cs-pathed.AppImage
```
##### 6.运行注册机
```
navicat-keygen --text ./RegPrivateKey.pem
```
* 选择产品类型： 1 Premium
* 选择语言： 1 Simplified Chinese
* 选择版本： 15
* 生成序列号： 填写至软件注册页面，并在断网后选择手工激活
```
[*] Serial number:
NAVC-PJWW-BKN4-C4YW
```
* 填写个人信息：
```
[*] Your name: sunjiaming
[*] Your organization: suda
```
* 输入注册码： 复制软件激活页面注册码并粘贴此处
```
[*] Input request code in Base64: (Double press ENTER to end)
nqKkI0BtJR5Nq***==
```
* 生成激活码： 复制Activation Code内容粘贴至软件激活页面

### 使用 navicat15 连接 MySQL

* 1.终端启动MySQL
```
sudo mysql -u root -p
xxxxxx /*输入密码*/
```
* 2.打开 navicat15
```
cd /home/sun/Navicat15
./navicat15-premium-cs-pathed.AppImage
```
* 3.连接配置
```
新建连接
连接名：mydb（随意命名）
主机改为:127.0.0.1
端口：3306
用户名：root
密码：123123（mysql用户密码）
测试连接即可
```

<img src="/images/post/2020-07-05-mysql+navicat/navicat连接mysql.png">
