---
title: 僕の覚えた順Vimコマンド
tags:
- Vim
categories:
- Vim
---
あけましておめでとうございます。年末年始、風邪で死んでおります。
なんだかよくわかりませんが、ここ数カ月体中の節々が痛いです。年ですか。
ちょっと作業するだけで<strong>小指も痛い</strong>ので、
今年はEmacsからVimへの乗り換えを画策したいと思います。
本当はSublime Text2にしたかったけど、痒いところに微妙に手が届かず、断念orz
そんなわけで、MacVimを使いながら、勉強したコマンドを
覚えた順に列挙していきたいと思います。適宜追加予定。
<h2>これを書き始めたときの僕のviレベル</h2>
<ul>
	<li>基本的にEmacsユーザ</li>
	<li>viはサーバの設定ファイルとかいじるときとかにたまに使用</li>
	<li>最低限のモード切り替え(i,A,etc)、移動(hjkl,gg,etc)や、最低限のコピペ(dd/yy/p)とかは知ってる</li>
</ul>
<h2>ビジュアルモード</h2>
コピー等する領域をコマンドベースじゃなくて、範囲を確認しながら行うモード。
ふつーのエディタならShift+カーソルで選択している状態。Emacsだとtransient-mark-modeオンでのリージョン選択相当。以下の表は記載なければビジュアルモードでのコマンド。
<table border="0">
<tbody>
<tr>
<td>ノーマルモードでv</td>
<td>ビジュアルモードに入る。
現在のカーソル位置から始まる任意の範囲を選択できる。
vの代わりにVで行単位での選択、&lt;C-v&gt;で矩形選択。</td>
</tr>
<tr>
<td>hjkl等</td>
<td>hjklはじめ、移動はノーマルモードと同様に利用可能。</td>
</tr>
<tr>
<td>d</td>
<td>選択範囲を削除</td>
</tr>
<tr>
<td>c</td>
<td>選択範囲を削除してインサートモードにする。</td>
</tr>
<tr>
<td>y</td>
<td>選択範囲をコピー(ヤンク)</td>
</tr>
</tbody>
</table>
<h2>画面分割</h2>
<table border="0">
<tbody>
<tr>
<td>:split もしくは &lt;C-w&gt;s</td>
<td>画面を水平分割</td>
</tr>
<tr>
<td>:vsplit もしくは &lt;C-w&gt;v</td>
<td>画面を垂直分割</td>
</tr>
<tr>
<td>&lt;C-w&gt;[hjkltb]</td>
<td>hjklで指定した方向の画面に移動。
&lt;C-w&gt;tで最初のウィンドウ、bで最後のウィンドウ</td>
</tr>
<tr>
<td>&lt;C-w&gt;c</td>
<td>分割した画面を閉じる</td>
</tr>
</tbody>
</table>
<h2>インデント</h2>
<table border="0">
<tbody>
<tr>
<td>&gt;&gt;</td>
<td>インデントを挿入</td>
</tr>
<tr>
<td>&lt;&lt;</td>
<td>インデントを削除</td>
</tr>
<tr>
<td>=</td>
<td>指定した範囲をオートインデント</td>
</tr>
<tr>
<td>gg=G</td>
<td>ファイル全体に対してオートインデントを適用。
ファイル先頭に移動(gg)→オートインデント(=)→ファイル終端(G)まで。</td>
</tr>
</tbody>
</table>
<h2>zencoding.vim</h2>
VimでのZen-Coding。下記をみながらお勉強。

<a href="http://mattn.kaoriya.net/software/vim/20100306021632.htm">Big Sky :: zen-codingの殆どの機能をzencoding.vimに取り込んだ。</a>

<table border="0">
<tbody>
<tr>
<td>略語入力後&lt;C-y&gt;,</td>
<td>Zen-Coding略語展開</td>
</tr>
<tr>
<td>範囲選択後&lt;C-y&gt;,</td>
<td>任意のタグで選択範囲を括る</td>
</tr>
</tbody>
</table>
<h2>移動・編集とか</h2>
編集の肌感覚がなんとなくわかってきた。
<table border="0">
<tbody>
<tr>
<td>g,</td>
<td>直前の編集箇所に戻る</td>
</tr>
<tr>
<td>cw</td>
<td>カーソル位置の単語を単語の終わりまでを削除してインサートモードに移行</td>
</tr>
<tr>
<td>caw</td>
<td>カーソル位置の単語全体を削除してインサートモードに移行</td>
</tr>
<tr>
<td>dw</td>
<td>カーソル位置から単語の終わりまでを削除</td>
</tr>
<tr>
<td>daw</td>
<td>カーソル位置の単語全体を削除</td>
</tr>
<tr>
<td>d$</td>
<td>カーソル位置から行末までを削除</td>
</tr>
<tr>
<td>d0,
d^</td>
<td>行頭からカーソル位置までを削除</td>
</tr>
</tbody>
</table>
