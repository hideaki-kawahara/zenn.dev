---
title: "macOS Catalinaで開発環境を整える"
emoji: "💻"
type: "tech"
topics: ["github", "mac", "zsh", "Catalina"]
published: true
---

# MacBookを壊した

MacBookを壊したので修理に出した。
そのため、macOSで開発環境を整え直します。
もうすぐmacOS Big Surが出てしまうので（記載日2020年11月6日）、Catalinaでの対応方法を記載しておきます。

2020年11月18日更新しました。
巻末にmacOS Big Surに関する記述を追記しました。
※Apple Silicon M1ではなく、Intel CPUでの動作確認です。

## 設定変更

* システム環境設定で以下を変更する。
  * 英語キーボードなので、caps lockをControl keyに変更します。
  * Dockで、最近使ったアプリケーションをDockに表示を無効にする。
  * Spotlightのキーボードショートカットを無効にする。
* 使わないけどファインダーですべてのファイルを表示にしておく。（コマンドラインで以下を入力する）
* スクリーンショットの余白を消す。（コマンドラインで以下を入力する）

ファイル表示
```
defaults write com.apple.finder AppleShowAllFiles TRUE
killall Finder
```

余白除去
```
defaults write com.apple.screencapture disable-shadow -boolean true
killall SystemUIServer
```

## brew

コマンドラインで何でもやるためにbrewを入れます。
Safariを起動・・・しないでいきます。

```
curl -sS https://brew.sh/index_ja | sed -e 's/<[^>]*>//g' | grep 'curl -fsSL' | sed -e 's/^[ \t]*//' | sed -e 's/^$ //' | bash
```

### 説明

brewのサイトから情報を取得して、sedでHTMLタグの抜いてインストールのところを引っ張りだして実行させてます。

## Homebrew caskについて

