---
layout:       post
title:        "在HTML中使用JavaScript"
subtitle:     "《JavaScript高级程序设计》"
date:         2018-04-10 16:00:00
author:       "Raquel"
header-img:   "img/in-post/post-eleme-pwa/eleme-at-io.jpg"
catalog:      true
tags:
    - 读书笔记
---

>做了半年前端，很后悔浪费了半年，决定开始好好干

###

<script>

元素

包含在

<script>

内部的JavaScript代码被从上到下依次解释，在解释完成前，页面中的其余内容不会被浏览器加载或者显示。

**async**：立即下载脚本，但不应妨碍页面中其他操作，只对外部文件有效。不保证执行顺序。

**defer**：脚本可以延迟到文档完全被解析和显示之后再执行，只对外部文件有效。相当于立即下载，但延迟执行。

**外部资源** 建议将

<script>

标签尽量放到body底部（浏览器在遇到

<body>

标签才开始出现内容）。IE 8， Firefox 3.5， Safari 4和Chrome 2都允许并行下载JavaScript文件，这样在下载外部资源时不会阻塞其他

<script>

标签。
