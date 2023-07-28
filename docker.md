```
FROM ruby:2.5
RUN apt-get update -qq && apt-get install -y build-essential libpq-dev nodejs

# // 「-qqオプション」はエラー以外何も吐かないことを意味する。
# // 「-y」オプションは全部yesで実行することを意味する。

RUN mkdir /myapp
WORKDIR /myapp

COPY Gemfile /myapp/Gemfile
COPY Gemfile.lock /myapp/Gemfile.lock

RUN bundle install
COPY . /myapp

```
FORM : 使用するイメージとバージョン
RUN :　コマンドの実行
WORKDIR :　作業ディレクトリの設定
COPY :　コピー元とコピー先のファイルまたはディレクトリを指定

Dockerfileとは、Dockerのイメージを自動で作成してくれるファイル

apt-getコマンドは、Debian系のディストリビューション（DebianやUbuntu）のパッケージ管理システムであるAPT（Advanced Package Tool）ライブラリを利用してパッケージを操作・管理するコマンドです。

COPY Gemfile /myapp/Gemfileはコンテナの中のmyappのGemfileにコピーしてあげるという意味　左がホスト側(自分のコンピュータ側)　右が仮想環境側のファイル

RUN bundle installはコンテナの中でbundle installをするという意味

COPY . /myappはホスト側の全部のファイルやディレクトリを


## Docker Compose
Docker Composeは、Dockerコンテナを簡単に定義、実行、管理するためのツールです。複数のDockerコンテナを1つのアプリケーションとしてグループ化し、コンテナ間の相互作用や設定を定義できるため、複雑なマルチコンテナアプリケーションを容易に展開できます。


FROM ruby:2.5: この行は、Rubyの公式Dockerイメージのバージョン2.5をベースにしていることを指定しています。つまり、このコンテナはRuby 2.5がインストールされた状態から始まります。

RUN apt-get update -qq && apt-get install -y build-essential libpq-dev nodejs: この行では、Dockerコンテナ内で実行されるコマンドを指定しています。ここでは、まずapt-get updateコマンドを実行して、パッケージリストを最新の状態に更新しています。次に、apt-get installコマンドを使って、build-essential（ビルドに必要なツール）、libpq-dev（PostgreSQLの開発用ライブラリ）、nodejs（Node.jsランタイム）をインストールしています。

RUN mkdir /myapp: この行では、コンテナ内に/myappというディレクトリを作成しています。

WORKDIR /myapp: この行では、以降のRUN、CMD、ENTRYPOINTなどのコマンドが実行されるディレクトリを/myappに設定しています。以降のコマンドは、/myappディレクトリ内で実行されることになります。

COPY Gemfile /myapp/Gemfile: この行では、ホストマシンのカレントディレクトリにあるGemfileを、コンテナ内の/myappディレクトリにコピーしています。

COPY Gemfile.lock /myapp/Gemfile.lock: この行では、ホストマシンのカレントディレクトリにあるGemfile.lockを、コンテナ内の/myappディレクトリにコピーしています。

RUN bundle install: この行では、bundle installコマンドを実行して、GemfileにリストされたRubyのGem（ライブラリやパッケージ）をインストールします。

COPY . /myapp: この行では、ホストマシンのカレントディレクトリにあるすべてのファイルを、コンテナ内の/myappディレクトリにコピーしています。これにより、アプリケーションのソースコードやその他のファイルがコンテナ内に配置されます。

以上のDockerfileをビルドすると、Ruby 2.5がインストールされ、必要なパッケージとGemがインストールされた状態のDockerコンテナが作成されます。そして、ホストマシンのカレントディレクトリにあるアプリケーションのファイルがコンテナ内の/myappディレクトリにコピーされます。これにより、アプリケーションをDockerコンテナ内で実行する準備が整います。


bundle installは、Rubyプロジェクトで使われる依存関係管理ツールであるBundlerを使って、プロジェクトに必要なGem（Rubyのライブラリやパッケージ）をインストールするコマンドです。

Rubyのプロジェクトでは、通常、外部のライブラリやパッケージを利用することがあります。これらの外部ライブラリはGemと呼ばれ、Bundlerを使用してプロジェクトに追加できます。GemはRubyプロジェクトの依存関係を解決し、必要なライブラリを簡単に管理することを可能にします。

bundle installコマンドは、プロジェクトのルートディレクトリにあるGemfileとGemfile.lockファイルを基にしてGemの依存関係を解決し、必要なGemをインストールします。Gemfileはプロジェクトの依存関係を定義したファイルであり、Gemfile.lockは現在のGemのバージョンや依存関係がロックされたファイルです。これにより、複数の開発環境やデプロイ環境で一貫性のあるGemのバージョンを保つことができます。

具体的には、bundle installコマンドはGemfileに記述されたGemの一覧を解析し、Gemの依存関係を満たすようにGemのバージョンを決定します。そして、これらのGemをインストールします。このようにして、開発者はプロジェクトの依存関係を明確に定義し、開発環境やデプロイ環境での動作を安定させることができます。




