# docker-laravel
PHP + Nginx + MySQLをDockerで動作させ、laravelフレームワークを使って開発を開始するための手順を説明する

## 参考資料
- 【図解】Dockerの全体像を理解する
  - https://qiita.com/etaroid/items/b1024c7d200a75b992fc
  - https://qiita.com/kotaro-dr/items/88ec3a0e2d80d7cdf87a
- laravel公式サイト
  - http://laravel.jp/
  - https://laravel.com/
- Visual Studio CodeでPHPをデバッグする方法
  - https://qiita.com/deux222/items/af75319ece05653c4bb5
- Composerについて
  - https://qiita.com/niisan-tokyo/items/8cccec88d45f38171c94
- Visual Studio Codeの使い方
  - https://www.atmarkit.co.jp/ait/articles/1507/10/news028.html

## ローカル開発環境構築
- 以下からDockerDesktopのWindows版をダウンロードしインストールする
   - https://hub.docker.com/editions/community/docker-ce-desktop-windows
- 以下からVisualStudio CodeのWindows版をダウンロードしインストールする
  - https://code.visualstudio.com/download
- VisualStudioCodeを起動してサイドナビの拡張機能アイコンをクリック
- 下記拡張機能を検索してインストールする
  - Docker
  - Git History
  - Japanese Language Pack for Visual Studio Code
  - PHP Debug
  - PHP Intelephense

## 初回コンテナ起動してプロジェクトを作成
- VisualStudioCodeの表示メニューからターミナルを選択
- 画面下に表示されたターミナルで下記コマンドを実行
  - docker-compose up -d --build
- ターミナルで以下のコマンドを実行してPHPコンテナにログイン
  - docker-compose exec php /bin/bash
- コンテナにログイン後下記コマンドを実行してlaravelのプロジェクトを作成
  - composer create-project --prefer-dist laravel/laravel プロジェクト名
- srcフォルダ内にプロジェクトフォルダが作成されその配下にソースコードが生成される
中身をプロジェクトフォルダの同じ階層に移動し空のプロジェクトフォルダは削除する
- 下記URLをブラウザで開くとＴOPページが表示される
  - http://localhost:5000/

## 次回以降コンテナを起動時に行う操作
- VisualStudioCodeのターミナルで下記コマンドを実行
  - docker-compose start

## コンテナ停止時に行う操作
- VisualStudioCodeのターミナルで下記コマンドを実行
  - docker-compose stop

## デバッグ実行を行う
- VisualStudioCodeサイドナビの実行アイコンをクリック
- サイドメニュー上部の再生ボタンをクリック
- PHPソースコード上の任意行の列番号をクリックしブレークポイントを設定
- PHPプログラムを実行するとブレークポイントを設定した位置でプログラムが停止し、F11でステップ実行ができます
