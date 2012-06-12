# gitを使ってみよう(とりあえずローカルで)

## インストール

インストールの選択肢

* MSYS Git のみ <= 今回はこれで！
* GitExtensions
* MSYS Git + TortoiseGit
* GitHub for Windows

### MSYS Git インストール時の選択肢

何が正解とかないけど、今回はこうしてみよう。

* インストールするコンポーネントはデフォルト
* コマンドプロンプトでも使えるようにする (Run Git from Windows Command Prompt)
* SSH は使わないのでデフォルトでいい(Use OpenSSH)
* 改行コードは as is で (Checkout as-is, commit as-is)

## まずは初期設定

### メールアドレスと名前の設定

コマンドプロンプトから次のように入力。

```
> git config --global user.name "Nobita Nobi"
> git config --global user.email "nobita.nobi@example.com"
```

Windows7 の場合 c:/Users/Windowsのユーザー名/.gitconfig に上の情報が格納されます。

```
[user]
    name = Nobita Nobi
    email = nobita.nobi@example.com
```

直接 .gitconfig を編集してもかまいません。

## ローカルリポジトリを作る

```
> mkdir git-renshu         # 練習用ディレクトリの作成
> cd git-renshu
> git init                 # リポジトリの作成
```

.git というディレクトリができているはず。このディレクトリの中にローカルリポジトリが格納されている。

## ファイルを追加してみる

エディタで hello.cpp を作り、gitの管理対象にしてみよう。

```
> git add hello.cpp        # ファイルを管理対象として追加
> git status               # 確認
# On branch master 
# Changes to be commited:
#   (use "git reset HEAD <file>..." to unstage)
#
#       modified:   hello.cpp
```

"Changes to be commited" は 「次にコミットされるのはこのファイルですよ」 という意味

## コミットしてみる

```
> git commit -m "hello.cpp を追加    # コミット
> git status                         # 確認
> git log                            # ログ確認
commit 286148bf2fe4d046bebf56fece6aa1917c70a1b4
Author: Nobita Nobi <nobita.nobi@example.com>
Date:   Mon Jun 11 09:06:41 2012 +0900

    hello.cpp を追加
```

## また編集してコミットしてみる

#
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#       modified:   git-00-intro.md
#