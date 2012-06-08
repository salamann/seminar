## gitセミナーでやってみたいこと

* gitをローカルリポジトリで使ってみる
    * リポジトリを作ってみる
    * 追加とコミット
    * .gitignore
    * 変更したらまた追加
    * 追加の取り消し
    * ログを見てみる
    * 優先度低
        * 削除
        * リネーム
* svnと違うところ
    * ローカルリポジトリ
    * ステージング領域
    * 連続するリビジョン番号はない
* bitbucket/github にリポジトリを作ってみる
* 共同作業
    * clone
    * pull
        * origin, master
    * リモートブランチとローカルブランチ
    * rebase
    * stash

* svnと違うところ(その２)
    * 基本的に push する前に pull しないとダメ
    * リポジトリ全体をクローンしてしまう
        * 巨大バイナリには向かない
    * リビジョンやブランチの概念

## 調べないといけないこと

* インストール
    * MSYS Git
* ブランチ/マージ/コンフリクト を試してみる
* GUI
    * TortoiseGit
    * MSYS GitのGUI
    * Git Extensions
* 使いやすいGUI diff/マージツール

## Gitの設定

### 名前とe-mailの設定

    git config --global user.name "John Doe"
    git config --global user.email "john.doe@example.com"   

### GUIの文字コード設定

    git config --global gui.encoding utf-8

## TortoiseGit

TortoiseGit は TortoiseSVN っぽく git を使うためのツール。
コマンドライン版の git の機能とは一対一対応していない。
ステージング領域とい概念がないようだ。

## 自分がひっかかったところ

* コマンドの機能が多すぎてフラグ一つで動作が大きく変わる
* ブランチはポインタに過ぎないことがわからないかった
* リモートブランチとかリモート追跡ブランチ
* リモート追跡ブランチの設定方法や確認方法
    * git branch -vv
    * git branch --set-upstream BRANCHNANE origin/BRANCHNAME
* ステージングを取り消す方法
    * ステージング取り消しとコミットの取り消しが同じコマンドなのは怖い

## svn でよく使う機能との対比

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
    * 無視設定                  (.gignore を編集)
    * ブランチ作成              (git -b NEWBRANCH [COMIT or BRANCH])
    * タグ
    * trunk -> branch マージ    (git checkout BRANCH; git merge TRUNK)
    * branch -> trunk マージ    (git checkout TRUNK; git merge BRANCH)
    * リネーム                  (git mv OLDNAME NEWNAME; git commit -am "MESSAGE")

## svn で困っていること

* ブランチ独自の変更とtrunkの取り込みの両立
    * ライブラリバイナリをコミットする場合がある
    * 特殊なワークアラウンドをブランチのみですることがある

## 参考

* Pro Git
* [Git Cheat Sheets JP](http://hail2u.net/documents/git-cheat-sheets-jp.html)
