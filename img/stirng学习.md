- string是c++中的一个数据结构他并不属于STL，在STL出来之前他就已经被设计出来了。它本身就是我们传统意义上的串(字符数组)，与C语言不同他不需要我们来担心扩容问题，底层函数设计的时候已经封装好了，我们可以非常方便的使用。

在日常生活中，string使用的非常频繁，例如我们写一段话，说一个词，以及记录大数字等等都会使用到string。

![img](https://nw3kdl6c06y.feishu.cn/space/api/box/stream/download/asynccode/?code=Y2ZmZGZiMGY3Y2EwZTU2YzhlNTA3MDI5YWNmYTM2M2ZfQmNlbHZnVEJwQ1JGbUFodDAxalA5OHBnQ1FLSWZwSEdfVG9rZW46TkVkcmJndWlBb09ZNWR4Y2RiM2NrV0lXbkdoXzE3NTQ0NDQ4OTk6MTc1NDQ0ODQ5OV9WNA)

- 如上图，既可以表示英文字母，也可以表示汉字。

# 编码方式

[从这个网站中可以看到c++的标准库](https://legacy.cplusplus.com/)

![img](https://nw3kdl6c06y.feishu.cn/space/api/box/stream/download/asynccode/?code=NzI2ODczODY2NzgzYjFmODIyM2RjYjllMjVmNzNkZWFfSTZIRTZDRWJEN2gyWGJ4cmNzN1JwTklUU2doeDgzUVhfVG9rZW46S0NMV2IwUGI3b1lGYlN4V3V3VmNUTWVkbjFjXzE3NTQ0NDQ4OTk6MTc1NDQ0ODQ5OV9WNA)

- 如上图string的是适配UTF-8编码格式的，那么utf-8编码格式是什么东西呢? string适配他干什么呢？

那我们就需要简单了解一下编码的由来了：

- 计算机是有美国那边发明的，但是计算机内部只能表示01序列，那么如何表示像"abcd"这样的字母呢? 可以把每一个字母/符号/数字进行编码，每一个特定的数字都对应一个字符，所以就有了**ascall编码**。
- 随着时代的发展，不止一个国家使用计算机，其他国家的如何表示呢? 而且美国的字母就那么写个，所以使用1个字节的ascall编码是可以表示完全的，就以我们国家为例子，光是汉字都上万了， 那么一个字节很明显是不够用的。况且世界上那么多国家，那么如何表示所有国家的字呢? 所以就推出了**unicode编码。**

![img](https://nw3kdl6c06y.feishu.cn/space/api/box/stream/download/asynccode/?code=MjNlZGZhNWE1NDlhYWU0MDI0ODhiMTgyYjEyNmYxMDFfVkdWWXU1RTA2ZGVBU3pRcFBRRW1XeXZhdFN1RERUUjVfVG9rZW46S3dlZ2JDTHpUb2R0Y2J4cWN0MGN3WG40bkZmXzE3NTQ0NDQ4OTk6MTc1NDQ0ODQ5OV9WNA)

而unicode编码由有三种编码方案：UTF-8,UTF-16.UTF-32。这里我们简单了解一下即可，utf-16是16位无符号整形，utf-32是32位无符号整形，那么utf-32就可以表示42亿多种不同的字。

而utf-8可不是单字节，而是变长字节：

![img](https://nw3kdl6c06y.feishu.cn/space/api/box/stream/download/asynccode/?code=Y2I4ZGVhNmYwYTVkMTkzNDk1NjlkODRkZWNmNjJmMmRfSGpyT08xZVZKazN6akR0QnJmVVZ5S2pRYVRXRVhXaGRfVG9rZW46T0taYmJrQnJHb2o5TDd4NGhNbmNuZU5RbmtjXzE3NTQ0NDQ4OTk6MTc1NDQ0ODQ5OV9WNA)

如上图，通过第一个字节的前几个bit位来确定到底是哪种编码位。这样的好处就是并不是每一个字都是2字节或者4字节，**依据他使用的范围而定，比较节省空间**。所以string适配的是这种编码方式。

![img](https://nw3kdl6c06y.feishu.cn/space/api/box/stream/download/asynccode/?code=MGQ1ZDM3NWQ4YzdhZWU2YmI1MDVhNzAwODcwOWE3MGNfWmEzUzJHWXZ0V0xPM3RGeEo4OHdSSXRTUURXVVhMU1pfVG9rZW46VEI2aWJMZEpjb1VRb3R4ZjRNb2NQd3RZbnZkXzE3NTQ0NDQ4OTk6MTc1NDQ0ODQ5OV9WNA)

- string依赖的是basic_string，string其实就是一个模版类，c++标准库中还提供了其他字节的string类。

# String 使用

- 在这一部分我不会讲解全部的函数，只是某些常用的而已。
- 构造函数
- 迭代器与数组访问的区别? 迭代器的好处!
- 迭代器的简单实现

## 构造函数

![img](https://nw3kdl6c06y.feishu.cn/space/api/box/stream/download/asynccode/?code=ZTBmMTdlMzMwMDgyMDA0YTNiZjdlNjhjNjAzYzI3YzRfenN6WUVIRGhXcVVselQ5azBTUW0wc09UVTZJUlAyb3FfVG9rZW46UmZ0MmIyZlo5b1ZwcFp4MHJTbWN0VEhobmhmXzE3NTQ0NDQ4OTk6MTc1NDQ0ODQ5OV9WNA)

![img](https://nw3kdl6c06y.feishu.cn/space/api/box/stream/download/asynccode/?code=ZjA3ZDdlMjgzNTkxNjFjNDZjNzJkNGQxNzg4MDE3NmVfZDJDcm5RaU5jeGFtWVBDUU1zaTFoVnB6RTNUSVlQaVZfVG9rZW46TTlITGJsYXlGb0l0VmF4amtYcmNJY2xrbkxtXzE3NTQ0NDQ4OTk6MTc1NDQ0ODQ5OV9WNA)

## string的大小

![img](https://nw3kdl6c06y.feishu.cn/space/api/box/stream/download/asynccode/?code=MGFjNGQ0ZDQ2MDEwMGQ1ZTllZTQzZmRiY2Q4YWYwYTBfa0pSWUlXS2dsV2NqajRmZFRsa3M1QTRSNGFHWnV6R1JfVG9rZW46RFJGNWJHM0FabzBxS3V4WWJQYWNXR2VBbnhkXzE3NTQ0NDQ4OTk6MTc1NDQ0ODQ5OV9WNA)

![img](https://nw3kdl6c06y.feishu.cn/space/api/box/stream/download/asynccode/?code=MTY5NDU4YzU5OTY5YjAyYjRmOWJhOTE5NDkyNTgwZGFfZUFBQ0dJZzd6VUd4NWNRVGJ1VjBBdFZFZVlqUWg0NGRfVG9rZW46WWFnVGJOOG1HbzlUd0F4VDU4M2N1UmhNbnlwXzE3NTQ0NDQ4OTk6MTc1NDQ0ODQ5OV9WNA)

## capacity()函数

![img](https://nw3kdl6c06y.feishu.cn/space/api/box/stream/download/asynccode/?code=OThkMTc2YzBmMjE5OWYzMTc0YjNkODRhNGU2ZTMzZWJfbkFVVmkxbUxXalFTMVpsemlkMllFeDdESFRvTm92ekRfVG9rZW46VXBsZGJzRWhGbzhUbWl4WTQwSWMzWEg4blViXzE3NTQ0NDQ4OTk6MTc1NDQ0ODQ5OV9WNA)

- capacity表示的是向系统申请的空间大小而不是我们子串占用的大小。
- 手册上也说了这个实际已申请的空间大小不一定需要等于实际size大小。在额外空间需要添加字符或子串的时候可以等于或者大于。
- 这样是为了节省效率，开辟空间是有消耗的，需要通过系统调用向系统申请空间。实际 大于等于 实际字符的个数，这个在不同系统实现的方式不一样，例如在windows系统中默认是开辟15个空间大小，如果我们需要16个字节大小的内容，那么就会在默认15直接空间中多开辟16个字节也就是31个字节大小。

![img](https://nw3kdl6c06y.feishu.cn/space/api/box/stream/download/asynccode/?code=NzljY2I1MTNkYzQ3YjAyN2Y5YmY0YjE2YzkwNmFiNGJfQ0JyQ0Uwbm9qaEoyTms1b0duWmpBOGt5Q0xLTjJmTDZfVG9rZW46UENZeGJ2MVVCb3NZS2x4akh0NWNCN1BmbnVlXzE3NTQ0NDQ4OTk6MTc1NDQ0ODQ5OV9WNA)

![img](https://nw3kdl6c06y.feishu.cn/space/api/box/stream/download/asynccode/?code=YmMwNjdlNTQ5MjFlMjg4NTA0ZTg4YTQxZGE2ZDFmMjdfMzEybjZuNDY1VUdUeHpvT1ZJRVNZV2drcEFmdDhYQ3NfVG9rZW46R05IemI4U2pFb3NNbEV4eUxMWmNubk9EbnJjXzE3NTQ0NDQ4OTk6MTc1NDQ0ODQ5OV9WNA)

## string的遍历方式