## Reactとは
画面を作成するJavaScriptのライブラリ。JQueryやVue.jsみたいなもの。React.jsとも書かれる。
単体では動かず、Node.jsで作ったプロジェクトの中で使用する。

## Node.js
もともとJavaScriptはブラウザ上でしか動作しなかったが、開発者向けにPC上でも動かせるような実行環境としてNode.jsが開発された。  
ブラウザ使用の開発と比べてどのような利点があるかというと、コードエラーが書いた時点で分かったり、ライブラリの依存関係で揉めなかったり、  
本番環境に近い形でテストができたり・・・というものらしい。
ビルド→動作確認でJavaScriptが動かない、F12で構文エラーを探して、といった煩わしさが無くなる。

## npm
JavaScriptで動作するパッケージ管理ツール。Node.jsで使用する（一緒に付いてくる）。
これを用いることで、js同士の依存関係や競合関係の問題を解決してくれる。
また、package.jsonに書いたスクリプトを実行する機能を持つ。  

例）ライブラリ追加
```cmd
npm install react
```
例）スクリプト実行
```cmd
npm run dev
```
<img width="506" height="533" alt="4" src="https://github.com/user-attachments/assets/798338cd-1738-4b50-a01b-841d8db8ee96" />

