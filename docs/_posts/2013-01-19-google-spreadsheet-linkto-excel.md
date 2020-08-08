---
author: aki
title: "Google SpreadsheetとEXCELを連携させる意外な方法"
slug: google-spreadsheet-linkto-excel
id: 6652
date: '2013-01-19 17:39:16'
layout: post
# categories:
#  - TIPS
tags:
  - EXCEL
  - Google Apps Script
  - Spreadsheet
---

Google Spreadsheetはとても便利なクラウドオフィス環境ですが、<span style="color: #ff0000;">最大の弱点</span>があります。

# それは「印刷に弱い」ということです。

印刷をしなくていい業務であればよいのですが、業務アプリの開発は「<span style="color: #ff0000;">最後は紙</span>」であることも多いのです。 私がこれまでGoogle Apps Scriptで開発してきた業務アプリにおいて，そこそこ凝った帳票はGoogle Docsワードプロセッサの文字置き換え→PDF出力→メール添付→あらかじめ印刷しておいた帳票に手差し印刷、という方法をとって来ましたが、フォントは化けますし、どうしてもEXCELで普及している罫線たっぷりのフォームを全面置き換えするところまでたどり着きませんでした。 今回はあきらめて，Google Docsで管理してきたデータを最終工程でEXCELにデータを取り込まなければならない環境，という前提で話を進めます。 もちろんGoogle Spreadsheet側のデータの更新の必要がなければ、ダウンロードして使えばいいことです。しかしレポート出力後もデータの更新がある場合、何度もEXCEL形式でダウンロードして，リンクを貼り直して…というやり方では何かかっこ悪いし、事故が起きそうです。 ここでは、完全にエンドユーザにも任せられて、プログラミングは全く使用せず、それでいてセキュリティ的にも感じのよい方法を紹介します。 『えっそんな方法あるの？しかも無料で…？』という感覚をお持ちになるかもしれませんが、私もそうでした。 Google DocsのデータとOfficeを連携させるOffiSync社はJiveに買収されてしまいましたし，大塚商会のデータースパイダーはODBC経由でよくできていそうですが，有料です． [http://www.offisync.com/index.html](http://www.offisync.com/index.html) [http://www.otsuka-shokai.co.jp/products/dwh/bi-tool/dataspider/adapter/](http://www.otsuka-shokai.co.jp/products/dwh/bi-tool/dataspider/adapter/) MySQLやZendPHP経由でいいのであれば、他にもやり方はあるのですが、そこまでコストを払いたくない！という人向けの方法です。 以下の手順を見ればわかりますが、EXCELやGoogle Docsのユーザであれば「使ったことがある機能の組み合わせ」で実現できてしまいます。

## 【Google Docs側でのエクスポート設定】

まず、GoogleDocs上のファイルから「ウェブに公開...」を選択します。そこで以下のようにエクスポートしたいテーブルを設定します。 [![WebPub](http://aki.shirai.as/wp-content/uploads/2013/01/WebPub.png)](http://aki.shirai.as/2013/01/google-spreadsheet-linkto-excel/webpub/) この公開用URLは元来、Google DocsのデータをHTMLとして表示したり、IFRAMEを使ってWebページに組み込んだりするのに使われていました。HTML形式以外ですとCSV，TSVとPDFが選択できますが、今回は動的更新のためにあえてHTML形式を使います。

## 【EXCEL側でのインポート設定】

さて、次はEXCELです。 リボンメニューの「データ」から「Webクエリ」を選んでください。 [![WebQuery](http://aki.shirai.as/wp-content/uploads/2013/01/WebQuery.png)](http://aki.shirai.as/2013/01/google-spreadsheet-linkto-excel/webquery/) ……もうおわかりですね！ここに先ほどのエクスポートURLを設定して、データが取れればラッキーです。やってみましょう。 [![WebQuery2](http://aki.shirai.as/wp-content/uploads/2013/01/WebQuery2.png)](http://aki.shirai.as/2013/01/google-spreadsheet-linkto-excel/webquery2/) よく見ると、オプションと取り込むテーブルをここで設定できます。 黄色い→で明示的に指定し、オプションでは様々なチェックボックスがあります。いろいろ試してみたところ、テキストフィールドの改行壊れを防ぐためにもHTMLであることを明示するのが良いようです。 さらに次のステップで「新しいシート」を取り込み先で選ぶことができますが、その前に「プロパティ」を選択してください。 [![WebQuery3](http://aki.shirai.as/wp-content/uploads/2013/01/WebQuery3.png)](http://aki.shirai.as/2013/01/google-spreadsheet-linkto-excel/webquery3/) 名前，更新頻度，新しいデータに対する扱いなどを設定できます。これはすばらしい。 さて、取り込み完了です。あとはEXCEL上で好きに料理すれば良いと思います。フォーム上からVLOOKUPを使って必要なデータを取れば印刷専用のEXCELを作ることも容易いでしょう。 [![WebQuery4](http://aki.shirai.as/wp-content/uploads/2013/01/WebQuery4-1024x211.png)](http://aki.shirai.as/2013/01/google-spreadsheet-linkto-excel/webquery4/) このデータ領域は「全て更新」を選ぶことでいつでも更新できます。もちろんEXCEL→Docsへの更新はできませんが、元々フォーム印刷目的ですのでセキュリティ的にもこれでいい用途もあるのでは？ ★VLOOKUPについて知りたい方はリクエストしてくださいね！ (書いてたら消えた) これでGoogleDocsをコアにして、確定申告やら請求書やらの帳票関係もクラウド化して、年賀状印刷などの紙が絶対必要な顧客管理アプリも統合させる見通しができました。 クラウドに乗せられないEXCEL守秘データとの整合もとれるし、謎の外部サービスにGoogleのパスワードをいれさせたりしないし、HTTPSで接続しているし(URLで鍵が丸見えなのでOfficeの接続を検証しないとセキュアとはいいがたいですが)可能性のある方法です。 GoogleDocsがXMLエクスポートをサポートするともっと使いでがありそう！