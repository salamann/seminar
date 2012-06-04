## gitセミナーでやってみたいこと

* gitをローカルリポジトリで使ってみる
    * リポジトリを作ってみる
    * 追加とコミット
    * 変更したらまた追加
    * .gitignore
* svnと違うところ
    * ローカルリポジトリ
    * ステージング領域
    * 連続するリビジョン番号はない
* bitbucket/github にリポジトリを作ってみる
* 共同作業
    * clone
    * pull
        * origin, master
    * ローカルブランチ
    * rebase
    * stash

* svnと違うところ(その２)
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
* 使いやすいマージツール

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

## 参考

* Pro Git
* [Git Cheat Sheets JP](http://hail2u.net/documents/git-cheat-sheets-jp.html)
