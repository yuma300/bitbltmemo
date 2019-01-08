---
title: DaocasinoのSDK exampleを動かしてみた
date: 2019-01-08 00:45:37
tags: daocasino
---

[Daocasinoとは](/bitbltmemo/2019/01/07/what-is-daocasino/)でDaocasinoがどのようなものかについて説明しました。
Daocasinoでは誰でもDaocasinoの[SDK]()を使ってGame Developersになれます。

今回の記事はこのSDKのexampleを実際に動かしたいと思います。

exampleの動かし方の動画もあり、これの通りにやるだけです。

# Daocasino SDK example動画
{% youtube x5oZr3hhu_k %}


# 手順

npm や nodeが既にインストールされているものとします。

## dc-cliのインストール

daocasino開発に必要な各種ツール、サーバーを簡単に使えるようにするコマンド `dc-cli` をインストールします。

```
$ npm i -g dc-cli
```


## プロジェクト作成

下記コマンドを実行することで生成されたディレクトリにSDKのライブラリや各種設定が用意されます。

```
$ dc-cli create daocasino/dc-sdk-example ./myDapp
$ cd myDapp
```

## ローカル上でイーサリアムVM起動&コントラクトデプロイ

ローカル上でイーサリアムのVMを起動し、bankrollerを動かすためのコントラクトをデプロイします。

```
$ dc-cli start
? Use docker container for up environment No
```


## ローカル上でwebサーバー起動

ゲームのフロントエンドをホスティングするwebサーバーをローカル上で起動します

```
$ npm run start
```


## ローカルのwebサーバーにアクセスしてゲームを試す

`npm run start` でエラーが出てなければブラウザで`http://localhost:3000`にアクセスします。


下のwizard画面が表示されるので`start`を押します。

![](/bitbltmemo/images/daocasino/daocasino-sdk-example1.png)

`local` を選択して`INIT ACCOUNT`を押します。 `platform_id`はローカルマシンのユーザー名が自動的に入ってきます。

![](/bitbltmemo/images/daocasino/daocasino-sdk-example5.png)

`INIT DAPP` を押します。

![](/bitbltmemo/images/daocasino/daocasino-sdk-example6.png)

`FIND BANKROLLER AND CONNECT` を押します

![](/bitbltmemo/images/daocasino/daocasino-sdk-example7.png)

ローカルで動いているBankrollerに接続します

![](/bitbltmemo/images/daocasino/daocasino-sdk-example3.png)

接続が完了するとゲーム画面が表示されます。1,2,3のどの目が出るか賭けます。

![](/bitbltmemo/images/daocasino/daocasino-sdk-example2.png)

4回やってみました。balanceの列でGameplayerとbankrollerの残高がわかります。
ちなみに、買ったら2貰えて負けたら1失うようです。期待値0.75なので長くやると間違いなく負けますねw

![](/bitbltmemo/images/daocasino/daocasino-sdk-example4.png)


# 動かしてみて思ったこと
とりあえずexampleを動かすのはめっちゃ簡単でした10分もあれば試せます。
実際にゲームをプレイしてみると、期待通りにstate channelが動いているように思われます。
state channelとはEthereumのブロックチェーンに書き込む頻度を減らして手数料や待ち時間を無くすための仕組みです。
賭ける度にブロックチェーンに書き込みが行われて手数料や待ち時間が発生していたのでは非常にストレスがあります。
このstate channelがまともに機能するかどうかがDaocasinoの成否の大きな要因の一つになるのは間違いないでしょう。



