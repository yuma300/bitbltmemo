---
title: Daocasinoとは
date: 2019-01-07 15:53:38
tags: daocasino
---

Ethereum上で動作するギャンブル用プロトコル[daocasino](https://dao.casino/)の説明をします。

# トークンについて
DaocasinoのプロトコルではBETというトークンが使われます。
このトークンは2017年7月に行われたICOにより発行されました。
ICO時のトークン価格は1ETH=2000BETで当時の1ETHの価格が30000円くらいなので1BET=15円くらいでした。
トークンの総発行量は167,270,821BETです。
現在このトークンが買えるのは[hitbtc](https://hitbtc.com/exchange/BET-to-ETH)のみです
このトークンがどのように使われるかについては後述の`仕組み`をご覧下さい。

# 諸情報

[ホームページ](https://dao.casino/)

[リポジトリ](https://github.com/DaoCasino)


[ホワイトペーパー](https://github.com/DaoCasino/Whitepaper/blob/master/DAO.Casino%20WP.md)

[twitterアカウント](https://twitter.com/daocasino)

# 紹介動画
{% youtube 7pTZW3Jv5z8 %}

# 仕組み

Daocasinoでは5つの役割が存在します。 `Operators`, `Bankrollers`, `Game Developers`, `Affiliators`, `Game Players` です。

{% plantuml %}
title <size:18>Daocasinoの仕組みのイメージ図</size>
package "Casino" {
component [Operators] as op
component [Bankrollers] as br
component [Game Players] as gp
gp --> op : 賭けをする
op ..> br : 報酬
op --> br : 賭けを受けてもらう
}
component [Game Developers] as gd
component [Affiliators] as af
gd -> op : ゲーム提供
op -left.> gd : 報酬
af -> gp : 賭けに誘導
op .> af : 報酬
{% endplantuml %}

Gampe DevelopersはDaocasinoが提供する[SDK](https://github.com/DaoCasino/dc-sdk-example)を用いてdaocasinoプロトコル用のゲームを作ります。

OperatorsはGame Developersが作ったゲームをホスティングしてwebページを用意します。これはまさにオンラインカジノです。

Game PlayersはOperatorsが用意したwebページにアクセスしプレイしたいゲームをプレイ（賭けを）します。

BankrollersはGame Playersの賭けを引き受けます。普通プレイヤーの賭けを受けるのはカジノの運営者つまりこの場合Operatorsのように思われますが、daocasinoではこのBankrollersが引き受けます。
Game Players側が高額な賭けをしたい場合、受ける側もかなりの額を用意しておかないといけませんがOperatorsは用意する必要はなくbankrollersが用意します。

AffiliatorsはOperatorsが運営するwebページに客となるGame Playersを呼び込みます。

テラ銭の一部がBankrollers, Game developers, Affiliatorsに報酬として流れます。

Daocasino自体は非中央主権なプロトコルなので誰でも自由に上記の役割に誰でもなれます。

BETはGame Playersが賭けたりBankrollersが賭けを受けたりBankrollers,Game Developers,Affiliatorsが報酬を受けるのに使われます。
