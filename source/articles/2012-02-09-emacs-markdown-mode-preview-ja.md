---
title: markdown-modeのプレビューで日本語が消える
tags:
- Emacs
categories:
- Emacs
---
最近はEmacs+markdown-modeで仕事の議事録をとってみてる。
だけど、markdown-modeで、markdownの変換結果プレビューすると日本語が全滅状態...

markdown-modeの問題というよりか、今の自分の環境では
リージョンをコマンドに引き渡すshell-command-on-regionそのものが日本語をうまく持っていけてないみたい。

ひとまず、リージョンではなくファイルで引き渡す設定が下記でできるので
markdown-modeの問題はこれで解決。
<code>
(setq markdown-command-needs-filename t)
</code>
