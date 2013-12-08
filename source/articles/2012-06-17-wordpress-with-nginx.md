---
title: Wordpressをnginx+fastcgiベースに移行した
categories:
- Server
tags:
- nginx
- Ubuntu
- Server
status: publish
type: post
published: true
meta:
  _networkpub_meta_published: done
  _edit_last: '1'
  _networkpub_meta_publish: '1'
  _networkpub_meta_content: '0'
---
旧さくらのVPS移行期限が近づいてきたので、急いでWordpressを新設したVPSに移行した。せっかくなのでnginxベースに。

WordPressは事前にWordPressディレクトリ内全ファイルをコピーしておく他、
データベースはすべてダンプし、移行先サーバに設置、インポートするだけ。データベースのダンプは
phpmyadminなどで行うか、wp-db-backup等のWordPressプラグインで行えばかんたん。

以下、Ubuntu 12.04での作業ログ。

nginx/php/fastcgiのインストール。<code>
aptitude install nginx php5-cli php5-cgi php5-gd spawn-fcgi</code>

/usr/bin/以下に以下の内容でphp-fastcgiファイルを作成。
<code>
\#!/bin/sh
/usr/bin/spawn-fcgi -a 127.0.0.1 -p 9000 -C 6 -u www-data -f /usr/bin/php5-cgi
</code>

作成したファイルに実行権限付加。
<code>
cd /usr/bin/
chmod a+x php-fastcgi
</code>

起動用スクリプト/etc/init.d/php-fastcgiを作成。

    \#!/bin/bash
    PHP_SCRIPT=/usr/bin/php-fastcgi
    FASTCGI_USER=www-data
    RETVAL=0
    case "$1" in
    start)
    su - $FASTCGI_USER -c $PHP_SCRIPT
    RETVAL=$?
    ;;
    stop)
    killall -9 php5-cgi
    RETVAL=$?
    ;;
    restart)
    killall -9 php5-cgi
    su - $FASTCGI_USER -c $PHP_SCRIPT
    RETVAL=$?
    ;;
    *)
    echo "Usage: php-fastcgi {start|stop|restart}"
    exit 1
    ;;
    esac
    exit $RETVAL
    console output

権限付加、自動起動設定してデーモン起動。
    chmod a+x /etc/init.d/php-fastcgi
    update-rc.d php-fastcgi defaults
    /etc/init.d/php-fastcgi start

nginxにWordpress用の設定を追加する。/etc/nginx/sites-available/wordpress に下記を追加。
    upstream php {
    server unix:/tmp/php-cgi.socket;
    server 127.0.0.1:9000;
    }
    
    server {
    listen 80;
    server_name your_domain_name;
    access_log /var/log/nginx/wordpress.access.log;
    error_log /var/log/nginx/wordpress.error.log;
    root /path/to/wordpress/;
    index index.php;
    location = /favicon.ico {
    log_not_found off;
    access_log off;
    }
    
    location = /robots.txt {
    allow all;
    log_not_found off;
    access_log off;
    }
    
    location / {
    try_files $uri $uri/ /index.php;
    }
    
    location ~ \.php$ {
    include /etc/nginx/fastcgi_params;
    fastcgi_param SCRIPT_FILENAME /path/to/wordpress/$fastcgi_script_name;
    fastcgi_intercept_errors on;
    fastcgi_pass php;
    }
    
    location ~* \.(js|css|png|jpg|jpeg|gif|ico)$ {
    expires max;
    log_not_found off;
    }
    }

作成した設定を有効化、fastcgi/nginxを起動。
<code>
ln -s /etc/nginx/sites-available/wordpress /etc/nginx/sites-enable/wordpress
/etc/init.d/php-fastcgi start
/etc/init.d/nginx start
</code>
<h2>参考サイト</h2>
<a href="http://iphone-diary.com/?p=9113">耐えられずにSixcoreサーバーへ移動 | 普通のサラリーマンのiPhone日記</a>
(Wordpressの移行)

<a href="http://tjun.jp/blog/2011/09/nginx/">さくらVPS+ubuntu+wordpressにnginx入れたメモ | tjun memo</a>

<a href="http://wiki.nginx.org/WordPress">WordPress</a>
(nginx公式)

<a href="http://akibe.com/wordpress%E7%94%A8%E3%81%AEnginx%E3%81%AE%E3%82%B5%E3%82%A4%E3%83%88%E8%A8%AD%E5%AE%9A%E3%82%92%E8%A6%8B%E7%9B%B4%E3%81%97/" target="_blank">Wordpress用のNginxのサイト設定を見直し @AKIBE</a>
