---
title: CSS常识及奇技淫巧
date: 2010-01-10T00:37:33+08:00
categories:
- Frontend
tags:
- css
---

# 常识

* div+css的说法算是以讹传讹（同样用SSH代替J2EE，一样让人生厌），如果非要表达符合web标准的页面开发，或许可以用xhtml+css；
* div仅是一个纯洁的块（block）元素而已，块元素还包括`form`、`h1`-`h6`、`hr`、`p`、`table`等；
* span是同样纯洁的内联（inline）元素，内联元素还包括a、input等；
* css布局模型包括：流（flow）模型、浮动（float）模型，和层（layer）模型；
* DTD声明会影响浏览器工作在compliance模式还是quirks模式。
<!-- more -->
# css filters & hacks
这里的filter不是指IE的透明特效，而是指利用特别的技巧在不同的浏览器（版本）下隐藏或强制一些css行为，从而在非兼容的浏览器中实现一致的外观；

hack时常用的选择符和属性写法包括以下类型：

1. `!important`；
2. 下划线属性；
3. 转义属性；
4. `* html`；
5. 属性选择符；
6. 子对象选择符（`>`）；
7. 相邻选择符；
8. 转义选择符（`\`）；
9. 注释反斜杠（`/* xyz \*/`）。

# 很好的参考资料（但不那么实用）
[http://centricle.com/ref/css/filters/](http://centricle.com/ref/css/filters/)

[http://www.communis.co.uk/dithered/css\_filters/css\_only/index.html](http://www.communis.co.uk/dithered/css_filters/css_only/index.html)

这里精简一下：
```css
> /* 只对IE6 */
> * html #elem { color: red; }
> #elem { _color: red; }
>
> /* 只对IE7 */
> *+html #elem { color: red; }
>
> /* 只对IE6、IE7 */
> #elem { *color: red; }
> #elem { #color: red; }
>
> /* 只对IE7、IE8 */
> #elem { color/*\**/: red\9; }
>
> /* 只对IE */
> #elem { color: red\9; }
>
> /* 排除IE6 */
> html>body #elem { color: red; }
> html[xmlns] #elem { color: red; }
> head:first-child+body #elem { color: red; }
> #elem { color/**/: red; }
> #elem { color: red !important; color: blue; }
>
> /* 排除IE6和IE7 */
> html>/**/body #elem { color: red; }
>
> /* 排除IE（对FF、Chrome、Op、Saf均可） */
> body:nth-of-type(1) #elem { color: red; }
> body:first-of-type #elem { color: red; }
>
> /* 只对FF */
> #elem, x:-moz-any-link { color: red; }
```

# css tricks

* 按标准，父元素不会根据子元素的内容进行高度自适应，这时可为父元素增加`overflow:auto;`和`display:inline-block;`；
* 子元素指定`position:absolute;`时，会按指定了`position:relative;`的父元素进行子元素的绝对定位，不指定的话默认是`position:static;`哦；
* IE6，指定`float:left;`时，浮向一边的边界会变成指定边界的2倍，解决方法是再指定`display:inline;`。
