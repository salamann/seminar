# Gitを使ってみよう(その４) - ブランチを使ってみよう

## 今日やること

* フィーチャーブランチを作る
* ブランチのマージ
* GUIツールの簡単な紹介

## ブランチの作成

master ブランチから分岐してブランチを作ってみましょう。

```
$ git checkout master
$ git checkout -b bufix-0123
```

最初に master をチェックアウトしているのは、ブランチの分岐元をはっきりさせるためです。これをしないと、たまたま現在作業中だったブランチから分岐したブランチを作ってしまいます。

bugfix-0123 は作成するブランチの名前です。例として使っているだけなので、ほかの名前でもかまいません。チケット番号0123のバグを直すというようなつもりでつけましたが、新機能の実装用ブランチであれば feature-??? のような名前をつけるといいかもしれません。

ブランチを作ったら、ファイルの編集や追加などして、コミットしてみましょう。

変更したファイルの確認をして、

```
$ git status
```

インデックスに追加してからコミットします。

```
$ git add 編集または追加したファイル名
$ git commit -m "バグ#0123を修正"
```

## ブランチのコミットをマージする

ブランチでの作業(バグ修正や機能実装)が終了したら、成果をマージしましょう。

```
$ git checkout master
$ git pull
$ git merge bugfix-0123
```

マージしたらログを確認をしてみましょう。

```
$ git log --oneline --graph
```

## マージ前に pull する理由

マージの前に、マージ先をチェックアウトして、さらに pull しています。これは、共有リポジトリに他の開発者の行ったコミットが追加されているかもしれないからです。

図で説明します。

```
【git pull 前】
                  master
                  v
リモート A--B--C--D

            master
            v
ローカル A--B
             \
               X--Y
                  ^
                  bugfix-0123
```

git pull で共有リポジトリのmasterブランチの変更を取り込むと、次のような状態になります。

```
【git pull 後】
                  master
                  v
リモート A--B--C--D

                  master
                  v
ローカル A--B--C--D
             \
               X--Y
                  ^
                  bugfix-0123
```

そして git merge します。

```
【git merge 後】
                  master
                  v
リモート A--B--C--D

                     master
                     v
ローカル A--B--C--D--E
             \      /
               X--Y
                  ^
                  bugfix-0123
```

git push して共有リポジトリに自分の変更を反映させます。

```
【git push 後】
                     master
                     v
リモート A--B--C--D--E
             \      /
               X--Y

                     master
                     v
ローカル A--B--C--D--E
             \      /
               X--Y
                  ^
                  bugfix-0123
```

master ブランチを push しただけでは bugfix-0123 というブランチ自体は共有リポジトリには伝わりませんが、ブランチで行ったコミットは伝わります。

Gitでのブランチはコミット(図のY)についた印にすぎないので、共有する必要がなければ共有リポジトリに伝える必要はありません。好き勝手にローカルでブランチを作っても、共有リポジトリにブランチが増える心配はありません。

## GUIツール

### Git GUI

MSYS Git に標準で入っているやつ。
ないよりましです。

### TortoiseGit

TortoiseGit は TortoiseSVN っぽく git を使うためのツール。
コマンドライン版の git の機能とは一対一対応していません。
	ステージング領域という概念は見せない方針のようです。

### Git Extensions

試したバージョンは 2.31。
日本語化されているが、GUIが残念な感じです。
コミットメッセージ入力欄で日本語入力がおかしいです。
(勝手に確定されてしまい使い物になりません。エディタで書いてコピペはできます。)

### GitHub for Windows

かっこいいけどやや重いかもしれません。
細かいことはできないかもしれないけど、シンプルなのでおすすめ。

MSYS Git を含むので、自分で別途インストールした MSYS Git と併用すると混乱することがあります。(後述の改行コード設定の説明を見てください)

## TIPS

### 改行コード設定について

Windows とそれ以外(Unix系, Mac)では慣習的に異なる改行コードが使われています。Windows では *CR LF* ですが、それ以外では *LF* です。

Git では異なるOS間の連携を行うために、コミットやチェックアウトの際に改行コードを自動変換する設定があります。(core.autocrlf)

詳しくは [Pro Git](http://git-scm.com/book/ja/Git-%E3%81%AE%E3%82%AB%E3%82%B9%E3%82%BF%E3%83%9E%E3%82%A4%E3%82%BA-Git-%E3%81%AE%E8%A8%AD%E5%AE%9A) を見てほしいのですが、この core.autocrlf に設定可能な値が３種類あります。

* *false* 改行コード変換しない(勉強会の第一回の設定)
* *true*  改行コード変換する(デフォルト)
* *input* コミット時のみ変換する

同じリポジトリに対して、異なる改行コード変換設定でコミットすると、１行だけしか変更していないテキストファイルでも、全体を変更したことになってしまいます。

GitHub for Windows と 生の MSYS Git を併用する場合には改行コード変換設定を合わせましょう。

```
$ git config --global core.autocrlf false
```

### 三種類の設定

設定は三種類あり、下のほうの設定のほうが優先です。

1. システム設定(C:/Program Files (x86)/Git/etc/gitconfig)
2. ユーザー設定(Win7 では C:/Users/ユーザー名/.gitconfig  WinXP では C:/Documents and Settings/ユーザー名/.gitconfig)
3. リポジトリ設定(.git/config)

それぞれ次のように設定可能です。

```
$ git config --system core.autocrlf true
$ git config --global core.autocrlf true
$ git config core.autocrlf true
```
