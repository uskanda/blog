---
title: Rsenseでの補完時に引数等を自動補完する
tags:
- Emacs
- Ruby
categories:
- Ruby
---
Emacsの整理にあたり、いつか試そうと思ってたけど使ってなかった
<a href="http://cx4a.org/software/rsense/index.ja.html" target="_blank">Rsense</a>を導入してみたらすごく便利だった！

組み込みライブラリのメソッド名の補完等はバッチリなんで、せっかくなんで
yasnippetと連携させて引数やブロック有無なども補完できるようにしてみた。

<a href="https://github.com/uskanda/ac-rsense-yas-expand">https://github.com/uskanda/ac-rsense-yas-expand
</a>

Emacs, auto-completeでのRsense利用が前提。
力技でRefeから組み込みライブラリの主要メソッドのsnippetを作って、
これまた力技でauto-completeにRsenseから伝えられたクラス情報を横取りして、yasnippetの起動条件に渡してる。
これで組み込みライブラリに関していえばIDEと遜色ないのではないかと。
