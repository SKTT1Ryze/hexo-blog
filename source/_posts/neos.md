---
title: Webバージョン遊戯王ゲームの開発
date: 2023-07-17 12:00:00
tag:
- 日本語
- Web
- ゲーム開発
---

## 遊戯王の紹介
遊戯王とは、元々日本の漫画家高橋和希による作品で、ここでは特にそれを原作としたメディアミックスゲームを指す。
又は、カードゲームの分野に所属し、[KONAMI](https://www.konami.com/ja/)から発売された「遊戯王OCG」は世界中で人気となり、2011年には累計販売枚数**251億7000万枚**を突破、「世界一販売数の多いトレーディング・カードゲーム」として認定されている。

コンピューター及びインターネットの高速発展により、便利性を持つデジタルゲームは求められ、「[遊戯王マスターデュエル](https://www.konami.com/yugioh/masterduel/eu/en/)」と言うKONAMIが開発されるデジタルトレーディングカードゲームは2022年1月19日にリリースした。おかげでプレーヤーは紙のカードを使うわず、パソコンまた携帯電話の上でデュエルを行うことができる。
[Steam](https://store.steampowered.com/)で発売から、同時連続数26万人を突破し、そして2022年2月6日には、ダウンロード回数が1000万回を超えたという発表が出された。

## YGOProとMyCardコミュニティの紹介
「マスターデュエル」はKONAMI会社の公式ゲームとして、中国のプレーヤーにとっていくつかの欠点がある：
- 利益のため商業ゲームであり、プレーヤーは様々な強力なカードを集めるには現金またはゲームコインを使用する必要がある；
- 中国では[グレート・ファイアウォール](https://ja.wikipedia.org/wiki/%E3%82%B0%E3%83%AC%E3%83%BC%E3%83%88%E3%83%BB%E3%83%95%E3%82%A1%E3%82%A4%E3%82%A2%E3%82%A6%E3%82%A9%E3%83%BC%E3%83%AB)の存在により、日本に配備されるゲームサーバーと連続することが難しい。

以上の欠点を解決し、更に中国の遊戯王コミュニティの発展を促進するのは、「YGOPro」のことです。
YGOProは中国の同人プレーヤーから開発され、[GPLv3 ライセンス](https://www.gnu.org/licenses/gpl-3.0.en.html)に準拠したオープンソースゲームです。完全無料で、プレーヤーは自由に友達或いはネットで知らない相手と対戦することができる。

現在[MyCard](https://mycard.moe/)と言う中国最大の遊戯王ファンコミュニティがYGOProの運営や開発を主導し、グッズの販売によってサーバーの料金を維持している。
YGOProに基づく、MyCardは豊富な機能例えば競争試合やダブルモードを提供している。その他、定期的なイベントが行われ、中国のファンたちを楽しませるよう努力をしている。

## Neosの紹介
現在YGOProは[PC](https://ja.wikipedia.org/wiki/%E3%83%91%E3%83%BC%E3%82%BD%E3%83%8A%E3%83%AB%E3%82%B3%E3%83%B3%E3%83%94%E3%83%A5%E3%83%BC%E3%82%BF)と[IOS](https://ja.wikipedia.org/wiki/IOS)と[Android](https://ja.wikipedia.org/wiki/Android_(%E3%82%AA%E3%83%9A%E3%83%AC%E3%83%BC%E3%83%86%E3%82%A3%E3%83%B3%E3%82%B0%E3%82%B7%E3%82%B9%E3%83%86%E3%83%A0)の配信が提供しているが、[Web](https://ja.wikipedia.org/wiki/World_Wide_Web)の配信が提供していない。つまり、プレイヤーはアプリをダウロードし無ければならないので、ブラウザで直接体験することが出来ない。

今では[Discord](https://discord.com/)とか[Telegram](https://telegram.org/)とかほとんどのソフトウェアはWeb版の配信が提供することになり、この点では「YGOProは時代に遅る」そう言う意見も出るかもしれない。

この問題を解決するため、私が2022年10月にWebバージュンのYGOProの開発を開始し、「遊戯王アニメ」の二代目主人公が好きで、彼のエースモンスター「Neos」に名付けられた。
それからほぼ一年が経ち、Neosは重大な成果を上がり、正式なリリースの目標に向かって進んでいる。

## Neosのデザイン
Neosのシステムは全体的に「フロントエンド」と「ベックエンド」と言う二つの部分に分けられることができる。

ベックエンドの務め：
- アカントの管理；
- ゲームの流れのコントロール；
- カードの効果の処理。

フロントエンドの務め：
- ゲーム画面の表示；
- プレーヤーの操作をベックエンドに伝える。

### ベックエンド
YGOProのベックエンドには複数の実装が存在している、例えば、[233](https://ygo233.com/)と[koishi](https://srv.koishi.pro/)。
フロントエンドには「IPアドレス」や「ポート」が分ればベックエンドと[Socket](https://en.wikipedia.org/wiki/Network_socket)また[WebSocket](https://www.geeksforgeeks.org/what-is-web-socket-and-how-it-is-different-from-the-http/)に基づく連続することができる。

これまで遊戯王は千枚以上のカードを発売した、どうやってこのような多数のカーデの効果を正確に処理するのか？
YGOProの開発者は[C++](https://en.wikipedia.org/wiki/C%2B%2B)に基づく[ygopro-core](https://github.com/Fluorohydride/ygopro-core)と言う「カード脚本エンジン」を作り出し、遊戯王カードを[lua](https://www.lua.org/)脚本として処理することになった。[neovim](https://neovim.io/)の設定ファイルのように。

### フロントエンド
Neosは[React](https://react.dev/)と[TypeScript](https://www.typescriptlang.org/)と[CSS](https://en.wikipedia.org/wiki/CSS)に基づく操作画面を構築し、[valtio](https://valtio.pmnd.rs/)を使って状態を管理する。
全体のデザインは以下の画像に示す：
<img src="/images/neos-arch.svg" />

詳しくはこちらへ：https://doc.neos.moe/docs/coding/design

## デモンストレーション
Github: https://github.com/DarkNeos/neos-ts
サイト: https://neos.moecube.com

<img src="/images/duel.png" width="500" />

## コードに貢献する
Welcome to create merge request in [Neos repo](https://code.mycard.moe/mycard/Neos).

