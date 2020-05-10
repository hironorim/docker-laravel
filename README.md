# docker-laravel
PHP + Nginx(WEBサーバー) + MySQL(DBサーバー)をDockerで動作させ、laravelフレームワークを使って開発を開始するための手順を説明する
エディタはVisualStudioCode、DB接続クライアントはHeidiSQLを使用する

## 環境構築の参考資料
- 【図解】Dockerの全体像を理解する
  - https://qiita.com/etaroid/items/b1024c7d200a75b992fc
  - https://qiita.com/kotaro-dr/items/88ec3a0e2d80d7cdf87a
- Composer(PHPパッケージ管理ツール)について
  - https://qiita.com/niisan-tokyo/items/8cccec88d45f38171c94
- Visual Studio Codeの使い方
  - https://www.atmarkit.co.jp/ait/articles/1507/10/news028.html
- Visual Studio CodeでのGitの基本操作まとめ
   - https://qiita.com/y-tsutsu/items/2ba96b16b220fb5913be
- Visual Studio CodeでPHPをデバッグする方法
  - https://qiita.com/deux222/items/af75319ece05653c4bb5

## 開発ドキュメント
- PHPドキュメント
  - https://www.php.net/manual/ja/index.php
- 日本語laravel公式サイト
  - http://laravel.jp/
- 英語laravel公式サイト
  - https://laravel.com/
- larravelチュートリアル
  - https://hobby23.net/archives/laravel-tutorial/
- nginxについてまとめ(設定編)
  - https://qiita.com/morrr/items/7c97f0d2e46f7a8ec967
- Dockerドキュメント
  - http://docs.docker.jp/index.html

## ローカル開発環境構築
- 以下からDockerDesktopのWindows版をダウンロードしインストールする
   - https://hub.docker.com/editions/community/docker-ce-desktop-windows
- 以下からVisualStudio CodeのWindowszip版をダウンロードして任意のフォルダに展開
  - https://code.visualstudio.com/download
- VisualStudioCodeを起動してサイドナビの拡張機能アイコンをクリック
- 下記拡張機能を検索してインストールする
  - Docker
  - Git History
  - Japanese Language Pack for Visual Studio Code
  - PHP Debug
  - PHP Intelephense
- SourceTreeに内蔵された下記gitフォルダにパスを通す
  - C:\Users\[ログインユーザー名]\AppData\Local\Atlassian\SourceTree\git_local\bin
- パスを通す方法は以下を参照
  - https://qiita.com/shuhey/items/7ee0d25f14a997c9e285
- 以下からHeidiSQLをダウンロードして任意のフォルダに展開
  - https://www.heidisql.com/download.php?download=portable-64

## 初回コンテナ起動してプロジェクトを作成
- DockerDesktopを起動
- VisualStudioCodeの表示メニューからターミナルを選択
- 画面下に表示されたターミナルで下記コマンドを実行
  - docker-compose build --no-cache --force-rm
  - docker-compose up -d
- ターミナルで以下のコマンドを実行してPHPコンテナにログイン
  - docker-compose exec php /bin/bash
- コンテナにログイン後下記コマンドを実行してlaravelのプロジェクトを作成
  - composer create-project --prefer-dist laravel/laravel プロジェクト名
- srcフォルダ内にプロジェクトフォルダが作成されその配下にソースコードが生成される
中身をプロジェクトフォルダの同じ階層に移動し空のプロジェクトフォルダは削除する
- 下記URLをブラウザで開くとＴOPページが表示される
  - http://localhost:5000/
- storageフォルダのpermissionエラーが出たら下記コマンドを実行して書き込み権限を付与する
  - chmod -R 777 storage

## コンテナ停止時に行う操作
- VisualStudioCodeのターミナルで下記コマンドを実行
  - docker-compose stop

## コンテナを起動時に行う操作
- VisualStudioCodeのターミナルで下記コマンドを実行
  - docker-compose start

## コンテナを作成しなおして再起動
- VisualStudioCodeのターミナルで下記コマンドを実行
  - docker-compose down --rmi all --volumes
  - docker-compose build --no-cache --force-rm
  - docker-compose up -d

## PHPデバッグ実行を行う
- VisualStudioCodeサイドナビの実行アイコンをクリック
- サイドメニュー上部の再生ボタンをクリック
- PHPソースコード上の任意行の列番号をクリックしブレークポイントを設定
- PHPプログラムを実行するとブレークポイントを設定した位置でプログラムが停止し、F11でステップ実行ができます

## データベースに接続
 - HeidiSQLを起動
 - IPは127.0.0.1、ポートは3306、.envファイルに記載されてユーザー名とパスワードを入力して開くボタンを押す

# ファイル
 - WEBサーバーのログ
   - /logs/access.log
 - PHPエラーログ
   - /logs/php-error.log
 - mysqlの設定ファイル
   - /docker/mysql/my.conf
 - nginxの設定ファイル
   - /docker/nginx/default.conf
 - phpの設定ファイル
   - /docker/php/php.ini
 - php opcacheを有効にしないファイルリスト
   - /docker/php/php.ini
   - Dockerからwindowsファイルシステムのアクセスが遅いので、laravelのようなサイズの大きいWEBフレームワークを使用するとページの表示が遅くなる。opcacheというコンパイルしたPHPコードをメモリにキャッシュする機能を使用して表示速度を上げる。
   有効にするとプログラムの即時反映がされなくなるので、開発者が更新するフォルダを除外リストに追加する。
 - phpのDockerファイル
   - /docker/php/Dockerfile
 - .環境設定ファイル(DB接続情報等)
   - /.env
 - DockerComposeファイル
   - docker-compose.yml
