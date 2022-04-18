---
title: 锟斤拷
date: 2011-04-23T23:31:25+08:00
categories:
- Python
tags:
- unicode
- encoding
---

今天不是聊我新取的ID——虽然它真是很酷的一个，[又]({{< relref "character-encodings-w-python" >}})来聊乱码问题了。相信每一个在非英语环境中工作的程序员都受到过乱码的困扰，做为程序员，简单的说，应始终意识到在内存中字符串是以Unicode方式表示的，在I/O时尽量使用UTF-8编码（除了在中文Windows控制台输出时不得已而使用GBK/GB18030），当遇到不可控制的外部系统使用了其他编码方式时，使用恰当的方法进行解码。
<!-- more -->
Unicode的基本多文种平面（Basic Multilingual Plane，BMP），即UCS-2，共有216\=65536个字符，能够满足绝大多数使用需求，另外的补充多文种平面（Supplementary Multilingual Plane，SMP），即UCS-4，更是提供了231\=2147483648个地址空间（UCS-4的首位恒为0），实际上在Unicode标准中已经定义了超过10万个字符，提供给全体地球人使用。

考虑以下Java代码：

```java
logger.info("当前JRE版本：" + System.getProperty("java.version"));
logger.info("当前默认字符集：" + Charset.defaultCharset());

String str = "UTF-8字符";
byte[] bytes = {(byte) 0xC0, (byte) 0xC0};

try {
	byte[] b1 = str.getBytes("ISO-8859-1");
	logger.info("使用ISO-8859-1编码：{}", toHexStr(b1));
	logger.info("使用UTF-8解码并转为Unicode字符串：{}", new String(b1, "UTF-8"));

	String s1 = new String(bytes, "UTF-8");
	logger.info("使用UTF-8解码并转为Unicode字符串：{}", s1);
	b1 = s1.getBytes();
	logger.info("使用UTF-8编码：{}", toHexStr(b1));
	logger.info("使用GB18030解码并转为Unicode字符串：{}", new String(b1, "GB18030"));
} catch (UnsupportedEncodingException e) {
	e.printStackTrace();
}
```

输出为：

```shell
22:55:02 [main] INFO : 当前JRE版本：1.6.0_14
22:55:02 [main] INFO : 当前默认字符集：UTF-8
22:55:02 [main] INFO : 使用ISO-8859-1编码：0x550x540x460x2D0x380x3F0x3F
22:55:02 [main] INFO : 使用UTF-8解码并转为Unicode字符串：UTF-8??
22:55:02 [main] INFO : 使用UTF-8解码并转为Unicode字符串：��
22:55:02 [main] INFO : 使用UTF-8编码：0xEF0xBF0xBD0xEF0xBF0xBD
22:55:02 [main] INFO : 使用GB18030解码并转为Unicode字符串：锟斤拷
```

可以看到在第1节代码中，当对Unicode字符串编码时，遇到ISO-8859-1没有定义的字符，就用`0x3F`（`?`）替代了；在第2节代码中，字节串`0xC00xC0`不是合法的UTF-8编码结果（因为对于2字节的UTF-8编码，第1字节应在`C0-DF`范围内，第2字节应在`80-BF`范围内），又被替换为`U+FFFDU+FFFD`这两个Unicode字符，再用UTF-8编码即变为`0xEF0xBF0xBD0xEF0xBF0xBD`，在中文环境下输出就出现了[著名的](http://baike.baidu.com/view/2638658.htm#sub2638658)锟斤拷（`0xEF0xBF`为锟，`0xBD0xEF`为斤，`0xBF0xBD`为拷）。

而Python语言在字符串编码问题上则显得更安全，在编码/解码时如果遇到不能解释的内容，不是盲目替换，而是抛出异常：

```python
# -*- coding: utf-8 -*-

str = u'UTF-8字符';
bytes = '\xC0\xC0'

try:
    b1 = str.encode('ISO-8859-1')
except UnicodeEncodeError:
    print u'无法使用ISO-8859-1编码：%s' % (str)

try:
    s1 = bytes.decode('UTF-8')
except UnicodeDecodeError:
    print u'无法使用UTF-8解码：%s' % (toHexStr(bytes))
```

输出为：

```shell
C:\>python test_string.py
无法使用ISO-8859-1编码：UTF-8字符
无法使用UTF-8解码：0xC00xC0
```
