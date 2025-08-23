---
title: Facebook上“News Feed”和“Your Story”的区别
date: 2020-12-21T20:58:14+08:00
categories:
- Tool
tags:
- hugo
- blog
- github
---

当分享内容到Facebook时（例如使用以下的浏览器书签栏脚本），有两个选项常常让人糊涂。
<!-- more -->
```javascript
javascript:var d=document,f='[https://www.facebook.com/share](https://www.facebook.com/share)',l=d.location,e=encodeURIComponent,p='.php?src=bm&v=4&i=1545109421&u='+e(l.href)+'&t='+e(d.title);1;try{if (!/^(.\*\\.)?facebook\\.\[^.\]\*$/.test(l.host))throw(0);share\_internal\_bookmarklet(p)}catch(z) {a=function() {if (!window.open(f+'r'+p,'sharer','toolbar=0,status=0,resizable=1,width=626,height=436'))l.href=f+p};if (/Firefox/.test(navigator.userAgent))setTimeout(a,0);else{a()}}void(0)
```

简言之，News Feed就是你在Facebook上最常用的功能，你的朋友和群组的新消息都在这里聚集。一条新消息就是一个Post。

其实，与其说是分享内容到News Feed，不如说是分享到你自己的Profile（旧称Timeline）。

Your Story是News Feed中的一个特殊品类，它们只会对你选定的观众群显示24个小时。时间一过，Story就会去到一个叫做Story Archive的地方，而这个地方只对你自己可见。

如果你愿意，可以把Story再分享回News Feed。不过一旦你删除了Story，那么分享的News Feed消息也会跟着被删除。
