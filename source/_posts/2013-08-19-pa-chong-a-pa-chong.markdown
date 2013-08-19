---
layout: post
title: "爬虫啊爬虫"
date: 2013-08-19 13:59
comments: true
categories: Python
---
作为一个Python玩家，爬虫可以说是不得不会的基本功。趁着找工作的需求，学写个BYR论坛招聘信息的爬虫
- - - 
###第三方Python包
-   Request:Requests包可以代替urllib2库抓取网页信息。正如介绍所说，Requests——HTTP for Humans，Requests比urllib2库更为简洁
-   BeautifulSoup:BeautifulSoup包用于HTML标签的分析，可以避免复杂的正则表达式
-   Redis:Redis是一种NoSQL，用于存放抓取的招聘信息
- - - 
###网页信息获取
```
r = requests.get(host+board+pages, headers=headers)
```
首先，先调用requests包的get函数取得网页信息。由于BYR论坛采用动态网页加载，需要加上XMLHttpRequest以取得完整内容。

###标签分析
```
soup = BeautifulSoup(r.text)
info = soup.findAll('a', href=re.compile(r"/article/JobInfo/\d+"), title=None)
```

利用beautifulsoup包对网页源码进行解析，取得帖子的地址与标题。

```
for i in info:
    if i.parent.parent.get("class") == "top":
        continue
    else:
        url = host + re.findall(href, str(i))[0]
        title = re.findall(r'>(.+)<', str(i))[0]
```

通过css属性将置顶帖过滤，并将地址补全
###信息储存

```
add('url', url+'   '+title)
```

将取得的信息存到redis的集合(sets)中，可以避免重复

###总结
这还只是一个初步的抓取功能，后续还需完善信息显示与关键词过滤等功能。

网络爬虫是一个十分实用的工具，值得好好研究。
