---
title: Android3.2で通知を出そうとするとエラーが出る
published: true
date: 2013-04-01 19:22
comments: true
tags: Android
---

## 問題
Androidアプリで通知を出そうとするとエラーの出る機種があるよ...
Honeycombの一部機種でだけ起こってるみたいだよ！

## こんなエラーが出てる

    E/AndroidRuntime(25922): FATAL EXCEPTION: main
    E/AndroidRuntime(25922): java.lang.NoSuchMethodError: android.app.Notification$Builder.setProgress
    E/AndroidRuntime(25922): 	at android.support.v4.app.NotificationCompatIceCreamSandwich.add(NotificationCompatIceCreamSandwich.java:31)
    E/AndroidRuntime(25922): 	at android.support.v4.app.NotificationCompat$NotificationCompatImplIceCreamSandwich.build(NotificationCompat.java:104)
    E/AndroidRuntime(25922): 	at android.support.v4.app.NotificationCompat$Builder.build(NotificationCompat.java:558)

## 原因
Android Support LibraryがAPI Level 13(Android 3.2)の機種に対してバグってたよ...
手元の3.0や3.1で試しても出なかったはずだよ...

<a href="https://code.google.com/p/android/issues/detail?id=36502">Issue 36502 - android - android support library v4 and notification on android-13 - Android - An Open Handset Alliance Project - Google Project Hosting</a>

android-support-v4.jarを更新したら直ったけどライブラリの差し替えなんてやりたくない時期だよ...(´・ω・`)
