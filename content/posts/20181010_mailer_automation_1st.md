---
title: "【前編】GoogleAppScriptで面倒な挨拶メール送信を自動化しよう! "
date: 2018-10-15T16:49:35+09:00
categories: ["自動化"]
tags: ["Google App Script"]
description: "GoogleAppScriptで面倒な挨拶メール送信を自動化しよう"
thumbnail: "images/gmail.png"
---

こんにちは。BizPro運営のmorioです。
記念すべき第一弾の記事では、GoogleAppScriptというプログラミング言語を利用した
メール業務自動化をご紹介しようと思います。

## 所要時間
15分

## できるようになること
クライアントに送信する謹賀新年メールや暑中見舞いメール。多い営業マンは500通~1000通ものメールを送信すると言われています。

この非生産的で嫌気のする業務をプログラムで自動化してしまいましょう。それもただの自動化ではなく、**「人の心を残した自動化」**です。

本章では、
**「クライアントに応じてメッセージを少しアレンジした謹賀新年メールを自動送信する」**
プログラムを一緒に作成していきます。




## 目次
#### 前編(15分)
1. GoogleAppScriptとは?
2. 使い方
3. メールを送信するプログラムを書いてみよう

#### 後編(45分)
4. スプレッドシートから値を取得しよう
5. メールの文面を少しずつ変えてみよう
6. 一斉に送信しよう
7. オススメ書籍


## 1. GoogleAppScriptとは

