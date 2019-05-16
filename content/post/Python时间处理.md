+++
title = "Python时间处理"
date = 2019-05-16T12:24:16+08:00
draft = false

# Tags and categories
# For example, use `tags = []` for no tags, or the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = ["Python","时间"]
categories = ["Python"]

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
[image]
  # Caption (optional)
  caption = ""

  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = ""
+++

# Python 时间处理

一共有三个时间模式。`date()`, `time()`,` datetime()`。此外还有处理**时间间隔的**`timedelta()`

## 获取当前

```python
import datetime
datetime.date.today() # 今天的日期
dateitme.datetime.now() # 此刻的时间
```
注意，以上两个返回的类型是`date类型`和`datetime类型`，而不是字符串。如果要返回字符串，则需要进行格式化。

> datetime.date(2019, 5, 16)
> datetime.datetime(2019, 5, 16, 12, 10, 49, 766690)
> 

## 格式化

格式化输出一般有两种，一是通过`.strftime()`进行格式化。而是使用`ISO`的格式。

```python
datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S") 
```
Y, m, d, H, M, S均有特定含义。这和print()中的格式化输出很像。

```python
datetime.datetime.now()
```
使用的是ISO的格式。

> '2019-05-16T11:56:33.151694'
> 

## 时间戳

时间戳是指格林威治时间1970年1月1日0时0分0秒到此刻的**总秒数**。

两个问题：

- 千年虫问题。一些程序员会把`1986`这样的年份，记为`86`。
- 2038问题。32位计算机最多存储到40亿，到2038年左右，秒数将超过40亿。于是使用32位时间戳的计算机会溢出。

两个方法：

- timetuple() 把日期时间转换成``struct_time``格式。
- 再使用time.mktime()转成时间戳

```python
today = datetime.date.today()
today.timetuple()
```

> time.struct_time(tm_year=2019, tm_mon=5, tm_mday=16, tm_hour=0, tm_min=0, tm_sec=0, tm_wday=3, tm_yday=136, tm_isdst=-1)

以上时间的格式就是struct_time

```python
time.mktime(today.structtuple())
```

> 1557936000.0

这个值就是秒数

## 时间段（计算）

前几节所有介绍的都是关于`时间点`， 时间点之间可以相减，得到时间段。

```python
today = datetime.datetime.now() # 获取当前日期时间
yesterday  = today - datetime.timedelta(days=1)

# 减去一天的时间间隔
```
同样timedelta() 还可以指定 hours等参数