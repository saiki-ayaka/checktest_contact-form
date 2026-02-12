markdown
# check-test お問い合わせフォームの環境構築

## 1. Dockerビルド
    開発環境を構築するために以下コマンドを使用し、ファイル内の記述を行う。
    ・cd check-test
    ・mkdir docker src
    ・touch docker-compose.yml
    ・cd docker
    ・mkdir mysql nginx php
    ・mkdir mysql/data
    ・touch mysql/my.cnf
    ・touch nginx/default.conf
    ・touch php/Dockerfile
    ・touch php/php.ini
    作成ファイルへの記述後、以下コマンドでビルドする。
    ・docker-compose up -d --build
## 2. laravel環境構築

    ・docker-compose exec php bash
    composerを使用してアプリケーションのベースファイルを作成する。(laravelはバージョン８を指定)
    ・composer create-project "laravel/laravel=8.*" . --prefer-dist
    以下コマンドで設定時間の確認を行い、日本時間に合わせる設定を行う。
    ・php artisan tinker
    　> echo Carbon\Carbon::now();
    .envのDB_の行をdocker-compose.ymlで設定した名前などに変更する。
    アプリケーションキーの生成を行う。
    ・docker-compose exec php php artisan key:generate
    マイグレーションの実行を行う。データベースにテーブルを作成する。
    ・php artisan migrate
    初期データ(シーダー)の投入を行う。
    ・php artisan db:seed

## 3. GitHubでリポジトリを作成する。
    checktest_contact-formの名前で作成。
    https://github.com というURLをコピーし、check-testディレクトリに移動後、以下のコマンドを実行する。
    ・git init
    ・git add .
    ・git commit -m "first commit"
    ・git branch -M main
    ・git push -u origin main

## 4. 開発環境

## 5. 使用技術(実行環境)
    ・Language: PHP 8.1.34
    ・Framework: Laravel 8.83.29
    #・JavaScript: jquery?(Laravel 8 のデフォルト（Laravel Mixなど）で入っていることが多いですが、使わなければ消してOK)
    ・Database: MYSQL 8.0.26
    ・WebServer: nginx 1.21.1
    ・tool: phpMyAdmin
    ・Container: Docker / Docker Compose


## 6. データベース設計図（ER図）
![ER図](./database-design.drawio.png)

## 7. アクセスURL
    ・開発環境　http://localhost
    ・phpMyAdmin　http://localhost:8080


## (?. テーブル一覧)
- **users**: 利用者情報
- **categories**: お問い合わせの種類
- **contacts**: お問い合わせ詳細