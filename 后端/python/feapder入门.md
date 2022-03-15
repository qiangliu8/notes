# feapder入门

## 框架Feapder介绍 

​      **feapder** 是一款简单、快速、轻量级的爬虫框架。起名源于 fast、easy、air、pro、spider的缩写，以开发快速、抓取快速、使用简单、功能强大为宗旨，历时4年倾心打造。支持轻量爬虫、分布式爬虫、批次爬虫、爬虫集成，以及完善的爬虫报警机制

### 框架流程图

![04e0a6e9e3b8ccaf92d9a74be96fee18](C:\Users\11026\Desktop\04e0a6e9e3b8ccaf92d9a74be96fee18.png)

### 模块说明

- **spider** 框架调度核心
- **parser_contronl** 模块控制器，负责调度spider
- **collector** 任务收集器，负责从任务队里中批量任务到内存，以减少爬虫队任务队列数据库的访问频率和并发量
- **parser** 数据解析器
- **start_request** 出事任务下发函数
- **item_buffer** 数据缓冲队列，批量将请求任务存储到数据库中
- **request_buffer** 请求任务缓冲队列，批量将请求任务存储到任务队列中
- **request** 数据下载器，封装了request，用于从互联网上下载数据
- **response** 请求相应，封装了response,支持xpath、css、re等解析方式，自动处理中文乱码

### 流程说明

1. spider调度**start_request**生产任务
2. **start_request**下发任务到**request_buffer**中
3. spider调度**request_buffer**批量将任务存储到任务队列数据库中
4. spider调度**collector**从任务队列中批量获取任务到内存队列
5. spider调度**parser_control**从collector的内存队列中获取任务
6. **parser_control**调度**request**请求数据
7. **request**请求与下载数据
8. request将下载后的数据给**response**，进一步封装
9. 将封装好的**response**返回给**parser_control**（图示为多个parser_control，表示多线程）
10. parser_control调度对应的**parser**，解析返回的response（图示多组parser表示不同的网站解析器）
11. parser_control将parser解析到的数据item及新产生的request分发到**item_buffer**与**request_buffer**
12. spider调度**item_buffer**与**request_buffer**将数据批量入库

## feapder使用

### feapder安装

```python
pip install feapder
```

### 创建项目

```python
feapder create -p Amazon-spider

Amazon-spider 项目生成成功
```

### 创建爬虫

```python
E:\Project\python\feapder\Amazon-spider>cd spiders

E:\Project\python\feapder\Amazon-spider\spiders>feapder create -s list_spider

ListSpider 生成成功
```

**爬虫代码如下**

```python
# -*- coding: utf-8 -*-
"""
Created on 2021-09-28 15:56:16
---------
@summary:
---------
@author: 11026
"""

import feapder


class ListSpider(feapder.AirSpider):
    def start_requests(self):
        yield feapder.Request("https://www.baidu.com")

    def parse(self, request, response):
        print(response)


if __name__ == "__main__":
    ListSpider().start()
```

### 写爬虫

#### 下发任务

```python
def start_requests(self):
    url = "https://www.baidu.com"
    yield feapder.Request(url, render=True)
```

#### 编写解析函数

观察页面结构，写xapth解析

