title: "macOSで開発環境を整える、できるだけコマンドラインだけで"
emoji: "💻"
type: "tech"
topics: ["github", "mac", "zsh"]
published: false

# MacBookを壊した

MacBookを壊したので修理に出した。
そのため、macOSで開発環境を整え直します。
そう、できるだけコマンドラインだけで！

# brew

コマンドラインで何でもやるためにbrewを入れます。
Safariを起動・・・しないでいきます。

```
curl -sS https://brew.sh/index_ja | sed -e 's/<[^>]*>//g' | grep 'curl -fsSL' | sed -e 's/^[ \t]*//' | sed -e 's/^$ //' | bash
```

## 説明

brewのサイトから情報を取得して、sedでHTMLタグの抜いてインストールのところを引っ張りだして実行させてます。

# Homebrew caskについて

Homebrew 2.2ぐらいから、cask関連の初期設定が不要になっているので、いきなりインストールができます。
2020年10月27日現在 Homebrewのバージョンは2.5.7です。
インストールできるアプリはサイトにあるので必要なものをインストールしましょう。
[https://formulae.brew.sh/cask/](https://formulae.brew.sh/cask/)

* Google IME
* Google Chrome
* Slack
* Zoom
* VSCode

これらをコマンドラインからインストールしていきます。

# Google IME

再起動が必要なGoogle IMEを入れます。

```
brew cask install google-japanese-ime
```

システム環境設定から設定を行ってから起動すると再起動を要求されるので再起動します。
なお、既存のIMEを削除するときは、Google IMEの英語入力を追加することを忘れずに行ってください。

# Google Chrome

認証とかでブラウザが必要になるので、Google Chromeを入れます。

```
brew cask install google-chrome
```

起動は以下のコマンドを実行します。
Google Accountなどにログインしておきます。
```
open /Applications/Google\ Chrome.app/
```


# Slack

仕事のやり取りに必須なSlackもcaskにあるのでコマンドラインからインストールします。
ログイン時にブラウザが起動します。

```
brew cask install slack
```

# Zoom

Zoomもcaskにあるのでコマンドラインからインストールします。
zoomusなので注意！
ログイン時にブラウザが起動します。

```
brew cask install zoomus
```

# VSCode

VSCodeもcaskにあるのでコマンドラインからインストールします。

```
brew cask install visual-studio-code
```

## 設定ファイル

設定の同期というのがあるのですが、プレビュー機能で時々動かなくなるので、私は設定ファイルをGitHubにバックアップしてます。

```
~/Library/Application\ Support/Code/User/settings.json
```


curlでさっくと持ってきます。

# その他

Dockerなどもありますが、必要に応じてインストールします。
詳しくはHomebrewのcaskリストを参照してください。
[https://formulae.brew.sh/cask/](https://formulae.brew.sh/cask/)

残りはコマンドライン系です。
快適にするために、どんどん入れていきます。

# git

```
brew install git
```

GitHubにSSH keyの追加をします。
以下の2つを確認しながらやります。

新しい SSH キーを生成して ssh-agent に追加する
[https://docs.github.com/ja/free-pro-team@latest/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent](https://docs.github.com/ja/free-pro-team@latest/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

GitHub アカウントへの新しい SSH キーの追加
[https://docs.github.com/ja/free-pro-team@latest/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account](https://docs.github.com/ja/free-pro-team@latest/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account)

# tmux

brew install tmux






# 個人的に入れたい

```
brew install wget
brew install gzip
brew install jq
brew install nkf
brew tap homebrew/services

brew install unzip
echo 'export PATH="/usr/local/opt/unzip/bin:$PATH"' >> ~/.zshrc

brew install tree

```

# アップデートして入れたい

brew install curl
echo 'export PATH="/usr/local/opt/curl/bin:$PATH"' >> ~/.zshrc

brew install nano


brew install coreutils
echo 'export PATH="/usr/local/opt/coreutils/libexec/gnubin:$PATH"' >> ~/.zshrc

brew install findutils
echo 'export PATH="/usr/local/opt/findutils/libexec/gnubin:$PATH"' >> ~/.zshrc
echo 'export MANPATH="/usr/local/opt/findutils/libexec/gnuman:$MANPATH"' >> ~/.zshrc


brew install gnu-sed
echo 'export PATH="/usr/local/opt/gnu-sed/libexec/gnubin:$PATH"' >> ~/.zshrc
echo 'export MANPATH="/usr/local/opt/gnu-sed/libexec/gnuman:$MANPATH"' >> ~/.zshrc





# 謎


brew install cowsay

brew tap fumiyas/echo-sd

# 開発言語の最新化
## Python
## Ruby
## PHP
## Perl
## Java
## Node.js
# データベースのインストール
## MySQL
## PostgresSQL