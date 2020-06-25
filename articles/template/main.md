#### 皆さん。バージョン管理は何を使用していますか？
多くの方がバージョン管理でGitを使用していると思います。Gitめちゃくちゃ便利ですよね！！ ほんとGit様様です。
今回は私がターミナルで設定しているおすすめGitエイリアスを紹介します。エイリアスを設定するとGitコマンドを便利に使用することができます。
ぜひ試してみてください ；）

---
## $ git log の設定
まずは準備として **$ git log** の表示を見やすくする設定を.gitconfigに追加します。 ※[参照URL](https://blog.toshimaru.net/git-log-graph/)

``` gitconfig
# ~/.gitconfig

[alias]
lg = log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %n%s %Cgreen(%cr) %C(bold blue)<%an>%Creset%n' --abbrev-commit --date=relative
```
この設定をして **$ git lg** コマンドを実行するとログが見やすく表示されます。

<div class="col-lg-6 p-0 ">
	<img src="/assets/20200612_Gitおすすめエイリアス設定/pic-1-dc1f9e2d01fc9d5c9e2520f4c89a855bb22aaf59a33a4b2129b81df9126d9b31.jpg" width="100%" >
</div>

<br>

---
## .bashrcにGitエイリアスを設定
次に **.bashrc** にGitエイリアスの設定を追加します。

``` bash
# ~/.bashrc

# git alias settings
alias gs='git status'
alias gd='git diff'
alias gda='git diff --cached'
alias ga='git add'
alias ga.='git add .'
alias gl='git lg'
alias gls='git lg -n8'

function gc(){
    git commit -m "$*"
}

function gdc(){
    echo ""
    git log | grep -A 4 "$*" | tail -n1
    echo ""
    git diff "$*^" "$*"
}
```
追記後は**$ source ~/.bashrc**コマンドを実行し、設定をターミナルに反映させてください。
このGitエイリアスの設定を追加することで例えば、今まで **$ git status** と入力して実行していたコマンドが **$ gs** で実行できるようになります。
設定したGitエイリアスの説明をします。


|  Gitエイリアス  |  実行されるコマンド  |  説明  |
| ---- | ---- | ---- |
|  $ gs  |  $ git status  |  リポジトリの状態を確認  |
|  $ gd  |  $ git diff  |  ファイルの追加・変更内容を確認  |
|  $ gda  |  $ git diff --cached  |  $ git add したファイルの追加・変更内容を確認  |
|  $ ga ファイル名 |  $ git add ファイル名 | ファイル名をコミット対象として追加  |
|  $ ga.  |  $ git add .  |  コマンドを実行したディレクトリ以下にある全てのファイルをコミット対象として追加  |
|  $ gl  |  $ git lg  |  リポジトリのコミットログを新しい順に表示  |
|  $ gls  |  $ git lg -n8  |  リポジトリのコミットログを新しい順に8つだけ表示  |
|  $ gc コミットメッセージ  |  $ git commit -m "コミットメッセージ"  | "コミットメッセージ"で $ git addしたファイルの追加・変更内容をGitリポジトリに登録(コミット)する  |
|  $ gdc ハッシュ値  |  $ git diff "ハッシュ値^" "ハッシュ値"  |  そのコミットのハッシュ値で行われたファイルの追加・変更内容を確認  |

<br>

---
## 簡単な使用例
最後に設定したGitエイリアスを使用した簡単な使用例を紹介します。

``` bash
# Gitローカルリポジトリを作成する流れ
$ mkdir test && cd test && git init # testディレクトリを作りtestディレクトリに移動しGitのローカルリポジトリを作成
$ touch hogehoge.html && ga hogehoge.html # hogehoge.htmlファイルを作成しコミット対象として追加
$ gc first commit # コミットメッセージ'first commit'でGitのローカルリポジトリに登録

# 開発の流れ
$ echo "atyotyo" >>  hogehoge.html # コード編集 "atyotyo"という文字をhogehoge.htmlに追加
$ gs # リポジトリの状態を確認
$ gd # 追加・変更内容を確認
$ ga hogehoge.html # 変更内容に問題なければコミット対象としてhogehoge.htmlを追加
$ gda # もし$ git addした後に追加・変更内容をもう一度確認したい場合に実行する
$ gc modified hogehoge.html # コミットメッセージ'modified hogehoge.html'でGitのローカルリポジトリに登録

# あるコミットの変更内容を確認する流れ
$ gl # コミットログを確認。追加・変更内容を確認したいコミットのハッシュ値をコピー
$ gdc 02eac97  # コミットハッシュ値'02eac97' で行われたファイルの追加・変更内容を確認
```


個人的に **$ gc** と **$ gdc** コマンドがとても便利で気に入っています。;)
例えば、過去に開発した機能を他の開発でも実装したいとき **$ gdc** コマンドを実行して過去の開発時の追加・変更内容を確認したりするような感じで使用しています。
**$ gdc**コマンドを実行すると、この記事の[一番最初の画像](#wrapper)の様な出力結果が得られる思います。
もし皆さんが使用している便利な設定等ありましたら、ぜひ教えてください！

<br><br>
p.s.
今回はじめて技術ブログを書きました。
ブログを書くのって難しい、、、精進します笑
