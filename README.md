# git の使い方

### 1.まず最初にすべきこと
### 2.基礎コマンド(最低限これは覚えよう)
### 3.覚えるべき補助コマンド
### 4.gitのbranchを活かすコマンド


## 1.まず最初にすべきこと
```
$ git config --global user.name "Your Name"
$ git config --global user.email your-email@example.com
```
すでにやっている方は無視してかまいません。
あなた自身についての設定をするコマンドです。
この他にも、gitで使うeditorを変更したい、という時は`$ git config --global core.editor /usr/bin/vim`などとすることができます。
絶対PATHが良いかと思います。(なんとなく)

また、gitコマンドの出力はデフォルトでは色分けなどされていないため見づらい場合が多いです。
このときに自動で色をつけてくれる設定が`$ git config --global color.ui auto`です。

`$ git config --help`でその他の情報を見ることができます。

また、gitコマンドの各ヘルプはconfigと同じように`$ git CMD --help`で参照することができます。

## 2.基礎コマンド(最低限これは覚えよう)
```
$ git clone
$ git add
$ git commit
$ git push
$ git pull
```

まずはこれを覚えます。

- `$ git clone REPOSITORY`
repository から Project を持ってくるコマンド

- `$ git add FILE OR DIRECTORY`
変更のあるファイルをgitにindex領域に読み込ませます。
このことをstagingと言います。
イメージ的にはgitのバッファに置かれる感じ。

- `$ git commit`
index領域にあるstagingされた変更を確定します。
commit messageはしっかり記述するように心がけましょう。
オプション無しだとeditorが起動されます。
日本語も使えます(環境によるはず？)

- `$ git push`
localでの作業内容をrepositoryにアップロードします。

- `$ git pull`
repositoryから最新の状態をlocalに反映させます。

### 2-1.基礎コマンドの応用
- `$ git push -u REMOTE BRANCH`
大抵の場合は $ git push -u origin master とする人が多いはずです。
-uオプションは、今後のgit pushやgit pullを設定したREMOTE BRANCHに対して行う、というものです。
1度つければ、その後はgit pushするだけで設定された場所に対して行います。
追跡オプションです。

- `$ git add -p`
リンク集に詳しい説明のページを載せていますので、ここでは簡単に。
このコマンドではソースコードの変更を1行レベルで行うことが可能となります。
もちろん複数行も可能。
対話式で色分けして表示してくれるのでとても便利です。
stagingする際にはこのコマンドを積極的に利用しましょう。

- `$ git commit -m '#ISSUE-NUMBER'`
githubとかだと、commit messageに #1 のようなissue番号を付けると、連携してくれるという便利機能がある。
gitlab5.4の現在(2013/10/03)では非対応のようで、現在最新版の6.1では対応しているらしい。
近いうちにアップデートします。

### 2-2.非推奨(?)な基礎コマンドの応用
- `$ git add .`
全てのファイルをindex領域に読み込みます。
非推奨だと思います。git commit -aと同じような感じなので理由は後述。
Initial commitとかの時にはいいのかな、とか思います。

- `$ git commit -m 'COMMIT MESSAGE'`
commit をワンライナー(1行)で終了させる構文です。
詳しいcommit内容を記述することができないのであまり推奨はされないらしい（？）

- `$ git commit -a`
このコマンドは全ての変更をcommitするという内容で、gitを使う場合はやらない方が良いコマンドです。
Mercurialと同じような使い方になってしまうためです。
細かくcommitすることができるのがgitの特徴なので、使わないように心がけましょう。

* 基本的にはここまで覚えて最低限の知識です。 *

## 3.覚えるべき補助コマンド
```
$ git log
$ git diff
$ git status
```

これらは補助のためのコマンドです。

- `$ git log`
これまでのlogを表示してくれます。
内容は大体以下のようなフォーマットです。

