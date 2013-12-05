---
title: RVM+PassengerでRuby1.8系と1.9系を同時利用する
categories:
- Ruby
tags:
- Ruby
- RVM
- Passenger
---
半年前に書いたものがアップせずに残ってたorz    
一応あげておこう。。。    

RedmineはまだRuby1.8/Rails2系しか対応してないからRuby1.8を使わなきゃいけないけど、    
他のRailsアプリはRuby1.9で動作させるようにしたい！というわけで    
Passengerで複数のRubyを使ってアプリを動かす方法を探したら、    
そのまんまの記事がPassenger公式に上がってた。    

<a title="Permanent link to Phusion Passenger &amp; running multiple Ruby versions" rel="bookmark" href="http://blog.phusion.nl/2010/09/21/phusion-passenger-running-multiple-ruby-versions/">Phusion Passenger &amp; running multiple Ruby versions</a>    

Passengerはnginx利用で単体起動する機能があるようで、    
"passenger start"でnginxインストールから起動までやってくれる。    
standaloneの場合、これで立ち上がったPassengerに大して、メインのApache/nginxのリバースプロキシでアクセスする。    
rc.localに自動起動のための設定を書いた。    

```Shell
su - $USERNAME -c "    
cd /webapps/redmine    
rvm use 1.8.7-head    
passenger start -a 127.0.0.1 -p 3000 -e production -d    
rvm use 1.9.2-head"
```
