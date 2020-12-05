---
layout: post
title: "Git及びTortoiseGitとGitHubの接続"
categories: git
tags: git github tortoisegit
---

{:toc}

### ・Git

初めてGitを使う場合はusernameとemailの配置。

<span style='color:red'> 念のため、GitHubのユーザー名とメールをGitに設定。</span>

git bash を起動。

```git bash
// ユーザー名設定
git config --global user.name "sekiz"
// メール設定
git config --global user.email "shirui0413@gmail.com"
```



設定したユーザー名とメールを忘れた場合、下記命令で

```git bash
git config --global --list
```



##### ・Gitのよく使うコマンド

```git bash
// ローカルリポジトリ作成
git init
// リポジトリにファイル追加
git add ファイル名
// コミット
git commit -m "コミット内容説明"
// リモート追加 
git remote add origin リポジトリのURL
// リモートにプッシュ
git push origin master
```



##### ・リモート設定（github）

→リモート設定

```git bash
git remote add origin https://github.com/shirui0413/sc_learning.git
```

→リモートにpush

```
git push origin master
```

pushを実行すると、GitHubのログインダイアログを表示されて、emailとpasswordを入力して、プッシュを続ける。

<img src="https://i.loli.net/2020/12/04/GBX7TCd3ZiygW54.png" alt="image-20201204112842841" style="zoom:50%;" />



##### ・GitHubでSSH接続

SSH Keyが存在するかチェック

```git bash
// .sshフォルダに移動
cd ~/.ssh
// ファイル表示
ls
```

![image-20201203234153770](https://i.loli.net/2020/12/03/G8UOqNey1FSEZok.png)

<span style="color:red"> id_rsa</span> と<span style="color:red"> id_rsa.pub</span>が存在すれば、SSH Keyが存在しています。

###### ・SSH Key生成

```git bash
ssh-keygen -t rsa -C "メールアドレス"
```

![image-20201204114108197](https://i.loli.net/2020/12/04/mMuSDELqUzxWGRc.png)

これで、公開キー(id_rsa.pub)と秘密キー(id_rsa)を生成されました。

###### ・公開キーをGitHubにセット

GitHubを登録して、右上の個人画像をクリックして、「setting」を選択。

<img src="https://i.loli.net/2020/12/04/toAB1wUucEmqipV.png" alt="image-20201204114937565" style="zoom:50%;" />

左側ナビメニューの「SSH and GPG keys」を選択

<img src="https://i.loli.net/2020/12/04/iHN5CtdOcPmhnVX.png" alt="image-20201204115054723" style="zoom:50%;" />

「New SSH key」ボタンをクリックして、

![image-20201204115146084](https://i.loli.net/2020/12/04/dwT1SL39Fi6PxN2.png)

![image-20201204120333018](https://i.loli.net/2020/12/04/us7BrCHEzRFOW6f.png)

###### ・成功で設定するかの検証

```git bash
ssh -T git@github.com
```

![image-20201204120747758](https://i.loli.net/2020/12/04/h7sXrBtk4iZqWQw.png)



###### ・SSHリモート設定

sshアドレス取得。

<img src="https://i.loli.net/2020/12/04/yuw8C4t9mIWUcGp.png" alt="image-20201204120937831" style="zoom:50%;" />

リモートに追加

```
git remote add origin_ssh git@github.com:shirui0413/sc_learning.git
```

設定したリモート表示

```
git remote -v
```

![image-20201204121936256](https://i.loli.net/2020/12/04/QW3tJVjxcsohXgT.png)

設定した後、pushの場合、ユーザー名とパスワードの入力は不要になる。



### ・GitのGUIツールTortoiseGitの設定

TortoiseGitはPageantというツールを用いて認証キーを管理することです。

Pageantにキーを認証させるものをGitHubに設定必要です。

##### ・PPK作成

TortoiseGitのPuttygenを起動し、[Generate]でキーを生成する。生成しているところにて、マウスの動くことが必要。

<img src="https://i.loli.net/2020/12/04/9ML3NxO7snKeGPq.png" alt="image-20201204123132292" style="zoom:33%;" /><img src="https://i.loli.net/2020/12/04/EWkHAU94LPjytfN.png" alt="image-20201204123213915" style="zoom: 50%;" />

<img src="https://i.loli.net/2020/12/04/VcyjU3u8QdZGthq.png" alt="image-20201204123712417" style="zoom:67%;" />



**公開キーをGitHubに設定。**

![image-20201204124131470](https://i.loli.net/2020/12/04/BTfh8gMeDXaHu7F.png)

**秘密キーをTortoiseGitに設定。**

![image-20201204124008485](https://i.loli.net/2020/12/04/jeYHFt6aJ7opQOS.png)

###### プッシュ

![image-20201204131005909](https://i.loli.net/2020/12/04/loJtIzEv8LSiqfO.png)

![image-20201204131945908](https://i.loli.net/2020/12/04/JB9vKrFpmZPCTGR.png)

