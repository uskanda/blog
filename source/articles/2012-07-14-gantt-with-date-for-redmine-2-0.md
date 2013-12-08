---
title: Redmine 2.0のガントチャートに日付表示を追加する
categories:
- Ruby
tags:
- redmine
- Ruby on Rails
---
Redmineのガントチャートはデフォルトだと日付がでない。過去にパッチが作られている。

<a href="http://ameblo.jp/hihihihiroki/entry-10854457740.html">【Redmine 1.1.2】ガントチャートに日付を表示させる｜渋谷ではたらくマー君の技術とかブログ。</a>
<a href="http://in.shappi.org/article/195687999.html">Redmineガントチャートの日付表示再び: 100ねんごの未来予想図</a>

これらを参考に、Redmine2.0でViewを直接書き換えた。ほぼ上記サイト作成のものそのままで動いた。

<a href="http://www.flickr.com/photos/uskanda/7564467856" title="gantt-with-date"><img src="http://farm8.staticflickr.com/7272/7564467856_464d4e4f27.jpg" alt="gantt-with-date" class="aligncenter"/></a>

Redmine 2.0.3.stable.9920にて確認。
$RAILS_HOME/app/views/gantts/show.html.erbに下記パッチ。

<script src="https://gist.github.com/3107779.js?file=show.html.erb.patch"></script>

こういう変更はERB差し替えになってしまう以上、Redmineプラグインにするのも微妙... バージョンアップごとにパッチするしかないのかなー
