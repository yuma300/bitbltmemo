---
title: Augurマーケット「2019年3月23日に行われるF1オーストラリアGPの優勝チームは？」を作ってみた
date: 2018-12-30 17:07:05
tags: Augur
---


[Augurマーケット「2018年中にETHのレートは500ドルを超える？」に参加してみた](https://yuma300.github.io/bitbltmemo/2018/12/20/augur-try-betting/) にて、実際にマーケットに参加してみました。
今度は自分でマーケットを作ってみました。

Augurの画面の左側にある `create` ボタンを押します。

まずは作ろうとするマーケットのタイトルとカテゴリを決めます

![](/bitbltmemo/images/augur/augur_create1.png)

マーケットの詳細や選択肢を用意します。

![](/bitbltmemo/images/augur/augur_create2.png)

マーケットの締切日やどのように結果を確定させるかの方法を定義します。

![](/bitbltmemo/images/augur/augur_create3.png)

ここで誰も何も賭けてない初期状態においても初めて賭けるひとが配当をもらえるようにするための注文を入れます。
Initial Liquidityと呼ばれるようで、どうやらこの注文はこのマーケット作った人以外は見れないようです。

![](/bitbltmemo/images/augur/augur_create4.png)

ここでマーケット作成に必要なコストや内容の確認画面です。結構かかるなあという感じですが、これでスパムを防げるという側面もあるのでしょう。

![](/bitbltmemo/images/augur/augur_create5.png)

最後にmetamaskで支払います。
0.014628ETHはvalidity bondで表示されていたコストでしょう。Gas代が0.023866ETHもかかります。
当然4.5423REPもかかります。

![](/bitbltmemo/images/augur/augur_create6.png)

実際に出来上がったマーケットがこちらです。

[Which team will win the F1 Australian Grand Prix 2019 March 23](https://cloudflare-ipfs.com/ipfs/QmRMugnaQg8LFdiKSQb5CGcHhVarUqpt4TXVc4ggAcjb3q/?augur_node=wss%3a%2f%2faugur-node.augur.casino&ethereum_node_ws=wss%3a%2f%2fgethnode.com%2fws#/market?id=0xb5849823fa84949493278cccf17846d875c86f38)

2019年3月23日に行われるF1 オーストラリアGPの優勝チームを当てるマーケットです。
興味がありましたら試しに参加してみてくれるとありがたいです。


Initial Liquidityとその後の配当の計算式とかvalidity bondとかno show bondとか今の所謎です。
今後その辺を調べていきたいなと思います。

