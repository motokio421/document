# LaravelでWebアプリを作成

## 概要
このカリキュラムではLaravelを使用した
Webアプリケーション(日記アプリ)を作成します。
実際にWebアプリケーションを作成することで、
開発の手順や、Laravelの機能などについて学んでいきます。

今回は全8ページからなる日記アプリを作成します

## カリキュラムに関して
実際に作業に入る前にカリキュラムに関しての説明です。  
- 各セクションには公式サイトのリンクを貼っています。
  - Laravelは非常に多機能なため、  
    カリキュラムでは、最低限必要な内容の記述にとどめています。  
    詳細を知りたい場合は公式サイトをご確認ください。
- コマンドの実行はLaravelのルートディレクトリ(app, bootstrapなどが保存されているフォルダ)で実行する必要があります。 
  - 本カリキュラムでLaravelをインストールするディレクトリのことです。   
- コマンドはターミナル(コマンドプロンプト)で実行します。  
- 編集するファイルの名称はコードの上部にコメントアウトで記載してます。  
- Gitでのバージョン管理の復習も兼ねて、最低1カリキュラムに1回はcommitしましょう。
  - 適切にcommitしておくことでLaravelの復習もしやすくなります。

## 事前準備
まずは開発のための準備を行います。  
実施することは、以下4つです。    
1. Laravelのインストール
2. 環境設定
3. DBの作成
4. 起動確認

## Laravelのインストール

まずは任意のディレクトリに移動します。  
```php
// 例

// ディレクトリの作成
mkdir ~/Desktop/NexSeed/Laravel

// ディレクトリの移動
cd ~/Desktop/NexSeed/Laravel
```

移動先のフォルダで以下のコマンドを実行してLaravelをインストールします。  
`composer create-project laravel/laravel --prefer-dist Diary 5.7`

## 環境設定
インストールしたLaravelをエディタで開きます。  
`.env.example`をコピーして、`.env`を作成します。

以下の通り追加、編集してください。
```php
// .env
DB_DATABASE=Diary // 編集
DB_USERNAME=root // 編集
DB_PASSWORD= // 編集
DB_SOCKET=/Applications/XAMPP/xamppfiles/var/mysql/mysql.sock // 追加
```

### MySQLのバージョンが5.7.7未満の場合
AppServiceProviderを編集
```php
// App/Providers/AppServiceProvider.php

use Illuminate\Support\Facades\Schema; //追加

public function boot()
{
    Schema::defaultStringLength(191); //追加
}
```

## DBの作成
Diaryという名前のDBを作成します。  

## 起動確認
- プロジェクトのルートディレクトリに移動
- `php artisan serve`でビルトインサーバを起動
- localhost:8000にブラウザからアクセス
- laravelのTOPページが表示されていることを確認する

## 参考リンク
[公式ドキュメント](https://readouble.com/laravel/5.7/ja/)