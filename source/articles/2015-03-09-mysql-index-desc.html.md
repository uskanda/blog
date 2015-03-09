---
title: MySQLのindexは降順にできない
date: 2015-03-09 22:40 JST
tags:
- MySQL
- Tips
- 恥ずかしながら今知ったシリーズ
categories: 
- データベース
---

`ORDER BY hoge ASC, fuga DESC`のように、複数カラムを利用し、かつ昇順/降順を両方含むソートをするクエリが遅い。  
実行計画を見ると`Use filesort`が出てて消さない...  インデックスがうまく効いていない？と思って調べているとぶつかったのがこれ。

> `index_col_name` 仕様は ASC か DESC で終わることができます。これらのキーワードは昇順や降順インデックス値ストレージを指定するための将来の拡張子として許容されます。現在は、それらは解析されますが無視されます。インデックス値は毎回昇順で格納されます。
>
> [MySQL :: MySQL 5.1 リファレンスマニュアル (オンラインヘルプ) :: 8.1.13 CREATE INDEX 構文 ](http://mysql.stu.edu.tw/doc/refman/5.1-olh/ja/create-index.html)

ってことは昇順/降順が統一されていない並び順の複合インデックスは作れない。 

いやいやこれMySQL5.1のリファレンスだし...

> An `index_col_name` specification can end with ASC or DESC. These keywords are permitted for future extensions for specifying ascending or descending index value storage. Currently, they are parsed but ignored; index values are always stored in ascending order.
>
> [MySQL :: MySQL 5.6 Reference Manual :: 13.1.13 CREATE INDEX Syntax](http://dev.mysql.com/doc/refman/5.6/en/create-index.html)

Oh... 
5.6でもダメでした。

そんなわけでソート条件に昇順/降順両方含む場合は別にソート用カラムを設けるのが無難ですね。
