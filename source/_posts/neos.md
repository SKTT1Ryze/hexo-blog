---
title: Webバージョン遊戯王ゲームの開発
date: 2023-07-27 12:00:00
tag:
- 日本語
- Web
- ゲーム開発
---

## 遊戯王の紹介
遊戯王とは、元々日本の漫画家高橋和希による作品で、ここでは特にそれを原作としたメディアミックスゲームを指す。
又は、カードゲームの分野に所属し、[KONAMI](https://www.konami.com/ja/)から発売された「遊戯王OCG」は世界中で人気となり、2011年には累計販売枚数**251億7000万枚**を突破、「世界一販売数の多いトレーディング・カードゲーム」として認定されている。

コンピューター及びインターネットの高速発展により、利便性を持つデジタルゲームは求められ、「[遊戯王マスターデュエル](https://www.konami.om/yugioh/masterduel/eu/en/)」というKONAMIが開発されたデジタルトレーディングカードゲームは2022年1月19日にリリースされた。おかげでプレーヤーは紙のカードを使うわず、パソコンまた携帯電話の上でデュエルを行うことができるようになった。
[Steam](https://store.steampowered.com/)で発売してから、同時接続数26万人を突破し、そして2022年2月6日には、ダウンロード回数が1000万回を超えたという発表がある。

## YGOProとMyCardコミュニティーの紹介
「マスターデュエル」はKONAMI会社の公式ゲームとして、中国のプレーヤーにとって二つの欠点がある：
- 利益を求める商業ゲームであり、プレーヤーは様々な強力なカードを集めるには現金またはゲームコインを使用する必要がある；
- 中国では[グレート・ファイアウォール](https://ja.wikipedia.org/wiki/%E3%82%B0%E3%83%AC%E3%83%BC%E3%83%88%E3%83%BB%E3%83%95%E3%82%A1%E3%82%A4%E3%82%A2%E3%82%A6%E3%82%A9%E3%83%BC%E3%83%AB)の存在により、日本に配備されてあるゲームサーバーと接続することが難しい。

以上の欠点を解決し、更に中国の遊戯王コミュニティーの発展を促進したのは、「YGOPro」のことです。
YGOProは中国の同人プレーヤーから開発され、[GPLv3 ライセンス](https://www.gnu.org/licenses/gpl-3.0.en.html)に準拠したオープンソースゲームです。完全無料で、プレーヤーは自由に友達或いはネットで知らない相手と対戦することができる。

現在[MyCard](https://mycard.moe/)という中国最大の遊戯王ファンコミュニティーがYGOProの運営や開発を主導し、グッズの販売によってサーバーの出費を支える。
YGOProに基づき、MyCardは豊富な機能（例えば競争試合やダブルモード）を提供している。その他、定期的にイベントを行い、中国のファンたちを楽しませるよう努力をしている。

## Neosの紹介
現在YGOProは[PC](https://ja.wikipedia.org/wiki/%E3%83%91%E3%83%BC%E3%82%BD%E3%83%8A%E3%83%AB%E3%82%B3%E3%83%B3%E3%83%94%E3%83%A5%E3%83%BC%E3%82%BF)と[IOS](https://ja.wikipedia.org/wiki/IOS)と[Android](https://ja.wikipedia.org/wiki/Android_(%E3%82%AA%E3%83%9A%E3%83%AC%E3%83%BC%E3%83%86%E3%82%A3%E3%83%B3%E3%82%B0%E3%82%B7%E3%82%B9%E3%83%86%E3%83%A0)の配信を提供しているが、[Web](https://ja.wikipedia.org/wiki/World_Wide_Web)の配信を提供していない。つまり、プレイヤーはアプリをウロードしなければならないので、ブラウザで直接体験することが出来ない。

今ではほとんどのソフトウェアはWeb版が配信されてあることになり（[Discord](https://discord.com/)、[Telegram](https://telegram.org/)など）、この点では「YGOProは時代遅れ」そういう意見も出るかもしれない。

この問題を解決するため、私が2022年10月にWebバージュンのYGOProの開発を開始し、「遊戯王アニメ」の二代目主人公が好きで、彼のエースモンスター「Neos」に名付けられた。
それからほぼ一年が経ち、Neosは重大な成果を収め、正式なリリースの目標に向かって進んでいる。

## Neosのデザイン
Neosのシステムは全体的に「フロントエンド」と「バックエンド」という二つの部分に分けられることができる。

バックエンドの務め：
- アカントの管理；
- ゲームの流れのコントロール；
- カードの効果の処理。

フロントエンドの務め：
- ゲーム画面の表示；
- プレーヤーの操作をバックエンドに伝える。

### バックエンド
YGOProのバックエンドには複数の実装が存在している、例えば、[233](https://ygo233.com/)と[koishi](https://srv.koishi.pro/)。
フロントエンドに特定な「IPアドレス」と「ポート番号」をあげたらバックエンドと[Socket](https://en.wikipedia.org/wiki/Network_socket)または[WebSocket](https://www.geeksforgeeks.org/what-is-web-socket-and-how-it-is-different-from-the-http/)を通じて接続することができる。

これまで遊戯王は千枚以上のカードを発売した上で、いかにこんな数のカードの効果を正確に処理するのか？
YGOProの開発者は[C++言語](https://en.wikipedia.org/wiki/C%2B%2B)に基づいて、[ygopro-core](https://github.com/Fluorohydride/ygopro-core)という「カード脚本エンジン」を開発したことで、遊戯王のカードを[neovim](https://neovim.io/)の設定ファイルのように[lua](https://www.lua.org/)脚本として処理できるようになった。

### フロントエンド
Neosは[React](https://react.dev/)と[TypeScript](https://www.typescriptlang.org/)と[CSS](https://en.wikipedia.org/wiki/CSS)に基づき操作画面を構築し、[valtio](https://valtio.pmnd.rs/)を使って状態を管理する。
全体のデザインは以下の画像に示されている：
<img src="/images/neos-arch.svg" />

詳しくはこちらへ：https://doc.neos.moe/docs/coding/design

## デモンストレーション
Github: https://github.com/DarkNeos/neos-ts
サイト: https://neos.moecube.com

<img src="/images/duel.png" width="500" />

## コードに貢献する
Welcome to create merge request in [Neos repo](https://code.mycard.moe/mycard/Neos).

