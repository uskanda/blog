---
title: Windows 8のMedia Center Packを適用するとエディション名が変わる
categories:
- Windows
tags:
- Windows
- Windows8
- MediaCenterPack
---

Windows 8はWindows2000以来初めて、発売日に手に入れてない(^_^;)    
仕事で各プレビュー版をそれなりに触ってしまったので、情熱が。。。  
さて、Windows 8は単体ではDVD再生ができない。これは前から周知があった。

<a href="http://msdn.microsoft.com/en-us/library/windows/desktop/ms724358(v=vs.85).aspx">GetProductInfo function</a>

以下のMedia Center Packを適用すれば再生可能になる。2013/1/31まではタダらしい。

<a href="http://windows.microsoft.com/ja-JP/windows-8/feature-packs">機能の追加 - Microsoft Windows</a>

このMedia Center Packを当てたWindows 8 Proは、通常のWindows 8 Proとは別エディションになるようだ。

見た限り、エディション判別によく使う、getProductInfo APIのpdwReturnedProductTypeの値がWindows 8 Proと異なる。

<a href="http://msdn.microsoft.com/en-us/library/windows/desktop/ms724358(v=vs.85).aspx">GetProductInfo function</a>

Media Center Packを適用すると、Proを示すPRODUCT_PROFESSIONAL(0x00000030)でなく、
PRODUCT_PROFESSIONAL_WMC(0x00000067)になってるようだ。

WindowsのOSバージョン/エディション判定ロジックのWindows8対応を行ったプロダクトがある場合、この点を見逃していないか確認が必要かも。


<a href="http://www.amazon.co.jp/exec/obidos/ASIN/B009K1SK3E/uasmks-22/ref=nosim/" target="_blank"><img src="http://ecx.images-amazon.com/images/I/510nCGJ7QdL._SL160_.jpg" alt="Microsoft Windows 8 Pro (DSP版)  64bit 日本語" /></a><br /><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B009K1SK3E/uasmks-22/ref=nosim/" target="_blank">Microsoft Windows 8 Pro (DSP版)  64bit 日本語</a>
