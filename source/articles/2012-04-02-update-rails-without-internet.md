---
title: オフラインでのRails3アプリ環境の構築
categories:
- Ruby
tags:
- Ruby
- Ruby on Rails
---
内製アプリの改修を納品したときにオフラインの本番環境に対してRailsアプリの更新をしなければならなかったのでメモ。
物理メディアのみのやり取りでgemの整理をするのは意外とめんどかった...

まず、下記コマンドで$RAILS_HOME/vender/cacheに依存gemのコピーが保存される。
<pre>
bundle package
</pre>
これをオンラインの環境で実施した後、オフライン環境で
<pre>
bundle install --local
</pre>
とすれば基本的にはOK。
...なのだけど、Rubygemsのバージョン依存のgemがあれば当然実行時のバージョンによってエラーが出てしまう。
デプロイ先はUbuntuだったので、rubygems-updateの最新.gemファイルを持って行って
<pre>
gem install rubygems-update --local
</pre>
とした。これで行けるかと思ったら今度はbundlerが死んだので、bundlerのgemも持って行って
<pre>
gem install bundler --local
</pre>
としてやっと解決。
bundlerはbundle packageでは入らないんでgemファイルを準備していったほうが無難っぽい。
