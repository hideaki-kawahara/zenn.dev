---
title: "PHPBrewでPHP8を入れる"
emoji: "🐘"
type: "tech"
topics: ["PHPBrew", "mac", "PHP8"]
published: True
---

# PHP8が出た

2020年11月26日にPHP8が正式にリリースされました。
[https://www.php.net/archive/2020.php#2020-11-26-3](https://www.php.net/archive/2020.php#2020-11-26-3)

色々と変わったPHP8を触ってみたいですよね？PHPBrewならできます。


## PHP

PHPBrewにPHP8.0.0対応版が出ておりました。
[https://github.com/phpbrew/phpbrew/releases/tag/1.27.0](https://github.com/phpbrew/phpbrew/releases/tag/1.27.0)

以前の記事では、PHPBrewでPHPの環境を作っていたので、PHPBrewを使ってみたいと思います。
[https://zenn.dev/sapi_kawahara/articles/20201029-mac-development-settings](https://zenn.dev/sapi_kawahara/articles/20201029-mac-development-settings)


オプションのknownでリリース情報を更新します、が・・・。

```
phpbrew known --update
```
しかしPHP8はでてきません。
そのためinitを実行してから、再びknownでリリース情報を更新します。

```
phpbrew init
phpbrew known --update
```

updateするとPHP8.0.0が出てくるので（2020年11月27日現在）、PHP8.0.0をインストールします。

```
phpbrew install 8.0.0 +default +dbs +curl +openssl=/usr/local/Cellar/openssl@1.1/1.1.1h
```

インストールしたら有効にする。
```
phpbrew switch php-8.0.0
```

バージョン表示します。
```
php -v
```

`PHP 8.0.0`と表示されればOKです。

```
PHP 8.0.0 (cli) (built: Nov 27 2020 18:21:26) ( NTS )
Copyright (c) The PHP Group
Zend Engine v4.0.0-dev, Copyright (c) Zend Technologies
```


それでは楽しいPHP8 LIFEを楽しんでください。
