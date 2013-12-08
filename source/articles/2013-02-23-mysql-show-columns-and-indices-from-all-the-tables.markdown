---
title: MySQLで全てのテーブルのカラムとインデックス有無を表示したい
date: 2013-02-23 19:00
tags: 
- MySQL
---

今の状況：

<blockquote class="twitter-tweet"><p>ひたすらMySQLのEXPLAINと格闘中である</p>&mdash; Yusuke Kanda (@uskanda) <a href="https://twitter.com/uskanda/status/305174512075411457">February 23, 2013</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

そればっかりやっているわけにもいかないんだけど...


さて、MySQLで、ER図も何もないので今のDB全体をなんとなく俯瞰したい。
当方生ぬるいORM厨でございます。

showなんとかを繰り返さなくても、DBのメタデータ一式をINFORMATION_SCHEMAデータベースから取れるのね。便利。

<a href="http://dev.mysql.com/doc/refman/5.1/ja/information-schema.html">MySQL :: MySQL 5.1 リファレンスマニュアル :: 21 INFORMATION_SCHEMA データベース</a>

テーブルと各テーブルのカラム、インデックスを下記で取得。
ツール使えよって話だけど、手探りの状態からだと手っ取り早い。

    SELECT information_schema.columns.table_name, information_schema.columns.column_name, 
           information_schema.columns.column_type, information_schema.statistics.index_name 
    FROM information_schema.columns LEFT JOIN information_schema.statistics 
    ON information_schema.columns.table_name = information_schema.statistics.table_name 
    AND information_schema.columns.column_name = information_schema.statistics.column_name;

複合インデックスが微妙だけど今欲しいものとしては問題なし。
また、mysql起動時に-HでHTML出力にできたので、それを手元において確認中。
