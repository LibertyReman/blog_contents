
#### 夏が近づいてきましたね。。。。
本田翼さんがYouTubeでドクタージャルトの[スティックタイプの日焼け止め](https://www.amazon.co.jp/Dr-Jart-ドクタージャルトゥエブリ線デーサンスティック-SPF50-Every-Stick/dp/B07CYVGXC5)を紹介していました。
それを見て、スティックタイプの日焼け止めなんかあるんや！と気になって買ってみました
本当は同じ物を買いたかったんですが、人気になりすぎて品切れで買えませんでした（泣）

デザインは良い たしかにさっと濡れる感じは良いのかもしれない


使用感
伸びにくい。液体のほうが肌に馴染んで しっかり濡れている感じがする


けど、しっかり濡れているか液体に比べてわかりにくいなーって思いました


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
大阪の夏って東京よりムシムシしてて、暑く感じませんか（泣）