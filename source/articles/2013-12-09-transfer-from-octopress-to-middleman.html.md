---
title: OctopressからMiddlemanに移行した
date: 2013-12-09 00:00 JST
tags: Middleman, Octopress
---

今年のはじめにWordpressからOctopressに移行したけど、結局ブログを書くようにはならなかったよ...
Middlemanを見てみたらよさげだったので、もう一度書き始めるきっかけに再度移行してみた。

Octopressでしっくり来なかったところ
---------------
* テンプレートエンジンに挫折  
  Liquidの記法が絶望的に覚えられない...
* ファイル構成  
  Octopressはgem/コマンドラインでの管理ツールが提供されておらず、cloneしたOctopressそのものからブログを構築していく。
  Octopress自体のバージョンアップをしたい場合はpullして持ってくることになる。
  本文以外のところのタグを変更しようとしてプラグインを独自にいじっているとOctopress本体の更新とのコンフリクトが厳しい。

Middlemanを触ってみて
---------------
### よさげなところ
* 構成が単純  
  sources以下にテンプレートやassetsを放り込んでいけばOK
* Railsライク  
  Padrinoベースなせいかもしれないけど、ヘルパー名やディレクトリ構成等、明らかにRailsを意識して作っている感じ。
  いいか悪いかはともかく、Railsユーザには直観が働くようにできている。
* 好きなテンプレートエンジンが選べる   
  今回は初[Slim](http://slim-lang.com)にしてみた。
* マルチブログが簡単  
  Webサーバの設定に頼ることなく、複数ブログが簡単につくれる。

### いまいちなところ
* ブログ機能自体は貧弱  
  主眼は静的サイトジェネレータなので、
  middleman-blog が提供する機能は記事管理/タグ付け/年別アーカイブ/ページネーションぐらい。
  cssもデフォルトだとなし。プロジェクト生成直後に見える画面↓なのは流石にどうだろう...

  <a href="http://www.flickr.com/photos/uskanda/11209451975/" title="middleman-blog-default by uskanda, on Flickr"><img src="http://farm6.staticflickr.com/5493/11209451975_540c5f2e83_n.jpg" width="320" height="183" alt="middleman-blog-default"></a>

  サクッとブログ作るって用途には向いてないかな。でも0から作っていくの楽しい。
* デプロイ設定  
  Github Pagesを強く意識しているOctopressよりはデプロイ設定が面倒な感じ。  
  ↓を参考にさせて頂いてTravis CI経由でビルド成功時にGithub Pagesにプッシュするようにした。

  [ブログをJekyllからmiddlemanに移行してTravis CIでGitHub Pagesにデプロイするようにした - Webtech Walker](http://webtech-walker.com/archive/2013/08/jekyll_to_middleman.html)  
  [Middleman で作った web サイトを Travis + GitHub pages でお手軽に運用する - tricknotesのぼうけんのしょ](http://tricknotes.hateblo.jp/entry/2013/06/17/020229)
