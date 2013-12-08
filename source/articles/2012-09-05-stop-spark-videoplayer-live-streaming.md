---
title: Flex SparkコンポーネントのVideoPlayerがライブストリーミングの時止まらない
tags:
- Actionscript
- Flash
---
最近はコンセプト検証用のサンプルプログラムを作って営業することが多い。
ここ数日、FlexでAdobe AIRのサンプルを作っているけど
ActionScript自体触った機会がないので手探り状態...

さて、こんなん
<pre class="lang:as decode:true " >&lt;s:VideoDisplay id="video_player"&gt;
	&lt;s:source&gt;
		&lt;s:DynamicStreamingVideoSource streamType="live" host="{data.host}"&gt;
			&lt;s:DynamicStreamingVideoItem streamName="{data.streamName}"/&gt;
		&lt;/s:DynamicStreamingVideoSource&gt;
	&lt;/s:source&gt;
&lt;/s:VideoDisplay&gt;</pre> 

作ってVideoPlayerにDynamicStreamingVideoSourceを指定してライブストリーミングを受信するようにすると、
video_player.play()で再生はできるけどstop()やpause()が効かない...(´・ω・｀)


手探りで
video_player.mx_internal::videoPlayer.stop();
としてみると止まった。

ただし、mx_internal名前空間以下のメソッドは<a href="http://cookbooks.adobe.com/post_What_is_mx_internal_-12212.html">アドビの説明</a>によると
<blockquote>
Problem
Looking at the Flex framework code, several properties and functions are prefixed with mx_internal. What is this?
Solution
mx_internal is a namespace used by the Flex framework to partition out functions and properties that may change in future releases of the Flex SDK.
</blockquote>
いつ消えるとも知れないらしい... Flexのバージョンアップに追随していく必要のあるアプリだと使えなさそう。
今回のケースでは問題少なそうだから、ひとまずこれで対処することにする。
