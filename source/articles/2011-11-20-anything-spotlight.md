---
title: anythingのspotlight検索項目でバイナリファイルを開くときにMacアプリケーションを使う
categories:
- Emacs
tags:
- Emacs
- anything.el
---
Spotlightの検索結果PDFを直接Preview.appで開きたいんでつくったー。    
<script src="https://gist.github.com/1379387.js"> </script>    
Macアプリケーションで開きたい拡張子をanything-c-source-mac-spotlight2-open-file-extensionsに加える。    
anything-c-source-mac-spotlight2をanythingのanything-c-source-mac-spotlightの代わりにsourceとして使えばOK。    
ファイル開く動作全般に適用しようかとも思ったけど、PDFや画像を開くケースってspotlight検索ぐらいな気がしたので、    
ひとまず満足。