>$ git log
>commit a3ad5268fc854e72ab83d03f1612b261a5b9060b
>Author: Yosuke OTA <yota@ns.ie.u-ryukyu.ac.jp>
>Date:   Thu Oct 3 09:45:24 2013 +0900
>\ 
>\    Update README
>\ 
>commit b20186deb59cabb9d780df764bce734245fbcc89
>Author: Yosuke OTA <yota@ns.ie.u-ryukyu.ac.jp>
>Date:   Thu Oct 3 09:39:57 2013 +0900
>\ 
>\    #1 Issue
>\ 
>commit a416ec305342a133b251ef3533bf503f44bee373
>Author: Yosuke OTA <yota@ns.ie.u-ryukyu.ac.jp>
>Date:   Thu Oct 3 09:38:08 2013 +0900
>\ 
>\    Update README about Issue-Number
>\ 
>commit 75dbb46b11725ca501ff0b67f5f2206437613923
>Author: Yosuke OTA <yota@ns.ie.u-ryukyu.ac.jp>
>Date:   Thu Oct 3 09:22:12 2013 +0900
>\ 
>\    Initial commit

- `$ git diff`
差分を表示してくれるコマンドです。
この状態でreturnすると、最新のcommitと現在のコードの差分を表示します。

- `$ git status`
現在の状態を知ることができます。
未commit状態のindex領域のファイルや、stagingされていないファイルを表示します。

### 3-1.覚えるべき補助コマンドの応用
- `$ git log -5   # または git log -n 5`
最近の5つのcommit logを表示する。

- `$ git log HASH`
git logしたときに出てくるcommitの横の文字列(hash)を書き込むことで、表示するcommit logの特定を行えます。
HASHは、commitの特定が出来れば良いので頭から4文字とかくらいでも問題なかったりします。

- `$ git log -p`
パッチ形式で変更を見ることができます。

他にもcommit logを検索してくれる--grepとか、いろいろ見れるので検索してみてください。

- `$ git diff HEAD~2`
HEADから2つ前との差分を見ることができます。
数字は変更可能です。
HEADというのは、現在あなたが作業している場所を指します。
BRANCHだったり。

## 4.gitのbranchを活かすコマンド
```
$ git checkout
$ git merge
$ git fetch
```

この辺りからはバージョン管理システムのBRANCHという考えが大事になってきます。
BRANCHについての説明は置いといて、checkoutによる操作の方法を記します。

- `$ git checkout BRANCH`
BRANCHコマンドに切り替えるコマンドです。
また、checkoutはその他にもファイルをcommitからindex領域に戻したりする際にも利用します。

- `$ git checkout -b aiueo`
aiueoというブランチを作成して、同時にaiueoブランチに切り替えます。

- `$ git merge BRANCH`
mergeとは、他のブランチの変更内容と現在のブランチの内容を合併させることです。
オプションをつけて`$ git merge --no-ff`とすることで必ずcommitを行うようにしましょう。

- `$ git fetch`
リモートからデータを取ってきます。
`$ git pull`と混合するかもしれませんが、fetchではデータを取ってきた後は何もしません。
`$ git pull` == `$ git fetch && git merge origin/master` という関係です。

## 4-1.どんなときに使うか

## 1. リンク集
[Markdown記法のチートシート](http://qiita.com/Qiita/items/c686397e4a0f4f11683d)
[git add -pについて](http://qiita.com/crifff/items/1abf08bca4ce51db4775)
[git log 全部入り](http://qiita.com/imudak/items/4a8549b46fe2e509a08c)
[git コマンド 見る編](http://d.hatena.ne.jp/naokirin/20111202/1322576420)
[HEAD^nとかHEAD~nとか](http://qiita.com/takoba_/items/bcda4c796778ecabe3b1)
[git checkout 使い方](http://transitive.info/article/git/command/checkout/)
[git merge 使い方](http://transitive.info/article/git/command/merge/)
[git push.defaultについて](http://qiita.com/misopeso/items/ede49b661cc7ad30528a)
