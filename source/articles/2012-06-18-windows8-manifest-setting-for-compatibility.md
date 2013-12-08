---
title: Windows8デスクトップアプリでの互換性マニフェスト設定
tags:
- Windows
categories:
- Windows
---
Windows7でもネイティブモードで動かすためにはマニフェストに互換性設定が必要だったように、Windows8でもネイティブモードで動かすにはマニフェストに宣言が必要。

<a href="http://msdn.microsoft.com/en-us/library/hh848036(v=vs.85).aspx">App (Executable) Manifest (Preliminary)</a>

Windows8でもネイティブモードでないとプログラム互換性アシスタント(PCA)が動く。
<blockquote><strong>Program Compatibility Assistant (PCA)</strong>
<ul>
	<li>Windows 8: Apps with the compatibility section do not get the PCA mitigation.</li>
	<li>Windows 7: Apps with the compatibility section are tracked for potential compatibility issues for Windows 8 changes (described in this document).</li>
	<li>Windows Vista (default): Apps that fail to install properly or crash during runtime under some specific circumstances get the PCA mitigation. For more information, see the Resources section.</li>
</ul>
</blockquote>
Windows8サポートであることを明示し、ネイティブモードで動かすには以下のGUIDをcompatibilityセクションで指定する。
<blockquote>{4a2f28e3-53b9-4441-ba9c-d69d4a4a6e38}</blockquote>
MSDN記載のサンプルは以下。
<blockquote>&lt;?xml version="1.0" encoding="UTF-8" standalone="yes"?&gt;
&lt;assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0"&gt;
&lt;compatibility xmlns="urn:schemas-microsoft-com:compatibility.v1"&gt;
&lt;application&gt;
&lt;!--The ID below indicates app support for Windows Vista --&gt;
&lt;supportedOS Id="{e2011457-1546-43c5-a5fe-008deee3d3f0}"/&gt;
&lt;!--The ID below indicates app support for Windows 7 --&gt;
&lt;supportedOS Id="{35138b9a-5d96-4fbd-8e2d-a2440225f93a}"/&gt;
&lt;!--The ID below indicates app support for Windows Developer Preview --&gt;
&lt;supportedOS Id="{4a2f28e3-53b9-4441-ba9c-d69d4a4a6e38}"/&gt;
&lt;/application&gt;
&lt;/compatibility&gt;
&lt;/assembly&gt;</blockquote>
