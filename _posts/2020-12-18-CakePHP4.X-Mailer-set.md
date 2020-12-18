---
layout: post
title: CakePHP4.X　Mailer－－メール送信
categories: cakephp4
tags: cakephp4 mailer php set　
---

* content
{:toc}


###### 必須な事前準備



１．クラスロード

```php
use Cake\Mailer\Mailer;
```



２．Emailtransportsの設定

【app.php】ファイルにて、プロファイルのテンプレートを追加。

![image-20201218133930025](https://i.loli.net/2020/12/18/v8OBqai2kfAClpR.png)

defaultプロファイルの設定。

![image-20201218134202096](https://i.loli.net/2020/12/18/1iNZrREmnszwu6Y.png)



３．googleアカウントの許可設定

[https://www.google.com/settings/security/lesssecureapps](https://www.google.com/settings/security/lesssecureapps)

![image-20201218135504563](https://i.loli.net/2020/12/18/XSq1JiVQvPd46cD.png)

<hr>

###### 送信すること

インスタンス作成とプロファイルの設定

```PHP
$mailer = new Mailer('default');
```

メール情報設定

```php
$mailer
    ->setFrom(['送信メール@gmail.com' =>'名称'])
    ->setTo('受信メール@gmail.com')
    ->setSubject('メールタイトル')
    // 送信する
    ->deliver('ここは内容');
```

