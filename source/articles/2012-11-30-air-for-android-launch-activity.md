---
title: AIR for Androidの起動アクティビティ名
tags:
- Adobe AIR
- Flash
- Android
---
2,3回調べちゃったので備忘。

AIR for Androidで作成したapk のエントリポイントとなるActivityの名称は
"AppEntry" 。

なので、adbからAIR for Androidで作成したアプリを起動する必要がある場合は以下のコマンドで実行可能。

<pre class="lang:sh decode:true crayon-selected" title="Launch AIR for Android App">adb shell am start -a android.intent.action.MAIN -n air.{APP_ID}/.AppEntry</pre>
