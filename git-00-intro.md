# gitを使ってみよう(その１)

## gitの特徴

我々が今使っている Subversion に比べると git にはこんな特徴があります。

* ローカルにもリポジトリがある(いろんなところにリポジトリがある)
* ブランチが気軽に使える(自分だけの作業用ブランチとか)
* 柔軟なコミット(コミットのやり直しとか)
* github や bitbucket などのホスティングサービスが充実

今日は、ローカルリポジトリの話のみです。
後はまた今度。

## インストール

### 何をインストールする？

* [MSYS Git](http://code.google.com/p/msysgit/downloads/list?q=full+installer+official+git) のみ ← 今回はこれ！
* GitExtensions
* MSYS Git + TortoiseGit
* GitHub for Windows

Git-1.7.10-preview20120409.exe を使いましょう。

### MSYS Git インストール時の選択肢

何が正解とかないけど、今回はこうしてみましょう。

* インストールするコンポーネントはデフォルト
* コマンドプロンプトでも使えるようにする (Run Git from Windows Command Prompt)
* SSH は使わないのでデフォルトでいい(Use OpenSSH)
* 改行コードは as is で (Checkout as-is, commit as-is)

## まずは初期設定

### メールアドレスと名前の設定

コマンドプロンプトから次のように入力。

    $ git config --global user.name "Nobita Nobi"
    $ git config --global user.email "nobita.nobi@example.com"

Windows7 の場合 c:/Users/*USERNAME*/.gitconfig に上の情報が格納されます。
WindowsXP の場合 C:/Documents and Settings/*USERNAME*/.gitconfig です。

    [user]
        name = Nobita Nobi
        email = nobita.nobi@example.com

直接 .gitconfig を編集してもかまいません。

## 使ってみる
### ローカルリポジトリを作る

    $ mkdir git-renshu         # 練習用ディレクトリの作成
    $ cd git-renshu
    $ git init                 # リポジトリの作成
    Initialized empty Git repository in C:/home/work/git-renshu/.git/

.git というディレクトリができているはずです。このディレクトリの中にローカルリポジトリが格納されています。

Subversion の .svn は作業ベースのリビジョンの情報しか保持していませんが、 .git はリポジトリの全情報を持っています。

### ファイルを追加してみる

エディタで hello.cpp を作り、gitの管理対象にしてみましょう。

    $ git add hello.cpp        # ファイルを管理対象として追加
    
    $ git status               # 確認
    # On branch master
    #
    # Initial commit
    #
    # Changes to be committed:
    #   (use "git rm --cached <file>..." to unstage)
    #
    #       new file:   hello.cpp
    #


"Changes to be commited" は 「コミット候補はこのファイルですよ」 という意味です。

### コミットしてみる

途中 warning がいろいろ出るかもしれないですが気にしないでください。

    $ git commit -m "hello.cpp を追加    # コミット
    [master (root-commit) 68088b6] hello.cpp を追加
     1 file changed, 7 insertions(+)
     create mode 100644 hello.cpp
    
    Warning: Your console font probably doesn't support Unicode. If you experience s
    trange characters in the output, consider switching to a TrueType font such as L
    ucida Console!
    
    $ git status                         # 確認
    # On branch master
    nothing to commit (working directory clean)
    
    $ git log                            # ログ確認
    WARNING: terminal is not fully functional
    commit 68088b64d475c39f5cec034b2b050440d284796b
    Author: Nobita Nobi <nobita.nobi@example.com>
    Date:   Tue Jun 12 10:40:15 2012 +0900
    
        hello.cpp を追加

68088b64d475c39f5cec034b2b050440d284796b は Subversion でいうリビジョン番号のようなものです。(また後で説明します。)

### また編集してコミットしてみる

hello.cpp を編集してから次のようにしてみましょう。

    $ git status                        # 現状確認
    # On branch master
    # Changes not staged for commit:
    #   (use "git add <file>..." to update what will be committed)
    #   (use "git checkout -- <file>..." to discard changes in working directory)
    #
    #       modified:   hello.cpp
    #
    no changes added to commit (use "git add" and/or "git commit -a")

"Changes not staged for commit" というメッセージが出てます。(詳しい意味は後で)
注意すべきなのは、 git の場合 subversion と違い、編集したファイルがだけだとコミット対象にならない、ということです。再び git add するとコミット対象となります。

    $ git add hello.cpp                 # コミット対象を指定
    
    $ git commit -m "hello.cpp の修正"  # コミット実行
    [master b7e8628] hello.cpp の修正
     1 file changed, 1 insertion(+), 1 deletion(-)
    
    Warning: Your console font probably doesn't support Unicode. If you experience s
    trange characters in the output, consider switching to a TrueType font such as L
    ucida Console!

## 解説

### インデックス(ステージング領域)

Subversion と違い、コミット前にインデックスと呼ばれる領域にファイルをコピーする必要があります。

    working tree      (作業領域)
     ↓
     ↓ git add
     ↓
    index             (コミット準備領域)
     ↓
     ↓ git commit
     ↓
    local repository  (自分専用リポジトリ)
     ↓
     ↓ git push  (これはまた今度説明する)
     ↓
    remote repository (共有リポジトリ)

インデックスに追加することを「ステージング」「ステージする」などとも言います。
インデックスのある理由は多分こういうことだと思います。

* コミット対象を吟味するため(GUIツールだと旨みが少ないかも)
* 部分的なステージングができる(git add -p)

例えば、バグ修正と新規機能追加を一緒にしてしまったけど、分けてコミットしたいときなどに便利です。

### リビジョン

Git では Subversion のようにわかりやすいリビジョン番号はつきません。68088b64d475c39f5cec034b2b050440d284796b のようなSHA-1ハッシュ値(コミット内容から計算されたユニークな数値)でリビジョンを表します。

なぜこんなわかりにくい番号になっているかというと Git が「分散」バージョン管理システムであるためです。

リビジョンを指定した操作をするときは、このハッシュ値を全部入力しなくても大丈夫です。先頭4桁くらい書けば識別してくれます。

## TIPS

### シンプルに状態表示

git status に -s オプションをつけるとシンプルな表示になります。
左端の文字がインデックスの状態。２文字目がワーキングツリーの状態。

```
$ git status -s
 M hello.cpp
M  good-morning.cpp
?? good-bye.cpp
```

### 比較

作業ツリー(working tree)で変更されている部分を知りたい場合。

    $ git diff

特定のファイルのみの変更点を知りたい場合。

    $ git diff hello.cpp

インデックスとリポジトリの差分を見たい場合。

    $ git diff --cached

### git diff や git log が一画面に収まらないとき

キー操作でスクロールすることができます。(unix系OSでよく使われる less というコマンドが裏で動いています)

* f 下にスクロール(forward)
* b 上にスクロール(backward)
* q 終了(quit)
* h ヘルプ(help)

日本語部分が行の後ろのほうで文字化けすることがありますが、使えなくはないです。

### 追跡中(リポジトリに登録済み)のファイルを全て add する

    $ git add -u

### 勝手にステージしてコミット

git commit に -a オプションを足すと、 git add の手間が省ける。

    $ git commit -am "コミットメッセージ"

### ファイルの編集を取り消す

インデックスからワーキングツリーにコピーすればよいです。

    $ git checkout -- hello.cpp   # -- はオプションとファイル名を分けるセパレータ(あいまいでないなら省略可能)

```
working tree      (作業領域)
 ↑
 ↑ git checkout
 ↑
index             (コミット準備領域)
```

checkout はブランチの切り替えにも使いますが、それはまた今度。

### git add しちゃったけど取り消したい場合

git reset でインデックスをリポジトリの最新版の状態に戻すことができます。

```
$ git reset hello.cpp      # hello.cpp のステージングを取り消し
$ git reset                # インデックスを全て元に戻す
```

```
index             (コミット準備領域)
 ↑
 ↑ git reset
 ↑
local repository  (自分専用リポジトリ)
```

### 無視するファイルを指定する

.gitignore というファイルに無視するファイル名のパターンを書きます。
"#" で始まるとコメント行になります。

    # エディタのバックアップファイルは無視
    *~
    *.*~
    *.bak

.gitignore 自体もリポジトリに入れておけます。

### ヘルプ

英語だけどヘルプが見られます。

```
$ git help コマンド名
```

日本語のドキュメントとしては [Pro Git](http://git-scm.com/book/ja) がお勧めです。
