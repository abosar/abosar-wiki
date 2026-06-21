# Main
## やりたいこと
Django（Python） + React.jsで構成されたWebアプリの作成。  
（どういうアプリを作りたいかはまだ定まっていない。）  
React.jsは画面周りを担当し、DjangoはAPI（プログラム間の窓口）や認証を担当する。  
DBはDjangoにSQLiteが付いてくるらしいので十分かと思っているが、  
とりあえずダミーデータでも良いので動くところを目標とする。  

<img width="511" height="674" alt="image" src="https://github.com/user-attachments/assets/eb7d4966-f68b-4fc4-b089-00f3cba3748c" />  

MVCでControllerと呼ばれていた部分が、Djangoではviews.pyとなっているので混同注意。

<img width="597" height="292" alt="image" src="https://github.com/user-attachments/assets/07d7ad1e-466e-41aa-9c5f-7e7e6c1ceed3" />

<img width="299" height="250" alt="image" src="https://github.com/user-attachments/assets/b5f3b95a-838a-4a21-acac-8fcf70694d29" />

## 環境構築
まずはインストールから。自分のPCには既にPythonとGitは入っていたが念のため記載しておく。  
```cmd
winget install Python.Python.3.12
winget install OpenJS.NodeJS.LTS
winget install Git.Git
```
インストールできたか確認。
```cmd
python --version
node --version
npm --version
git --version
```
Python3.12.10、node.jsはv24.17.0、npmは11.13.0、gitは2.54.0であることが確認できた。  

今回はひとまず音楽アプリを作る想定で、musicnewsというフォルダをgitで管理する。
プロジェクト全体の位置でgit init（initialize:初期化の略）を送信。
```cmd
C:\code\musicnews git init
```
今回のフォルダ構成。
```
musicnews/
├── .git/
├── .gitignore
├── server/     ← Djangoの雛形を作成するフォルダ。バックエンド
└── client/     ← Reactの雛形を作成するフォルダ。フロントエンド
```

※省略するが、この辺りでGitHubにPushしている。（.gitignoreなどフォルダ内に何かしらのファイルが必要。）
```
1. abosar-wikiをPCにclone
2. その中にmusicnewsフォルダを作成（コピー）
3. git add .
4. git commit -m "◯◯"
5. git push
```

## バックエンドの雛形作成
severフォルダで作業する。まずはPython標準モジュールのvenv（virtual environmentの略）を使用し、
PC自体にパッケージがインストールされないよう仮想環境を作成する。
以下はpythonのモジュール（-m）からvenvを使用し、フォルダ名を.venvにするという意味。
```cmd
C:\code\musicnews\server python -m venv .venv
```
以降、本プロジェクトでPythonライブラリをインストールしたい時はvenvのアクティベートをしてから行う。  
（毎回コマンドプロンプトやPowerShell起動時に1回有効化する必要がある。）  
早速Djangoのインストールで試してみる。以下はコマンドプロンプトの場合。
```cmd
C:\code\musicnews\server .venv\Scripts\activate.bat
# ↓に表示が変わる
(.venv) C:\code\musicnews\server>pip install django
```
成功時、「Successfully installed asgiref-3.11.1 django-6.0.6 sqlparse-0.5.5 tzdata-2026.2」と表示を確認。
C:\code\musicnews\server\.venv\Lib\site-packagesを見ると確かにライブラリのフォルダが追加されている。

続いて以下のパッケージもインストールする。
djangorestframeworkはReactとDjangoの間をjsonでやり取りする（REST）ために必要で、
django-cors-headersはReactからDjangoのAPIを呼ぶために必要。
```
pip install djangorestframework django-cors-headers
```

補足）Reactは`http://localhost:5173`、Djangoは`http://127.0.0.1:8000`と別々のサイトで動く。  
ブラウザは別サイト同士の通信をブロック（CORS）するが、django-cors-headersを使うことで許可の設定が書ける。  

## Pythonで環境再現するためのファイル作成
以下のコマンド。このテキストファイルを使用することで、同じPython環境が他PCでも再現できる。
```
C:\code\musicnews\server>pip freeze > requirements.txt
```
requirements.txtのあるフォルダで以下のコマンドを打つと、記載されたパッケージをすべてインストールしてくれる。  
（venvを使用しないとグローバルにインストールされることに注意）  
```
pip install -r requirements.txt
```
