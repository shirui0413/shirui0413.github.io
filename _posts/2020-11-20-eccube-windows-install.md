---
layout: post
title: "CECUBE開発者向けインストール ーーwindows版"
date: 2020-11-20 18:56:43
categories: eccube4X
tags: eccube windows
---

* content
{:toc}
[ec-cube公式サイト](https://doc4.ec-cube.net/)



##### <u>1．システム要件</u>

<img src="https://i.loli.net/2020/11/18/mYIwMtWGf4Q1lvJ.png" alt="image-20201118104711502" style="zoom:50%;" />

<img src="https://i.loli.net/2020/11/18/qJBHva9nbxDg81h.png" alt="image-20201118104929275" style="zoom:50%;" />

##### 		<u>有効になっているphpモジュールの確認</u>

```
php -m
```

<img src="https://i.loli.net/2020/11/18/42fVcTNS3MZtwHy.png" alt="image-20201118105359121" style="zoom: 50%;" />

　　足りないことと自分でネットからインストール方法を調べて、自分も**fileinfo**というライブラリがないで、調べて**php.ini**の**extension=fileinfo**を有効にすると解決しました。



##### <u>２．コマンドラインでインストール</u>

- ###### EC-CUBEをインストールしたいディレクトリへ移動

  ```
  cd ディレクトリ
  ```

  例：<img src="https://i.loli.net/2020/11/18/7vVCQd2A4nf6lse.png" alt="image-20201118111538724" style="zoom:50%;" />

- ###### ディレクトリに移動した後、composer.pharファイルを生成する

  [ここをクリックして、composer.pharのダウンロードを進めます](https://getcomposer.org/download/)

  

  <img src="https://i.loli.net/2020/11/18/7KqRkOVZMXvfmwy.png" alt="image-20201118111728270" style="zoom: 67%;" />

  composer.phar ファイルをEC-CUBEをインストールしたいディレクトリに保存。

  <img src="https://i.loli.net/2020/11/18/jzwmSq3HYBM8PUo.png" alt="image-20201118112223392" style="zoom: 50%;" />

- ###### composer.pharのバージョンをEC-CUBEの4.0の対応しているバージョン(1.x)に変更する

```
php composer.phar selfupdate --1
```

例：<img src="https://i.loli.net/2020/11/18/CZVEvBujQFSopKs.png" alt="image-20201118112551699" style="zoom:50%;" />

- ###### 開発者向けec-cube4をインストール

```
php composer.phar create-project ec-cube/ec-cube ec-cube "4.0.x-dev" --keep-vcs
```

例：![image-20201118144331557](https://i.loli.net/2020/11/18/IwOLACVFhvU7Ryk.png)

DB作成こと、まず置いといて、後でDBの作成とスキーマ導入の作業が一緒に進めましょう。

- ###### ec-cubeディレクトリが生成されて、ec-cubeに移動し、ビルトインヴェブサーバの起動する

  ```
  php bin/console server:run --env=dev
  ```

  例：<img src="https://i.loli.net/2020/11/18/HaS6tW5mLVnvqAP.png" alt="image-20201118181801196" style="zoom:50%;" />

  こちの環境にて、今127.0.0.1:8000のサーバーが立っているので、今度8001のポートを作成されました。

  チュートリアルにて、ここでは、127.0.0.1:8001/adminにアクセスすれば、管理者のログイン画面が表示されることですが、実際は下記画面のエラーが発生しました。

  ここを調べて、.envファイルの設定が必要となります。

  <img src="https://i.loli.net/2020/11/18/8uBb9OzfK7RoHgV.png" alt="image-20201118182051532" style="zoom:50%;" />

- ###### .envファイルの設定

作成されたec-cubeフォルダ中には.envというファイルがあります。

ファイルを開いて、開発モードで、APP_ENV=dev と　APP_DEBUG=1の設定が必要となるを書いております。

![](https://i.loli.net/2020/11/18/uD1RVqWa2AOcTJM.png)ここで変更します。

![](https://i.loli.net/2020/11/18/4RxPQaYuD9rlXof.png)

127.0.0.1/8001/adminにアクセスして、今度はこんなエラーが表示された。

![image-20201118183852219](https://i.loli.net/2020/11/18/KFnsymzUR6waXNY.png)

これはデータベースを設定することやっていない原因です。

- ###### DB設定

  .envファイルに`DATABASE_URL=mysql://dbuser:secret@mysql/eccubedb` としておきます

  ![image-20201118190853725](https://i.loli.net/2020/11/18/m2On9Ijk5wzQK7A.png)

- ###### DBスキーマ導入

先ず、ctrl+C でビルトインヴェブサーバを停止する。

![image-20201118191455496](https://i.loli.net/2020/11/18/BMKc2Rqvwgy8Jlu.png)

```
# データベース削除
php bin/console doctrine:database:drop --force
```

例：![image-20201118191826668](https://i.loli.net/2020/11/18/wvqU3TzD95hi28Q.png)先ほど、プロジェクトを生成する時、このdatabase の作成すること失敗しましたが、今度の削除もできましたのを気がする為、も一度試して、も削除することできました。先ほどこのdatabaseの実際の生成することがありません、ここ多分念のためそのdatabaseが存在いないの確認だけで。

```
＃ データベース作成
php bin/console doctrine:database:create
```

例：![image-20201118192555892](https://i.loli.net/2020/11/18/qbA9ZNhS8FfDIGt.png)

```
＃ スキーマの削除
php bin/console doctrine:schema:drop --force
```

例：![image-20201118192753211](https://i.loli.net/2020/11/18/wO8rqTkSDiRQXPM.png)

```
# スキーマ生成
php bin/console doctrine:schema:create
```

![image-20201118193823403](https://i.loli.net/2020/11/18/eQMjFZEkAU5DvLx.png)

```
# 初期データ生成
php bin/console eccube:fixtures:load
```

![image-20201118193940960](https://i.loli.net/2020/11/18/hPOKB69wca48QJq.png)

それでは、設定完了しました。

##### <u>３．登録</u>

ビルトインヴェブサーバを起動して、127.0.0.1:8001/adminにアクセスして、管理者のログイン画面が表示されました。

ユーザー名：　admin

パスワード： 　password

![image-20201118194207772](https://i.loli.net/2020/11/18/sgFBLC4mTl7zpdW.png)

![image-20201118194439528](https://i.loli.net/2020/11/18/vfs7QF4cSAPrRg5.png)