GUIアプリをコマンドでインストールするものです。
インストールできるアプリはサイトにあるので必要なものをインストールしましょう。
[https://formulae.brew.sh/cask/](https://formulae.brew.sh/cask/)

とりあえず以下のものを、これらをコマンドラインからインストールします。

* Google IME
* Google Chrome
* Slack
* Zoom
* VS Code
* Docker
* iTerm2
* Intel Power Gadget

## Google IME

再起動が必要なGoogle IMEを入れます。

```
brew install --cask google-japanese-ime
```

システム環境設定から設定を行ってから起動すると再起動を要求されるので再起動します。
なお、既存のIMEを削除するときは、Google IMEの英語入力を追加することを忘れずに行ってください。

## Google Chrome

認証とかでブラウザが必要になるので、Google Chromeを入れます。
これでSafariを起動せずにChromeを入れることができます。

```
brew install --cask google-chrome
```

起動は以下のコマンドを実行します。
Google Accountなどにログインしておきます。
```
open /Applications/Google\ Chrome.app/
```
起動後はデフォルトブラウザをChromeに変更しておきます。

## Slack

仕事のやり取りに必須なSlackもcaskにあるのでコマンドラインからインストールします。
ログイン時にブラウザが起動します。

```
brew install --cask slack
```

## Zoom

Zoomもcaskにあるのでコマンドラインからインストールします。
~~zoomusなので注意！~~
**2020年11月29日よりzoomusからzoomに変更されました**。
ログイン時にブラウザが起動します。

```
brew install --cask zoom
```

zoomusでインストールしているときは、一度アンインストールしてください。
```
brew uninstall zoomus
brew install --cask zoom
```


## VSCode

VSCodeもcaskにあるのでコマンドラインからインストールします。

```
brew install --cask visual-studio-code
```

### 設定ファイル

設定の同期というのがあるのですが、プレビュー機能らしく動かなくなることがあります。
そのため、設定ファイルをCloudに置いてあるので、curlでさっくと持ってきて、以下の場所に入れます。

```
~/Library/Application\ Support/Code/User/settings.json
```


## Docker

```
brew install docker
brew install --cask docker
brew install docker-machine
```

## iTerm2

```
brew install --cask iterm2
```

見やすい色に変更します。

## Intel Power Gadget
```
brew install --cask intel-power-gadget
```

再起動してくれと言われたら再起動します。

## tmux

ここからコマンドライン関連です。

```
brew install tmux
```
設定ファイルをCloudに置いてあるので、curlでさっくと持ってきて、以下の場所に入れます。
もしくは検索して入れます。

```
~/.tmux.conf
```

自動起動は以下のSolution 6を参照しました。

[https://qiita.com/ssh0/items/a9956a74bff8254a606a](https://qiita.com/ssh0/items/a9956a74bff8254a606a)


## git

```
brew install git
```

初期設定は以下のようにしておきます。
Default brunchはmainにしておきます。
```
git config --global user.name "名前"
git config --global user.email メールアドレス
git config --global init.defaultBranch main
```

次にSSH Keyを作り、GitHubに登録します。
以下の2つを確認しながらやります。

新しい SSH キーを生成して ssh-agent に追加する
[https://docs.github.com/ja/free-pro-team@latest/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent](https://docs.github.com/ja/free-pro-team@latest/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

GitHub アカウントへの新しい SSH キーの追加
[https://docs.github.com/ja/free-pro-team@latest/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account](https://docs.github.com/ja/free-pro-team@latest/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account)

## 個人的に入れたい

```
brew install wget
brew install gzip
brew install jq
brew install nkf
brew install unzip
brew install tree
```

インストール後~/.zshrcに以下の設定を入れる。

```
export PATH="/usr/local/opt/unzip/bin:$PATH"
```

## アップデートして入れたい

```
brew install curl
brew install nano
brew install coreutils
brew install findutils
brew install gnu-sed
```

インストール後~/.zshrcに以下の設定を入れる。

```
export PATH="/usr/local/opt/curl/bin:$PATH"
export PATH="/usr/local/opt/coreutils/libexec/gnubin:$PATH"
export PATH="/usr/local/opt/findutils/libexec/gnubin:$PATH"
export MANPATH="/usr/local/opt/findutils/libexec/gnuman:$MANPATH"
export PATH="/usr/local/opt/gnu-sed/libexec/gnubin:$PATH"
export MANPATH="/usr/local/opt/gnu-sed/libexec/gnuman:$MANPATH"
```

## 開発言語やデータベースで必要になるので入れる

```
brew install autoconf
brew install openssl
brew install readline
brew install sqlite
brew install automake
brew install libxml2
brew install mcrypt
brew install mhash
brew install pcre
brew install zlib
brew install bzip2
brew install libzip
brew install icu4c
brew install krb5
```

インストール後~/.zshrcに以下の設定を入れる。
```
export PATH="/usr/local/opt/sqlite/bin:$PATH"
export PATH="/usr/local/opt/libxml2/bin:$PATH"
export PATH="/usr/local/opt/bzip2/bin:$PATH"
export PATH="/usr/local/opt/icu4c/bin:$PATH"
export PATH="/usr/local/opt/icu4c/sbin:$PATH"
export PATH="/usr/local/opt/krb5/bin:$PATH"
export PATH="/usr/local/opt/krb5/sbin:$PATH"
export PATH="/usr/local/opt/openssl@1.1/bin:$PATH"
export LDFLAGS="-L/usr/local/opt/openssl@1.1/lib"
export CPPFLAGS="-I/usr/local/opt/openssl@1.1/include"
```

libxml2を入れると、brewがPython3を入れてしまうんだよな。
Pythonはpyenvで管理したいんだけどね・・・。

## 謎

```
brew install cowsay
brew tap fumiyas/echo-sd
brew install echo-sd
```

## PostgresSQL

ここから開発言語やデータベースなどを入れていきます。


```
brew install postgresql
```

データベース起動は開発時に行うのでインストールだけします。
インストールしておかないと、PHPなどがインストール時にエラーが発生するので入れておきます。

13.0が入りました。
$ postgres --version
postgres (PostgreSQL) 13.0

## MySQL

```
brew install mysql
```

8.0.22が入りました。
$ mysql --version
mysql  Ver 8.0.22 for osx10.15 on x86_64 (Homebrew)

データベース起動は開発時に行うのでインストールだけします。

## Python

pyenvを入れて最新バージョンを入れる。
（brew doctorでのWarningが出るが無視）

```
brew install pyenv
pyenv install --list | grep -v '[a-z]'
pyenv install 最新版
pyenv versions
```

tumxを起動しているとpyenvが切り替わらないので
~/.zshrcのtumx起動後にpyenv initを入れる。

```
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
if command -v pyenv 1>/dev/null 2>&1; then
  eval "$(pyenv init -)"
fi
```

参考
[https://shunsuke.me/ja/tech/how-to-setup-dev-env-on-macos/#pyenv](https://shunsuke.me/ja/tech/how-to-setup-dev-env-on-macos/#pyenv)

フレームワークは適宜入れる。

## Ruby

rbenvを入れて最新バージョンを入れる。

```
brew install rbenv
rbenv install --list
rbenv install 最新版
rbenv global 最新版
```

インストール後~/.zshrcに以下の設定を入れる。
```
eval "$(rbenv init -)"
export RUBY_CONFIGURE_OPTS="--with-openssl-dir=$(brew --prefix openssl@1.1)"
```

フレームワークは適宜入れる。


## PHP

事前にPHPが使用する物を入れておく。
先にpearを入れないとコンフィグレーションができないので下記を参考にpearを入れておく。

[https://qiita.com/applexco/items/f10e87477dc5d41cf751](https://qiita.com/applexco/items/f10e87477dc5d41cf751)

インストール後~/.zshrcに以下の設定を入れる。

```
export PATH="/Users/ユーザー名/pear/bin:$PATH"
```

以下を参考にしてPHPBrewを入れる。

[https://github.com/phpbrew/phpbrew/blob/master/README.ja.md](https://github.com/phpbrew/phpbrew/blob/master/README.ja.md)

Defaultのvariantsにデータベースなどを追加して入れます。
2020年11月1日現在openssl@1.1でした。

```
phpbrew install 最新版 +default +dbs +curl +openssl=/usr/local/Cellar/openssl@1.1/1.1.1h
```

インストールしたら有効にする。
```
phpbrew switch 最新版
```

フレームワークは適宜入れる。


## Perl

perlbrewを入れて最新バージョンを入れる。

```
curl -L http://xrl.us/perlbrewinstall | bash
```
インストール後~/.zshrcに以下の設定を入れる。

```
source ~/perl5/perlbrew/etc/bashrc
```

最新版を入れる。
--notestを入れないと物凄く遅いです。

```
perlbrew init
perlbrew install-patchperl
perlbrew available
perlbrew install --notest perl-最新版
perlbrew switch perl-最新版
```

## Node.js
2021年2月14日更新：brewで入るnode-build(4.9.29)がgccを要求して、gccはXcode Command Line Tool(CLT)を要求してくるので、この章では、この方法が使用できません。

nodenvで入れます。
```
brew install nodenv
nodenv init
```

インストール後~/.zshrcに以下の設定を入れる。
```
eval "$(nodenv init -)"
```

nodenv-yarn-installをインストールする。
```
mkdir -p "$(nodenv root)/plugins"
git clone https://github.com/pine/nodenv-yarn-install.git "$(nodenv root)/plugins/nodenv-yarn-install"
```

インストールしたいバージョンを確認します。（すごい量が出る）
```
nodenv install --list
```

最新版を入れます。
```
nodenv install 最新版
nodenv rehash
nodenv global 最新版
```

node-buildも自動的に入ります。

次に確認コマンドです。
OKが出れば良いです。

```
curl -fsSL https://github.com/nodenv/nodenv-installer/raw/master/bin/nodenv-doctor | bash
```

バージョン確認です。
```
node -v
yarn -v
npx -v
npm -v
```

## 終わりに
macOS Catalinaになってから、XcodeやXCode Command Line Tools(CLT)などを入れなくても、brewを入れることができるようになり、初期設定の時間が少しだけ短縮できるようになりました。

残念ながら、node-build(4.9.29)からはgccが必須になり、その影響でXCode Command Line Tools(CLT)が必須になりました。

今後、macOS Big SurやApple Silicon Macになったとき、どんな感じで環境構築が変わるのだろうか？楽しみです。


## macOS Big Sur

### Docker
Version 2.5.0.1(49550)で問題なく動作しております。

