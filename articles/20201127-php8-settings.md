---
title: "PHPBrewでPHP8を入れる"
emoji: "🐘"
type: "tech"
topics: ["PHPBrew", "mac","PHP", "PHP8"]
published: True
---

# PHP8が出た

2020年11月26日にPHP8が正式リリースされました🎉
[https://www.php.net/archive/2020.php#2020-11-26-3](https://www.php.net/archive/2020.php#2020-11-26-3)

色々と変わったPHP8を触ってみたいですよね？PHPBrewならできます。


## PHP8をインストールする

PHPBrewにPHP8.0.0対応版が出ておりました。
[https://github.com/phpbrew/phpbrew/releases/tag/1.27.0](https://github.com/phpbrew/phpbrew/releases/tag/1.27.0)

以前の記事では、PHPBrewでPHPの環境を作っていたので、PHPBrewを使ってみたいと思います。
PHPBrewを使用していない人で、PHPBrewを使いたいと思ったなら、以前の記事をご確認ください。
[https://zenn.dev/sapi_kawahara/articles/20201029-mac-development-settings#php](https://zenn.dev/sapi_kawahara/articles/20201029-mac-development-settings#php)

すでにPHPBrewを使用した場合は、オプションのknownでリリース情報を更新します、が・・・。

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

## JITの検証

デフォルトではJITは有効になっていません。
JITを有効にするには設定ファイルをいじります。
```
~/.phpbrew/php/php-8.0.0/etc/php.ini
```

コメントを外します。
```
zend_extension=opcache
```

0を1に変更します。
```
opcache.enable_cli=1
```

追記します。
```
opcache.jit=on
opcache.jit_buffer_size=100M
```

ベンチを動かしてみます。
[https://github.com/php/php-src/blob/master/Zend/bench.php](https://github.com/php/php-src/blob/master/Zend/bench.php)

```
% php bench.php
simple             0.002
simplecall         0.001
simpleucall        0.001
simpleudcall       0.001
mandel             0.007
mandel2            0.008
ackermann(7)       0.008
ary(50000)         0.004
ary2(50000)        0.005
ary3(2000)         0.008
fibo(30)           0.019
hash1(50000)       0.006
hash2(500)         0.005
heapsort(20000)    0.007
matrix(20)         0.005
nestedloop(12)     0.003
sieve(30)          0.004
strcat(200000)     0.002
------------------------
Total              0.097
```

ちなみにPHP 7.4.13では、こんな感じです。
```
% php bench.php
simple             0.023
simplecall         0.009
simpleucall        0.024
simpleudcall       0.024
mandel             0.086
mandel2            0.099
ackermann(7)       0.025
ary(50000)         0.006
ary2(50000)        0.006
ary3(2000)         0.041
fibo(30)           0.085
hash1(50000)       0.011
hash2(500)         0.007
heapsort(20000)    0.025
matrix(20)         0.022
nestedloop(12)     0.043
sieve(30)          0.013
strcat(200000)     0.004
------------------------
Total              0.553
```

想像以上にPHP8のJITは早いですねー。