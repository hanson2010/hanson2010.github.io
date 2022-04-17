---
title: Python字符编码常识
date: 2010-01-21T10:21:37+08:00
categories:
- Python
tags:
- unicode
- python
---

Unicode是被所有主要计算机公司接受的非官方字符集，而ISO 10646（UCS）是被视为全球法定标准。两个标准包括相同的字符库和二进制表示。

为了方便传输和存储，一般要对Unicode进行编码转换。常见的编码有ISO8859-1、GB2312、GBK、UTF-8，和UTF-16等，其中UTF-16直接就是Unicode编码，未做转换。Unicode 5.0如果不算兼容区共包含70217个汉字。GB2312有6763个汉字，GBK有21003个汉字，GB18030-2000有27533个汉字，GB18030-2005有70244个汉字。
<!-- more -->
Python中的str和unicode类型分别对应字节码字符串（Byte string，不提扩展ASCII字符集了）和最多占据4字节的数字（Unicode字符集）。任何时候仅在程序内部使用Unicode对象进行保存和计算，I/O时需要进行编码。decode(encoding)可以把字节码字符串转换为Unicode，encode(encoding)可以把Unicode转换为字节码字符串。

```
> >>> '海生'
> '\xba\xa3\xc9\xfa'
> >>> u'海生'
> u'\u6d77\u751f'
> >>> '海生'.decode('gbk')
> u'\u6d77\u751f'
```

要工作在UTF-8下，需要将Python源代码以带BOM的UTF-8编码保存，并在文件头部添加：
```
> #!/usr/bin/env python
> # -*- coding: UTF-8 -*-
```

Windows上大量应用程序以代码页（Code page）为基础，简体中文Windows XP的默认代码页是936，即编码是GBK，在不指定编码时使用。

```
> >>> u'\u9fa5'.encode('gbk')
> '\xfd\x9b'
> >>> print u'\u9fa5'.encode('gbk')
> 龥
> >>> print u'\u9fa5'
> 龥
```

同样的数据经过不同的编码可以得到不同的二进制结果，如果查询同样的GBK代码页可能对应于不同的字符。也就是说，使用与环境不兼容的编码是引入乱码的原因。

```
> >>> u'\u9fa5'.encode('utf-8')
> '\xe9\xbe\xa5'
> >>> print u'\u9fa5'.encode('utf-8')
> 榫
> >>> '榫'
> '\xe9\xbe'
```

在GB18030中新添加的汉字不能使用GBK编码，即便通过GB18030编码后也不能在未配置相应代码页的终端上正常显示。

```
> >>> print u'\u3400'.encode('gbk')
> Traceback (most recent call last):
> File "", line 1, in
> UnicodeEncodeError: 'gbk' codec can't encode character u'\u3400' in position 0:
> illegal multibyte sequence
> >>> print u'\u3400'.encode('gb18030')
> ??
```
