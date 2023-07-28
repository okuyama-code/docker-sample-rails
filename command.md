docker-compose up -d

docker-compose exec web bash


2.コンテナを起動し、環境構築に必要なコマンドを特定する。
docker-compose up -dをしたのち、docker-compose exec web bashをします。こうすることでwebという名称のアプリケーション側のコンテナの中のbashを起動できます。
このステップでは、コンテナの中でrailsのアプリケーション起動を行い、http://localhost:3000 でWebアプリにアクセスできるようにします。ここで入力したコマンドがそのまま環境構築に必要なコマンドになるため、重要な作業になります。
ここからはDockerの話というよりはRailsのアプリケーション起動に必要なコマンドの話となります。
まず、$ rails db:createを入力してDBの作成を行います。
その後、$ rails db:migrateを入力してmigrationファイルの内容をDBに反映します。
最後に、rails s -b 0.0.0.0を入力して、Railsサーバーを起動します。
これらを入力した後、ブラウザ上でhttp://localhost:3000 を入力することでWebアプリにアクセス可能になります。

rails new アプリケーション名 （オプション）


rails new a

cd a

rails s サーバー起動
