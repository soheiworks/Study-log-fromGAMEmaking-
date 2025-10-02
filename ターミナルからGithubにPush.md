① GitHub作業用のディレクトリに移動する

②リポジトリをローカルPCにクローンする
git clone ttps://github.com/soheiworks/<mark style="background: #FF5582A6;">Rot-addict.git</mark> ←リポジトリ名
   Rot-addictというディレクトリが生成されるので、中にアップロード(push)したいファイルを入れる。
 （git cloneはローカルPCにリポジトリの内容をコピーするので、PCごとに最初の1回だけで良い。）

③鍵を作る
　ssh-keygen -t<mark style="background: #ADCCFFA6;"> ed25519 </mark>-C "soheiworks@users.noreply.github.com"
　Curve25519という楕円曲線（数学的なカーブ）を使っているので、このコマンド名になっている。 

④ssh-agent（鍵を保管する場所）を起動
　eval "$(<mark style="background: #FFF3A3A6;">ssh-agent -s</mark>)"
 ↓↓<mark style="background: #FFF3A3A6;">ssh-agent -s </mark>コマンドを実行すると、これが出てくる。↓↓ 
 ―　―　―　―　―　―　―　―　―　―　―　―　―　―　―　―　―　―　―　―　―　―
　SSH_AUTH_SOCK=/tmp/ssh-0oWPoPyot3hb/agent.1345; export SSH_AUTH_SOCK;
　SSH_AGENT_PID=1346; export SSH_AGENT_PID;
　echo Agent pid 1346;
 ―　―　―　―　―　―　―　―　―　―　―　―　―　―　―　―　―　―　―　―　―　―
eval "$( )" にすると、シェルがその中身を実行コマンドに変えて実行する。

⑤ssh-agentに生成した鍵を登録
　sh-add ~/.ssh/id_ed25519

⑥登録した鍵を表示する
　cat ~/.ssh/id_ed25519.pub

⑦表示させた鍵をGitHubに貼り付け
　→ GitHubの右上のアイコンをクリック→ Settings
　→ 左のコマンド列から、🗝 SSH and GPG keysをクリック
　→ 右上の <mark style="background: #BBFABBA6;">New SSH key </mark>をクリック
　　　→ Title : ONEXminiなどのPC名
　　　→ Key type：Authentication Key
　　　→ Key：⑥で表示された鍵をコピペして、<mark style="background: #BBFABBA6;">Add SSH key</mark> をクリック

⑧ssh -T git@github.com
　Hi soheiworks! You've successfully authenticated... と出れば完了。

⑧git add Rot-addict.c
   pushしたいファイルをセット
   ※ git add . にすれば、ディレクトリ内のファイルが全てセットされる
   ※git addしたファイルのaddを止めたい場合は、git reset <mark style="background: #ABF7F7A6;">Rot-addict.c </mark> ←ファイル名
   　git addしたすべてのファイルのaddを止めたい場合は、git reset

⑨git commit -m "ファイル変更の内容”
　※commit済のファイルを止めたい場合は、 git reset HEAD^

⑩git push origin main
　（リモートリポジトリ<mark style="background: #FFB86CA6;">origin </mark>に、ローカルの<mark style="background: #D2B3FFA6;">main</mark> branchの内容を飛ばすという意味）

<mark style="background: #FFB86CA6;">origin</mark>　は、Githubのリポジトリのこと
<mark style="background: #D2B3FFA6;">main</mark>　は、デフォルトのブランチ名（昔はmasterと呼ばれた）


以下、イメージ
⑧の　add　は、発射台にロケットを載せる
⑨の　git commit -m は、打ち上げ前にどんなロケットかアナウンス
⑩の　git push origin main で、打ち上げ
