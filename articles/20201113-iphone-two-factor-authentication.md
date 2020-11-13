---
title: "2段階認証に使用しているiPhoneの機種変更"
emoji: "📱"
type: "tech"
topics: ["スマートフォン", "iPhone", "2段階認証"]
published: false
---

# 秋の風物詩

毎年、秋ぐらいになるとiPhoneは新機種が発売されます。
エンジニアなら、スマートフォンは2段階認証アプリが入っているので、ちゃんと機種変更したいですね。

有名なところだと「Google Authenticator」です。
[https://apps.apple.com/jp/app/google-authenticator/id388497605](https://apps.apple.com/jp/app/google-authenticator/id388497605)


それとiCloudにバックアップできる「Microsoft Authenticator」などが便利ですね。
[https://apps.apple.com/app/id983156458](https://apps.apple.com/app/id983156458)

今回は「Microsoft Authenticator」を使用してiPhoneの機種変更をしていきたいと思います。


# 準備作業
それでは機種変更する前の作業を行います。
前提条件として、同一Apple IDで同一電話番号で、機種変更するケースとして記載ます。

## データの削減
[設定] - [一般] - [iPhoneストレージ] で、サイズが大きなのは削除していきます。
LINEやSafariなどはキャッシュを消しておくとサイズが小さくなります。

LINEが重い…キャッシュの蓄積が原因かも！ キャッシュを削除する方法
[http://official-blog.line.me/ja/archives/72213176.html](http://official-blog.line.me/ja/archives/72213176.html)

## 各種アプリの移行
同じユーザーで複数のスマートフォンにて起動を抑止しているアプリの移行をしないといけません。

クラウド移行できるものは、それの指示に従っておきます。
例えばドラクエウォークなどは「スクウェア・エニックスアカウント（SQUARE ENIX ACCOUNT）」を設定しておきます。

データの引き継ぎで移行する物は、機種変更する前にデータ引き継ぎを行っておきます。

PIN CODE移行するのならメモを取っておきます。

### ウォレット

SuicaやPASMOなどのウォレットアプリも同じユーザーで複数のスマートフォンにて起動を抑止をしています。
ウォレットからSuicaとPASMOを削除しておきます。

* Suica
【機種変更】iPhone／Apple Watchから、別のiPhone／Apple Watchへ。
[http://appsuica.okbiz.okwave.jp/faq/show/1537](http://appsuica.okbiz.okwave.jp/faq/show/1537)

* PASMO
iPhone／Apple Watchから、別のiPhone／Apple Watchへの機種変更にともない、PASMOを移行したい。
[https://support.mobile.pasmo.jp/faq/show/622](https://support.mobile.pasmo.jp/faq/show/622)


クレジットカードは移行前のiPhoneでも使用可能ですが削除することを推奨します。

### LINE

LINEは面倒ですが手順を確認しながら進めます。
[https://guide.line.me/ja/migration/](https://guide.line.me/ja/migration/)

* 電話番号とメールアドレスを登録する。
* トークをバックアップする。
* [アカウント引き継ぎ設定]をオンにする。


## バックアップ
パソコンがあればiTunesでバックアップが取れます。
その際に、端末の自動同期をオフにしておくことが重要です。

iCloudに余裕がある方はiCloudにバックアップするのも良いでしょう。
[設定] - [Apple ID] - [iCloud] - [iCloudバックアップ]から、今すぐバックアップを作成をタップします。


## Microsoft Authenticator
Microsoft AuthenticatorはiCloud経由でバックアップします。
[ハンバーガーメニュー] - [設定]でiCloudバックアップがオンになっていれば移行できます。

