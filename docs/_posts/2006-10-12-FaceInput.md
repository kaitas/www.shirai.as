---
layout: post
title: "顔入力AceSpeeder2"
date: 2006-10-12 19:22:26 GMT
author: aki
---
## PCから異臭

今日の午前中は日本からわざわざお客さんがきていたのでデモ。
昨日は朝の5時までプログラミングしてたから眠い...。

Reality Center(円柱形ディスプレイルーム、SGIとか繋がってたりする)で、自分のデモの番がきたので、いざディスプレイケーブルをつなごうとすると、PCは作動しているのに画面が消えている。そして何だか電子部品が焦げるような匂いが...。

幸い電源ボタン長押し→再投入で復旧はしたけど、なんだかやばい感じ。ファンは回っているけどときどきカラカラいうし、そもそも不快な匂いを吐きまくっている...。しかしまあ電池の爆発とかじゃなくてよかった。

さらにデスクトップPCでデモをしていると、今度は昨日にひきつづきハードディスクごと停止...仏滅かい、今日は。

こうなったら、Vistaのローンチを待たずに、ノートPC予算を執行しようかと検討中。

いまのところ優良候補は「DELL XPS M2010」なんだけど、これならVistaも動くだろうしな(OSを追加購入する予算がないのは痛いけど...)。ハードディスクが２つ付くのは良いね。8kgもする鉄板かかえてMobility Radeon X1800というのはちょっと物足りないかもしれないけど。


みなさん、お薦めのノートPCはありませんか？教えてください！

・Vista対応
・通勤用では無いので軽い必要は無い
・Shader Model 3.0以降必須
・Core Duoもしくはそれ以降
・電池は長持ちするにこしたことが無い
・壊れにくいこと
・日本のメーカーである必要は無い(ASUSとかもOK)
・フランスで買えればなおよし(OSは日米仏OK、キーボードもこの際AZERTYでも可)

----
## 顔入力AceSpeeder2

顔面で操作できるAceSpeeder2が出来上がりました。
今回のはかなりロバストです。
昼光下、人種不明、子供多し、背景光あり…ということでロバストでなければ動かないだろう、という判断です。

でも認識ループは設定次第では10msec前後で動いてます。
トータルな反応速度について、いくつか実験しないと実用レベルではないのですが、２日前の出来としてはまずまずではないでしょうか。

![FaceInput.JPG](/assets/2006/FaceInput.JPG)


それにしても１晩で作ってしまうところが恐ろしい、我ながら。
これぞ「則巻千兵衛的・科学者」の醍醐味。

細かい技術的な説明は昨夜この辺に書いたので、割愛。
- [http://ameblo.jp/akihiko/entry-10018217497.html](https://ameblo.jp/akihiko/entry-10018217497.html)
- [https://kaitas.github.io/2006/10/11/CvHaarClassifierCascade.html](https://kaitas.github.io/2006/10/11/CvHaarClassifierCascade.html)

でもいくつかメモ。

cvGetTickCountとcvGetTickFrequencyの組み合わせはすばらしい。内部でQueryPerformanceCounterを呼んでいて、これがマイクロ秒の測定を可能にしている。


さて、帰って事務作業しよう…。日本は金曜だし。
IVRC関係の旅行準備がたくさんあるしなあ（ため息）。

