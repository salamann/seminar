# ローカルでsvnライクに使ってみよう

## インストール

インストールの選択肢

* MSYS Git のみ
* GitExtensions
* MSYS Git + TortoiseGit

## ローカルリポジトリを作る

$ mkdir git-renshu         # 作業用ディレクトリの作成
$ cd git-renshu
$ git init                 # リポジトリの作成

.git というディレクトリができているはず。

## まずは初期設定

* メールアドレスと名前の設定
* エディタの設定?

## ファイルを追加してみる

hello.cpp を作る。

> $ git add hello.cpp        # ファイルを管理対象として追加
> $ git status               # 確認

## コミットしてみる

> $ git commit -m "コミットメッセージ"     # コミット
> $ git status                             # 確認
> $ git log                                # 確認
