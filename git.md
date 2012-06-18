## 流れ

* ローカルで使ってみる
    * インストール
    * ローカルリポジトリの作成
    * ファイルの追加やコミット
* 共同作業してみる
    * bitbucket or github を使ってみる
    * clone
    * pull
    * push
* ローカルブランチしてみる
    * branch
    * rebase

## svnと違うところ
* ローカルリポジトリ
    * ローカルでコミットできる
    * 全部ローカルにあるので巨大なリソースは扱いにくい
* ステージング領域
* 連続するリビジョン番号はない
* ブランチの概念
* 基本的に push する前に pull しないとダメ

## 調べないといけないこと

* インストール
    * MSYS Git
* ブランチ/マージ/コンフリクト を試してみる
* GUI
    * TortoiseGit
    * MSYS GitのGUI
    * Git Extensions
    * GitHub for Windows
* 使いやすいGUI diff/マージツール

## Gitの設定

### 名前とe-mailの設定

    git config --global user.name "John Doe"
    git config --global user.email "john.doe@example.com"   

### GUIの文字コード設定

    git config --global gui.encoding utf-8

## GUIツール

### Git GUI

MSYS Git に標準で入っているやつ。
ないよりまし。

### TortoiseGit

TortoiseGit は TortoiseSVN っぽく git を使うためのツール。
コマンドライン版の git の機能とは一対一対応していない。
ステージング領域という概念は見せないようだ。

### Git Extensions

試したバージョンは 2.31。
日本語化されているが、残念なGUIだった。
コミットメッセージ入力欄で日本語入力がおかしかった。
(勝手に確定されてしまい使い物にならない。エディタで書いてコピペならいける。)

### GitHub for Windows

かっこいいけどやや重い。

MSYS Git 直たたきしたときと GitHub for Windows を使ったときで動作が違うので、push するときにコンフリクトすることがあった(と思う)。
GitHub for Windows では autocrlf = true になっているのに、自分でMSYS Git をインストールしたときに autocrlf = false としていたのが原因かな？

##

### 自分がひっかかったところ

* コマンドの機能が多すぎてフラグ一つで動作が大きく変わる
* ブランチはポインタに過ぎないことがわからないかった
* リモートブランチとかリモート追跡ブランチ
* リモート追跡ブランチの設定方法や確認方法
    * git branch -vv
    * git branch --set-upstream BRANCHNANE origin/BRANCHNAME
* ステージングを取り消す方法
    * ステージング取り消しとコミットの取り消しが同じコマンドなのは怖い

### svn でよく使う機能との対比

* よく使うもの
    * チェックアウト            (clone)
    * 追加 -> コミット          (add -> commit [-> push])
    * 修正 -> コミット          (add -> commit [-> push])
    * 元に戻す
        * 全体                  (git reset --hard)
        * 特定のファイル        (git reset -- FILE; git checkout -- FILE)
    * 更新                      (git pull)
    * 削除                      (git rm FILE)
    * ログ                      (git log [--oneline])
    * 比較
        * work <->index         (git diff -- PATH)
        * index<->HEAD          (git diff --cahced -- PATH)
    * 特定のリビジョンとの比較  (git diff COMMIT -- PATH)
    * 変更のチェック            (git status)
* 頻度が低いもの
    * 特定のリビジョンのファイルに戻す  (git checkout COMMIT -- PATH)
    * 無視設定                  (.gitgnore を編集)
    * ブランチ作成              (git branch NEWBRANCH [COMMIT or BRANCH])
    * タグ                      (git tag TAG [COMMIT]
    * trunk -> branch マージ    (git checkout BRANCH; git merge TRUNK)
    * branch -> trunk マージ    (git checkout TRUNK; git merge BRANCH)
    * リネーム                  (git mv OLDNAME NEWNAME; git commit -am "MESSAGE")

## Subversion では面倒なこと

* ブランチ独自の変更とマスターの取り込みの両立
    * ブランチでのみライブラリバイナリをコミットする
    * ブランチのみ特殊なワークアラウンドをするがマスターの変更も取り込む

## 他のツールとの連携

### コメント編集用エディタとして xyzzy を使う

* 起動中のxyzzyで開きたい
* バッファを削除したら編集終了にしたい
* UTF-8で日本語コメントを書きたい

といった要求があったので、以下のようにしました。

* .xyzzy でUTF-8Nで開きなおす関数を定義しておく

```
(defun revert-buffer-utf8n ()
  (interactive)
  (revert-buffer *encoding-utf8n*))
```

* xyzzycli.exe を xyzzycli-utf8n.exe という名前でコピーする
* xyzzycli-utf8n.ini という名前で次の内容のファイルを作る

```
[xyzzy]
followingOptions=-f revert-buffer-utf8n
```

* .gitconfig に以下の内容を追加

```
[core]
    editor = start //wait c:/xyzzy/xyzzycli-utf8n -wait
```

### WinMerge を difftool として使用する

.gitconfig に以下のように記述する。

```
[diff]
    guitool = winmerge
    tool = winmerge
[difftool "winmerge"]
    cmd  = 'C:/Program Files/WinMerge/WinMergeU.exe' -e -ub -dl "Base" -dr "Mine" "$LOCAL" "$REMOTE"
[difftool]
    prompt =false
```

## 参考文献

* [Pro Git](http://git-scm.com/book/ja)
* [Git Cheat Sheets JP](http://hail2u.net/documents/git-cheat-sheets-jp.html)
