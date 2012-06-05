## gitセミナーでやってみたいこと

* gitをローカルリポジトリで使ってみる
    * リポジトリを作ってみる
	* 
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
	* 追加 -> コミット
	* 修正 -> コミット
	* 元に戻す
	* 更新
	* 削除
	* ログ
	* ベースと比較
	* 特定のリビジョンとの比較
	* 変更のチェック
* 頻度が低いもの
	* ブランチ
	* タグ
	* trunk -> branch マージ
	* branch -> trunk マージ
	* リネーム

## svn で困っていること

* ブランチ独自の変更とtrunkの取り込みの両立
	* ライブラリバイナリコミット
	* 特殊なワークアラウンド

## 参考

* Pro Git
* [Git Cheat Sheets JP](http://hail2u.net/documents/git-cheat-sheets-jp.html)
