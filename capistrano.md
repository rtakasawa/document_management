# capistrano関連のドキュメント

## EC2インスタンスを複製して、Capistranoで同時デプロイ

### Yattaで同時デプロイを実施したので手順を残しておく

- 既存のインスタンスから同じインスタンスを作成する
  1. パブリックサブネットを作る
  1. ルートテーブルの設定
  1. 既存のインスタンスのAMIを作成
  1. AMIから新規インスタンスを作成\
  こうすることで既存のインスタンスと同じインスタンスを作成できる。\
  ディレクトリ構成やインストールしたライブラリ、ユーザーも既存のインスタンスと同じ。
  1. ElasticIPの取得、割当\
  IPアドレスを固定しないと以下の設定ができないとの必要

- capistranoの設定
`/config/deploy/production.rb`を下記サイトを参照し編集した
  > https://tackeyy.com/blog/posts/deploy-web-service-to-each-servers

- Nginxの設定ファイルの変更\
`/etc/nginx/conf.d/yatta.conf`のEC2インスタンスのIPアドレスを編集

- デプロイ時のコマンド\
下記サイトを参考にした
  > https://tackeyy.com/blog/posts/deploy-web-service-to-each-servers

### その他：参考情報
#### 今回、新規インスタンスで誤って新たにユーザーを作成したので、権限周りのエラーが発生した。その時の参考情報
- エラー対応で参考にしたサイト
  > https://qiita.com/ironsand/items/cb2e5c777a4cca5e4dd1
- ユーザー一覧の確認コマンド\
`cut -d: -f1 /etc/passwd`