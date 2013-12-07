---
title: yasnippet(dropdown-list)が列ハイライト利用時にも表示が崩れないようにする
categories:
- Emacs
---
数年ぶりに設定を見直し中なので、どこまでもEmacs小ネタ。
yasnippetの補完候補表示等に利用されるdropdown-listの表示が
現在のカーソル位置の列をハイライトするcol-highlight利用時に崩れるので、
dropdown-list利用時にcol-highlightを一時停止するようにした。
<script src="https://gist.github.com/1424152.js"> </script>
