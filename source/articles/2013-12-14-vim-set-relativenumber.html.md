---
title: Vimのrelativenumber設定が便利すぎてヤバイ
date: 2013-12-14 01:00 JST
tags: Vim
---

何故か近々会社でVimについて話すことになったんで、Vim環境を整理してたら良い設定を知りました。

## カーソルのある行との差分行数を表示してくれるrelativenumber

Vimでは、下記設定をするとウィンドウ左に行数を表示できます。

```
set number
```

![set number画像](http://gyazo.com/5e6b1cc7ece7aeb807aab144780cbaf3.png)

これに加えて、下記の設定を加えると

```
set relativenumber
```

見栄えがこうなります。

![set relativenumber画像](http://gyazo.com/4d20af53dcff2dc779a16b0457c0d5d8.gif)

## 何が嬉しいのか
こんな見え方が嬉しいのはVimならでは。つまり、
移動・削除等のオペレータ利用時のカウントが一目瞭然なのです！

### 例
こんなファイルがあったとします。今カーソルは24行目にあります。
ここからメソッドふたつ、52行目の"end"までを一気に削除したい場合...

![relativenumber説明サンプル]( http://gyazo.com/83d07d578b6da17b33f6a84572c5bea5.png)

僕のVim力ではこれまで行単位の範囲選択(V)をしてから52行目あたりまで移動して、
選択範囲の削除(d)をしていました。

![範囲選択](http://gyazo.com/3d7152a7734029c43571bdc028c3437e.gif)

これに対して、`set relativenumber` していると...

![relativenumberした場合](http://gyazo.com/d2df5a268c71d7823d404d1344d0a271.png)

削除したい範囲が28行先までであることがすぐわかります。
つまり、d28jと打つだけで削除できます。瞬殺です。

![relativenumberした場合の削除](http://gyazo.com/9b3e4d0480c24aa5d1bf7190e4c74842.gif)

こんな感じで、大きく離れた行や、行間に対する作業が非常にしやすくなります。おすすめです。
Vim7.3以降で使えるので、最近のLinuxディストリのビルトインVimやMacVimなら使えるはずです。
