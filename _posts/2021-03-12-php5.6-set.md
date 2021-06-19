---
layout: post
title: PHP5.6 iniファイル配置
categories: php
tags: php ini 　
---

* content
{:toc}


# php5.6 的 php.ini 开发期间常用配置

;显示除了提示外所有的错误
error_reporting = E_ALL & ~E_NOTICE

;设定拓展目录
extension_dir = "ext"

常用解锁拓展库
extension=php_bz2.dll
extension=php_curl.dll

extension=php_gd2.dll
extension=php_gettext.dll

extension=php_mbstring.dll

extension=php_mysql.dll
extension=php_mysqli.dll

extension=php_openssl.dll

extension=php_pdo_odbc.dll

extension=php_pdo_sqlite.dll

extension=php_soap.dll
extension=php_sockets.dll
extension=php_sqlite3.dll

extension=php_xmlrpc.dll
extension=php_xsl.dll

;设定中国时区
date.timezone = Asia/Tokyo

;设定加密密钥文件路径，下载地址：http://curl.haxx.se/ca/cacert.pem
openssl.cafile=D:/code/php/cacert.pem

;这个没懂是干嘛的，不过装 Drupal8 提示要开启
always_populate_raw_post_data = -1

;最大执行时间设置为0(无时间限制)，可以在php程序里这样设置 ini_set("max_execution_time", 0);
max_execution_time = 0