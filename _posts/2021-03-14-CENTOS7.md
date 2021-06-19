---
layout: post
title: CENTOS7 apache/php配置
categories: centOS7 apache php
tags: php apache centos7
---

* content
{:toc}


# centOS7常用命令

###### 将用户切换到root管理员

```
su root
```



# Apache

###### install

```Linux
yum -y install httpd
```

###### turn on service 

```Linux
systemctl start httpd.service
```

###### set apache service to start at boot

```Linux
systemctl enable httpd.service
```

###### 验证apache服务是否安装成功

在本机浏览器中输入虚拟机的ip地址，CentOS7查看ip地址的方式为：

```
ip addr
```

这里是访问不成功的。

查了资料，说法是，CentOS7用的是Firewall-cmd，CentOS7之前用的是iptables防火墙；要想让外网能访问到apache主目录，就需要做以下的操作：

```
firewall-cmd --permanent --zone=public --add-service=http
firewall-cmd --permanent --zone=public --add-service=https
firewall-cmd --reload
```

然后再访问外网ip，如果看到apache默认的页面--有Testing 123...字样，便是成功安装了apache服务了。

![image-20210314175658198](https://i.loli.net/2021/03/14/BNcDW5xIzk6Qahv.png)

# php

###### install

```
yum -y install php
// phpバージョン
php --version
```

###### restart apache

```
systemctl restart httpd.service
```

###### test

可以写一个php文件在浏览器中运行

eg.

```
// info.phpファイル生成または開く
vi /var/www/html/info.php
// エディタモードに変更
i
// 内容を入力
<?php phpinfo(); ?>
// エディタモード退出
Esc
// 変更を保存
:wq
```

然后，在自己电脑浏览器输入       虚拟机IP地址/info.php
运行，会出现php的一些信息

![](https://i.loli.net/2021/03/14/sWyhPcXnK73v1u8.png)

###### install モジュール

```
// pdo
yum install php-pdo
// php-xml
yum install php-xml

// mb_string
yum -y install php-mbstring

// posix_isatty() 
yum -y install php-process


```



# MySQL

**MariaDB**

###### install

```
yum -y install mariadb mariadb-service
```

![image-20210314183603699](https://i.loli.net/2021/03/14/a1AWF9Ph7fYkrUK.png)

###### start Mysql

```
systemctl start mariadb.service
```

###### start Mysql at boot

```
systemctl enable mariadb.service
```

###### mysql のrootアカウントとパスワード設定

```
mysql_secure_installation
```

然后会出现一串东西，可以仔细读一下，如果你懒得读，就在提示出来的时候，按Enter就好了，让你设置密码的时候，你就输入你想要的密码就行，然后继续在让你选择y/n是，Enter就好了；当一切结束的时候，你可以输入`mysql -uroot -p`的方式，验证一下。

![image-20210314190627192](https://i.loli.net/2021/03/14/3T65MsP4lRzEo2h.png)