![Image](https://liginc.co.jp/wp-content/uploads/2013/09/eyecatch5.jpg)

**GoogleAppScript**とは、Googleが提供するさまざまなアプリケーションを自動操作したり連携させるためのプログラミング言語です。

JavaScriptを拡張しているつくられているため、大部分がJavaScriptと共通の文法をもっています。


### ビジネスパーソンが真っ先にGoogleAppScriptを学ぶべき理由
ビジネスパーソンがまっさきに学ぶべきプログラミング言語は間違いなくこの**GoogleAppScript**です。

<br>

#### 1. 目の前の業務をすぐに自動化できる
今流行りのPythonなどは、優れたデータ分析を行えたり、Webアプリケーションを作成するのに極めて便利な言語です。
しかし、この言語を日々の業務に活用できるようになるまでは、少なくとも300時間はかかります。

一方でこのGoogleAppScriptは、Gmailやカレンダー・スプレッドシートなどの処理を自動化することに特化しています。
日々の事務処理を自動化するということについては、もっとも学習効率が良い言語です。例えばgmailの自動化についてであれば2時間ほど学べばあらかた基本的な操作は抑えることができます。

<br>


#### 2. プログラミング環境の構築が必要ない
Ruby, Python、C#, Scala など、皆さんも耳にしたとがある言語は、言語を動かすための設定(環境構築)をPC上で行わねばなりません。
初心者がこの環境構築を行おうとすると、平気で1日や1週間かかることもあります。

しかし、GoogleAppScriptは特殊な言語で、環境構築が必要ありません。Gmailのアカウントとブラウザさえあれば実行することができてしまいます。事前準備がほぼ必要ないという点で、時間のないビジネスパーソンにとって非常に優れた言語なのです。


## 2. 使い方
### Gmailアカウントの用意
まずはGmailアカウントを用意しましょう。


{{<figure src="/images/gmail.png" width="100" height="100">}}

### スプレッドシートの作成

#### 1. 以下のリンクを開いて、新しいスプレッドシートを作成しましょう。

[GoogleSpreadSheet](https://www.google.com/sheets/about/)

#### 2. 新しいシートを作成しましょう
[![Image from Gyazo](https://i.gyazo.com/cc21700462537dbd3e171efba17c8432.png)](https://gyazo.com/cc21700462537dbd3e171efba17c8432)

このようなシートが作成されます。

[![Image from Gyazo](https://i.gyazo.com/bd1e73111c01bd24cb9269a1cd77d56c.png)](https://gyazo.com/bd1e73111c01bd24cb9269a1cd77d56c)

※使用したことがない方に補足として一言で説明すると、GoogleSpreadSheetとはWeb上で他者と共有できるExcelです。


### スクリプトエディタの起動
つづいてGmailを自動操作するプログラムをかくための、**スクリプトエディタ**を開きましょう。

[![Image from Gyazo](https://i.gyazo.com/02f8baf869803614ce1166702fd410af.png)](https://gyazo.com/02f8baf869803614ce1166702fd410af)

<br>

以下のような、GoogleAppScriptを書き実行するためのエディタがでてきます。

[![Image from Gyazo](https://i.gyazo.com/3cd2817fbedfce04e6f9e06076173f0d.png)](https://gyazo.com/3cd2817fbedfce04e6f9e06076173f0d)

<br>

この上でGoogleAppScriptを書いていくことで、さまざまな事務作業を自動化していくことが可能になります。
またGoogleAppScriptを深く理解し、使いこなすためにはこの言語の基となっている**JavaScript**の理解が必要です。

本記事では、とにかくプログラムを動かすことを重視して、基礎的な文法には意図的に触れません。
**JavaScript**の基礎文法をもっと学習したい方向けに、別の記事をご用意しますので請うご期待。



## 3. メールを送信するプログラムをかいてみよう
エディタの準備が完了したところで、メールを送信するプログラムを書いてみましょう。

※【注意】本記事を参考にプログラムを書くにあたって、「理解を深める」よりも**「とにかく動かす」**ことを重視してください。細かな文法の理解などは、別記事にて深められるようにします。


### 関数(処理のかたまり)を定義しよう
まずは関数を定義してみましょう。
エディタ内のコードを以下のように書き換えましょう。

``` gas.js
function sendMail() {
  Logger.log('HelloWorld')
}
```

順を追って説明をしていきます。

<br>

#### 関数
関数とはJavaScriptにおける処理を1つにまとめて、その処理に名前をつけるためのものです。
以下のような形で記載します。

```
funciton 関数名() {
  処理の中身
}
```

()は引数というものになりますが、ここでは説明を割愛します。

<br>

#### Logger.log
GoogleAppScript独自の文法でLog(コード実行の記録)を取得・表示するために使用します。
コードの途中で値を確認したり、バグの原因をさぐるために使用します。

コードの実行後に以下のキーを押すとLogを確認することができます。

Mac|Windows
:---|:---
Command + Enterキー| Ctrl + Enterキー

<br>



### 関数を実行しよう
つづいて上記で定義した関数を実行します。実行方法は非常に簡単です。

1. エディタ上のタブから、関数名を選択(sendMail)
2. 隣の関数実行ボタン(▶)をクリック
3. ログを確認( Command + Enter | Ctrl + Enter )

以下の動画も参考にして実行してみましょう。
"ログ"画面でHelloWorldという文字が確認できれば、関数の実行は完了です。

[![Image from Gyazo](https://i.gyazo.com/e937ed8f2408d9536c81215c81a770fb.gif)](https://gyazo.com/e937ed8f2408d9536c81215c81a770fb)


### メールを送信してみよう
前編の最後に、メールをGoogleAppScriptから送信して終了としましょう。
メールを送信するためには、関数の中身を以下のように書き換える必要があります。

``` gas.js

function sendMail() {
  MailApp.sendEmail({
    to: 'hoge@hoge.com',
    subject: 'こんにちは',
    body: 'こんにちは。私の名前はmorimoriです'
  })
}

```

hoge@hoge.comの部分には送り先のアドレスを指定しましょう。
まずは先程と同様にこの**sendMailという関数を実行してみましょう**。

関数の実行方法は

1. エディタ上のタブから、関数名を選択(sendMail)
2. 隣の関数実行ボタン(▶)をクリック
3. ログを確認( Command + Enter | Ctrl + Enter )

でしたね！

<br>

[![Image from Gyazo](https://i.gyazo.com/dbea3c61d666aba1119bc535c706f262.png)](https://gyazo.com/dbea3c61d666aba1119bc535c706f262)

いかがでしたでしょうか? ↑のようなメールは送られてきましたか？
では、細かい説明をしていきたいと思います。

### MailApp.sendEmail()
これはGoogleAppScriptが用意してくれている、独自の関数です。
Gmailにアクセスすることができメールを送信できます。

公式のリファレンスにも様々な使い方が記載されています。(読むのが少々難しいので、軽く目を通すくらいで構いません)
https://developers.google.com/apps-script/reference/mail/mail-app

<br>

MailApp.sendEmail()は()の中にオプションを与えることでメールを送信できます。
そのオプションの中で主に使用するものは、to, subject, bodyの3つです。
※初学者への配慮でオプションと表現していますが厳密にはJavaScriptのオブジェクトというものを与えています。

``` gas.js
MailApp.sendEmail({
  to:      送り先のアドレス,
  subject: 件名,
  body:    本文
})
```

上記のリファレンスにも似たようなコードが載っていますね！
英語で読むのは骨が折れますが、このような公式のリファレンスを読むことができるようになると自在にGoogleAppScriptを操ることができるようになります。

[![Image from Gyazo](https://i.gyazo.com/d8a1375b409649eb274a463ba1413f76.png)](https://gyazo.com/d8a1375b409649eb274a463ba1413f76)


## お疲れさまでした！
前編はこれにて終了です！いかがでしたでしょうか?
これだけ簡単にプログラミングができ、普段利用しているGmailを動かすことができるGoogleAppScriptの可能性を感じていただけたのではないかと思います。

後編では、より実践的なプログラムを書いていきますので、このままの勢いで下記のリンクへ飛んでプログラムを書いていきましょう！


