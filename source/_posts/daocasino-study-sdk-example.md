---
title: Daocasino SDKのモジュール調査
date: 2019-01-14 00:39:31
tags: Daocasino
---

[DaocasinoのSDK exampleを動かしてみた](/bitbltmemo/2019/01/08/daocasino-sdk-example/)でDaocasino SDKのexampleを動かしてみました。
今回の記事ではDaocasino SDKがどのようなモジュール構成になっていてモジュール間でどのようなやりとりをしているのか調査結果を書きます。


{% plantuml %}
title <size:18>Daocasinoのモジュール構成</size>
component [ipfs] as ip
component [ethereum network] as net


package "Player Side" {
component [game application] as app1
component [dc-webapi] as dcweb1 <<sdk>>
component [dc-core] as dccore1 <<sdk>>
component [dc-ethereum-utils] as dceth1 <<sdk>>
component [dc-messaging] as dcmes1 <<sdk>>
Player -> app1
app1 -> dcweb1
dcweb1 -> dccore1
dccore1 -> dceth1
dccore1 --> dcmes1
}

dceth1 -> net
dcmes1 -> ip

package "Bankroller Side" {
component [game application] as app2
component [dc-webapi] as dcweb2 <<sdk>>
component [dc-core] as dccore2 <<sdk>>
component [dc-ethereum-utils] as dceth2 <<sdk>>
component [dc-messaging] as dcmes2 <<sdk>>
app2 <- Bankroller
dcweb2 <- app2
dccore2 <- dcweb2
dceth2 <- dccore2
dcmes2 <-up- dccore2
}

net <- dceth2
ip <- dcmes2
{% endplantuml %}


# 各モジュール説明

## PlayerとBankroller
これはモジュールではなくて[Daocasinoとは](/bitbltmemo/2019/01/07/what-is-daocasino/)で説明したGame PlayersとBankrollerです。


## game application
これはゲームのロジック部分です。自分でなにかDaocasino用ゲームを作る場合はこの部分を用意することになります。
Daocasino SDKのexampleにおいては、tutorial.jsがこれにあたります。



## dc-webapi
Daocasino SDKを構成する一つです。
Daocasinoプロトコルのインタフェースが用意されています。
game applicationからこのdc-webapiが用意したインタフェースを実行していくことでDaocasino用のゲームとして動作します。

## dc-core
Daocasino SDKを構成する一つです。
ゲームの結果部分の処理を行います。
ゲームの結果部分とは具体的には、どういうランダムナンバーを生成してPlayerの選択と照らし合わせてPlayerかBankrollerどちらが勝ちなのか判定してその結果PlayerとBankrollerそれぞれの残高がどうなったのか計算します。
この処理結果はブロックチェーンには書き込まれずstate channel上で保持されます。

ゲームの結果部分はPlayer側Bankroller側両方同じロジックで同じタイミングで処理されます。もじどちらかが不正をした場合、当然同じ結果になりません。その場合、はdisuputeというモードに切り替わりどちらが不正しているのかの検証が行われます。

Player側がこれ以上ゲームを続行する意思がなくゲーム終了となった場合はstate chunnelが閉じられて初めてブロックチェーンにお互いの残高が記録されます。

## dc-ethereum-utils
Daocasino SDKを構成する一つです。
Ethereumのブロックチェーンにアクセスしてなにかやるときのいろいろな処理をまとめた便利ライブラリです。
ランダムナンバーを生成したり、state channelを閉じて結果をブロックチェーンに書き込むときに使われます。


## dc-messaging
Daocasino SDKを構成する一つです。
ゲームの結果部分の処理を含めてPlayer側とBankroller側は通信する必要があります。お互いweb socketで通信するのですが、その際IPFSのPubSub機能をつかってweb socketでの双方向リアルタイム通信を実現しています。


## Ethereum network
Etheruemブロックチェーンのことです。ランダムナンバーの生成やゲーム終了時点でのPlayerとbankrollerの残高が保存されます。

## IPFS
PlayerとBankroller間のwebsocket通信を実現するためにこのIPFSのPubSub機能が使われます。

