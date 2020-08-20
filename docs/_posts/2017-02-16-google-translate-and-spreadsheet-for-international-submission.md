---
author: aki
title: "新しいGoogle翻訳とスプレッドシートを使って国際会議への執筆をスマートにするついでに英作文力を高速に身につけるハック"
slug: google-translate-and-spreadsheet-for-international-submission
id: 40305
date: '2017-02-16 12:44:46'
layout: post
comments: false
categories:
  - 大学教員
  - 大学教員ライフハック
tags:
  - CG
  - GAS
  - Google Apps Script
  - Google翻訳
  - Laval
  - Laval Virtual
  - SIGGRAPH
  - Spreadsheet
  - TeX
  - VR
  - YouTube
  - 執筆
  - 学会
  - 指導
  - 日本語
  - 書き方
  - 白井研究室
  - 英語学習
---

(2019-01-26追記) GoogleTranslate関数のカンマがセミコロンになる環境があるっぽいです。  
正確な情報は[Googleの公式ヘルプを参照](https://support.google.com/docs/answer/3093331?hl=en&authuser=1)、というところなのですが、明確な情報は見つけられませんでした。ただ筆者の環境（英語・フランス語環境）ではスクリーンショットのようにセミコロンになってしまいます。  

<figure class="wp-block-embed-twitter wp-block-embed is-type-rich is-provider-twitter">

<div class="wp-block-embed__wrapper">https://twitter.com/o_ob/status/1089020611379097600</div>

</figure>

CG,VR業界の研究者はこの時期、Laval VirtualやSIGGRAPHといった国際投稿のピークにあります。

白井研究室は規模の割には国際投稿が多いです。

[https://blog.shirai.la/publications/](https://blog.shirai.la/publications/)

また数だけでなく内容も学部生でACMの学生研究コンテストで[世界3位](https://blog.shirai.la/blog/2014/08/siggraph2014-src/)を受賞したりと、大学の入試難度の割には世界トップクラスの評価を受けることもあったりします(ちなみにACM SRCは書き物だけでなくファイナルはプレゼン審査込みです)。

本人の頑張りや先生の頑張り、研究の難度やインパクトはあるにせよ、一般的には日本語の論文を「ただ翻訳」したからといって別のアーティクルになったとみなすことはできません。しかし卒業論文や日本VR学会、インタラクションといった、日本語だったら構造的もクオリティ的にもしっかり書けるし、新規性もディスカッションもしっかりしている、さらにそのadvancementも加えられるような投稿もあるけれど、いざその学生に『英語投稿しようぜ！』と提案すると、もうその瞬間にグッチャグチャになる…といった経験はよくあります。

そもそも先生方も英語科学論文執筆のスキルや経験が十分にある方であれば指導もできるかとは思いますが、書き方のトレンドも分野によってはずいぶん違いますし、普段「日本語どっぷり業務」で押しつぶされている大学教員様が英語論文を査読等で読むのに精一杯なのに、ただ書くだけならともかく、「日本語の勢いを保ったまま翻訳する」というスキルを維持するのはなかなか難しいです。

そもそも日本語だって研究の先進性を求められるのに！英語まで書かねばならんのか！  
これはハンデだ！俺は英語圏に生まれればよかった！うわーん！！  
と嘆くのは簡単ですが、私はそうは思いません。  
日本語に加えて英語もフランス語も、中国語も少しはわかりますが、英語単一文化圏に生まれていたら、それ以外の言語に目を向ける機会もなかったでしょうし、日本語が高度だからこそ、詩や短歌、冗談やマンガ・アニメやTwitterのような楽しいことも沢山あります。

また論文を書くことによって高度な日本語を身につける機会にもなります。いい勉強です。

さて、Google翻訳です。これは英語学習には不向きな面もあります。Google翻訳を英作文の一部にでも使おうものなら「どう見ても機械翻訳」という作文になり、あらゆる先生方から否定されたものです。しかし最近のアップデートにより「より自然な翻訳結果」が取得できるようになりました。

### ではGoogle翻訳を科学論文の執筆に使えるか？というと、Noです。

少なくともそのままでは使える品質にはありません。理由はいくつかあります。

*   「自然な翻訳」のために、多少の誤りは**適当に**正してくれる（誤りを発見できない）
*   日本語と英語では論法が逆（日本語は大事なことを最後に書く）
*   日本語は構造的に書こうとすると自然な日本語にならない
*   ときどき物凄い勘違いをする
*   原文の日本語がそもそも曖昧。特に**係り受けが本人に聞かないと不明**だったりする。
*   日本語と英語の多義性を考慮する必要がある（例：Play=遊び？試合？演奏？…）
*   ただしものすごく速い、しかも無料。

以下の解説は、上記のようなGoogle翻訳の特性を利用して、英語投稿のワークフローと新しい英作文力向上のための勉強法を提案しています。特に先生方と若い学生さんがWeb上で深夜日中を問わずコラボして執筆するような環境を想定しています。細部に関してはノウハウもあるので割愛しちゃいますが、最大に重要な関数はこれです。

> # =GOOGLETRANSLATE(B1,"ja","en")

これをGoogleスプレッドシートに入れてみてください。賢い先生であればこれだけで十分と思います。

つまりこの関数を使うことで、Google翻訳のエンジンをGoogle Spreadsheetから使うことができます[*](#note)。

[関数リファレンス](https://support.google.com/docs/answer/3093331)

### 構文　`GOOGLETRANSLATE(テキスト, [ソース言語, ターゲット言語])`

使い方としてのポイントはこの先です。ワークフローにしてまとめます。

### ＜準備＞

1.  まず以下のヘッダを１行目に用意し「表示→固定→1行」、A1〜F1に以下。  

    > Question, Answer(人間による英作文), Google英語, 質問の自動翻訳, 人間による日本語, 人間による英作文の邦訳, MEMO

2.  オンライン投稿によくあるWebフォームの質問をスプレッドシートのA列に分解して貼り付ける
3.  D列[D2]にA列を日本語訳する式を設定 [<span class=" default-formula-text-color" dir="auto">=</span><span class=" default-formula-text-color" dir="auto">GOOGLETRANSLATE</span><span class=" default-formula-text-color match-paren" dir="auto">(</span><span dir="auto">A2</span><span class=" default-formula-text-color" dir="auto">,</span><span class=" string " dir="auto">"en"</span><span class=" default-formula-text-color" dir="auto">,</span><span class=" string " dir="auto">"ja"</span><span class=" match-paren default-formula-text-color" dir="auto">)</span>]
4.  E列にD列の日本語質問に該当する「とりあえずの日本語」を書く。和文論文から貼り付ける。いま書けない場合は「条件付き書式」を設定して空白セルに色付けしておくと良い。  
    ここでは例として「**触覚フィードバックを用いたショートニング不使用クッキーによるハードクッキーのテクスチャー解析**」という仮の和文論文からのコピペを貼り付けておきます。  
    ＊あえて係り受けが不明瞭なタイトルです。
5.  C列[C2]にE列を英訳するセルを設定する[=GOOGLETRANSLATE(E2,"ja","en")]
6.  さらにF列[F2]にB列を日本語訳するセルを設定する [<span class=" default-formula-text-color" dir="auto">=</span><span class=" default-formula-text-color" dir="auto">GOOGLETRANSLATE</span><span class=" default-formula-text-color match-paren" dir="auto">(</span><span dir="auto">B2</span><span class=" default-formula-text-color" dir="auto">,</span><span class=" string " dir="auto">"en"</span><span class=" default-formula-text-color" dir="auto">,</span><span class=" string " dir="auto">"ja"</span><span class=" match-paren default-formula-text-color" dir="auto">)</span>]
7.  G列はメモ、必要に応じて文字数カウントとか実装するといいです。文字数カウントはLEN()で作れますが、ワードカウントしたい人はGASで作るといいかもです（shirayuca@qiitaによる[実装例](http://qiita.com/shirayuca/items/61e7a5618d899d3ac906)）。

スクリーンショットにするとこのようになります。

[![](http://aki.shirai.as/wp-content/uploads/2017/02/スクリーンショット-2017-02-16-11.59.36-1024x577.png)](http://aki.shirai.as/wp-content/uploads/2017/02/スクリーンショット-2017-02-16-11.59.36.png)

### ＜使い方＞

手順通りに作ってくれた人は、もう使えると思います、あえてテンプレとしてダウンロードさせないのは「自分で作った方が理解できるしカスタマイズもできる」からです。列が右に左にするのは「その方が対訳として見やすい」からです。以下手順になります。

1.  D列の自動翻訳の日本語質問を読みながら、E列にまず日本語を書いていきます。
2.  するとC列に勝手に英語が生成されます。
3.  B列に「C列の英語を見ながら人間の英作文」を書きます。少なくとも単語で困ることはなく、書き出しもスラスラ書けます。ただしC列の英語が一発でOKになることはまずないです、疑ってかかるか、楽をしたければE列の日本語を改善していきましょう。
4.  英作文が正しいかどうか、F列を見ながらすすめます。E列とF列がほぼ同じ意味になればよいわけです。
5.  あれ？もう完成していますね！しかも１作文ごとに英作文力がアップしていくことを感じられます。

上記の例では「not use」というGoogle翻訳の提案を無視して「without」としています。そもそも日本語のタイトルが冗長であることに気が付いたりもします。主文が「触覚フィードバックを用いた」なのか「ショートニングを使わない」なのか、Googleさんにはわかりません。MEMO欄に「おい主著者、どっちが主文だかはっきりしろ！」と書いておくと良いでしょう。右クリックで「メモ」や「コメント」を使うと校閲しやすく、Web上で高速に共著作業が進んでいきます。

## さて本文の執筆です

上記は国際投稿の際のEasyChairやSIGGRAPH SISにおけるWebフォームの例ですが、本文も同様です。白井研究室の場合、和文の場合は[CloudLaTeX](https://cloudlatex.io/),、英語論文は[ShareLaTex](http://t.co/J1E4nZJYZr)を使用していますので、CloudLaTeXからの英語→日本語の変換工程で構造的に執筆された日本語を英語に翻訳していく過程が必要になりますから、上記のシートをコピーしてカスタマイズして、A列の質問を主著者や先生のストラテジに置き換えていけば良いのです。

Google翻訳の特性上、あまり長い作文をしようと思わない方がいいです。一方で、コンテキスト（前後関係）も重要ですので、だいたい目安としては一段落程度で区切ったり、代名詞Itなどを補完しながら中間的な（＝Googleさんにわかりやすい）言語で書いてあげると良いと思います。その言語を日本語で行える、右クリックすればメモなども使える、という点が上記のワークフローの特徴です。必要であればどんどん行を増やしていくと良いです。

最後にB列をガシッとコピーして、Word等のトラディショナルな英語チェック環境やエキサイト翻訳のようなクラシックな翻訳エンジンに通してみることをお勧めします。図版を入れる作業なども必要ですからこのワークシートだけで全てを終わらせるわけにはいきませんが、この段階で人間の有料英語レビューに依頼できるレベルまでは達しているはずです。Todo管理なども含めると分業もしやすくずいぶんとストレスの少ない英語執筆が可能になると思います。

ブログに書いた方がいいだろうなというレベルはこの辺りまでですね！

白井研究室のノウハウとしては、上記の方法だけで論文を書いている訳ではありません。これに加えてGAS(Google Apps Script)なども組みあわせていったりもします。ビデオの字幕やYouTube字幕などもこれでずいぶん改善されます。そもそもワークフローにこだわるというよりは自力で、動的に、改善していくことが重要と思います。

なおGoogle翻訳はGoogle Cloud API経由でも使える訳ですが、課金やセットアップが必要な情報に比べてもずいぶんスマートなのでした。  
http://unokun.hatenablog.jp/entry/2015/08/08/103841

白井としては、これでAndroidタブレットやスマホでも書ける！というのは大きいです（右腕が使えませんので、机で両腕を使って書ける時間が限られているのですイタタ…）。

フィードバックありましたら [@o_ob](https://twitter.com/o_ob) までどうぞ！

<a name="note"></a>*(追記:2017/2/17 22:00)  

<blockquote><a href="https://twitter.com/_240_/status/832506607196106752"></a></blockquote>  
<blockquote><a href="https://twitter.com/o_ob/status/832519206021107712"></a></blockquote>

本稿のGoogle Spreadsheet関数で利用できるGoogle翻訳では、フレーズ間の翻訳確率を計算して翻訳先の言語の適切な語順に並べ替える、フレーズベース機械翻訳（PBMT）を採用しているようです。2016年11月にアップデートされたニューラルネットワークベースのGoogle Neural Machine Translation（GNMT）はPBMTよりも翻訳精度が上がる印象がありますが、本稿の関数にはまだ実装されていないようです。  
ご参考：グーグルの翻訳AIが「独自の言語」を生み出したといえる根拠（2016.11.24）  
http://wired.jp/2016/11/24/google-ai-language-create/

(例1)  
原文：**Percent of overcrowded households among bottom quintile of income distribution.**

Spreadsheet関数版Google翻訳（エンジン不明）：**所得分配の底五分位間の過密世帯の割合。**  
[Web版Google翻訳（GNMT日英）](https://translate.google.co.jp/#en/ja/Percent%20of%20overcrowded%20households%20among%20bottom%20quintile%20of%20income%20distribution.)：**所得分配の下位5分の1の間で混雑した世帯の割合。**

ちなみにWeb版のほうもクリックすると翻訳候補として「底五分位間の」が出てきますのでやはり「新しい」とはいえGNMTはまだSpreadsheetには使われてないと見てよいでしょう。いつ反映されるのでしょうかね！楽しみです。ただしある日突然変わるので注意が必要です。原文や作文はちゃんと保持してくださいね。

(例2)2017/2/18 23:00追記  
原文: **Talk of tech innovation is bullshit. Shut up and get the work done – says Linus Torvalds**

GNMT日本語訳: **技術革新の話はうそつきです。シャットダウンして作業を完了させる - Linus Torvalds**

GoogleTranslate関数: **ハイテク技術革新の話はでたらめです。黙って仕事を成し遂げる - Linus Torvalds氏は述べています**

この文であればGoogleTranslate関数の方が素直な訳でいいですね、GNMTによる日本語訳は英語に直すと「The story of technological innovation is a liar. Shut down and complete the work」、うそつきとシャットダウンが強く残ってしまっています。  
なおこの一文は実際のニュースとしてはもっと恣意的な翻訳をされているのでまだマシなのかもしれませんが…。

<blockquote><a href="https://twitter.com/o_ob/status/832766274203561984"></a></blockquote>

しかしGoogle翻訳(GNMT)の翻訳結果がお上品になるのは良いことなんだろうか？「ブルシッt」が「うそつきです」になる事で人類のヘイトを抑えられるどころかより齟齬を産んでるんじゃねーの、って気持ちもある。  
この辺り、もう現実はチェス囲碁将棋AIと翻訳に関してはSFに両足突っ込んでる感じがしますね。シンギュラリティです。

ところでSpreadsheetにはこれ以外にも[面白い関数](https://support.google.com/docs/table/25273?hl=ja&ref_topic=3105411)がいっぱいあります。

ImportFeed, ImportXML, IMAGE, それに最新の株価・為替が取得できるGoogleFinance関数も便利です。

Excelで苦手なヒストグラムも一発で出せますよ！

どんどん使ってみてくださいね。

## ご紹介の際は一言頂ければ幸いです

国際論文連発の研究室が明かす、英作文超ノウハウ。Google翻訳ってスプレッドシートから使えるんだ！｜ギズモード・ジャパン   

[https://www.gizmodo.jp/2017/03/google_translate_spreadsheet.html](https://www.gizmodo.jp/2017/03/google_translate_spreadsheet.html)

(追記2019-01-26)  
いつまでもスプレッドシート関数が更新されないので簡単に #LanguageApp 使えるようにするTipsを @kaz_inoue さんが書いてくださっています  
**Google Spreadsheet の googletranslate 関数の代わりに LanguageApp を使うワークシート関数を作ってイケてる翻訳ができるようにする**  
[https://qiita.com/kazinoue/items/82779a11af8a2dea0d21](https://twitter.com/o_ob/status/1089022941398888448)  

<figure class="wp-block-embed-twitter wp-block-embed is-type-rich is-provider-twitter">

<blockquote><a href="https://twitter.com/o_ob/status/1089022941398888448"></a></blockquote>

</figure>