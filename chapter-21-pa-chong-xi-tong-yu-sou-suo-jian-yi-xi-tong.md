# Chapter 21 爬虫系统与搜索建议系统

Q:

![](<.gitbook/assets/image (27).png>)

A: C



Q:

![](<.gitbook/assets/image (19).png>)

A: A

为了对网页进行分析，解析出链接信息，标题信息等，我们是需要保存整张网页的，而不只是纯文本内容。



当用户搜索 Hello World 的时候，搜索引擎会去倒排索引中检索 Hello 和 World 共同出现的文档有哪些，并且求出交集。一个相关的面试考点就是如何求两个有序数组的交集。



Q:

![](<.gitbook/assets/image (57).png>)

A: B



Q:

![](<.gitbook/assets/image (23).png>)

A: B

下载效率还受限于 CPU 个数和带宽。2000 个进程会导致大量的进程上下文切换（Context Switch），从而导致代码运行效率下降。





Q:

![](<.gitbook/assets/image (74).png>)

A: B



Q:

![](<.gitbook/assets/image (9).png>)

A: A E



Q:

![](<.gitbook/assets/image (7).png>)

A: B



Q:

![](<.gitbook/assets/image (43).png>)

A: D



这是知乎的 robots 协议：[https://www.zhihu.com/robots.txt](https://www.zhihu.com/robots.txt)\
更多的关于 robots 协议的规则感兴趣的话可以看看 [https://baike.baidu.com/item/robots/5243374?fr=aladdin](https://baike.baidu.com/item/robots/5243374?fr=aladdin)



指数补偿(Exponential Backoff)指的是，在执行事件时，通过反馈，逐渐降低某个过程的速率，从而最终找到一个合适的速率（来处理事件）。

指数补偿通常用于网络和传输协议，比如在进行网络连接时，如果第一次请求失败，那么可以等待 _t1_ 秒之后重试，如果再次请求还是失败，那么等待 _t2_ 秒之后重试。重试可以一直继续下去，直到等待次数或等待时间超过特定值为止。

等待的时间 _ti_ 是可以自由指定的，常用 1, 2, 4, 8 这样的指数序列，因此叫指数补偿。

类似的用到了指数补偿思想的场景还有动态数组（C++ 里的vector，Java 里的 ArrayList，Python 里的 list），动态数组之所以支持你不断的往里加入新元素，就是因为当一个数组满了以后，会再创建一个新的两倍元原来大小的数组来替换掉旧数组。

关于爬虫的知识点我们就讲到这里了，今天所讲的知识已经远远足够应付系统设计的面试了。如果感兴趣进行实践的同学，可以看一下下面这个链接中的文章，这个文章的作者用 20 台 AWS 的机器在 40 小时内抓取了 2.5亿篇网页，只花了 580$。

[http://www.michaelnielsen.org/ddi/how-to-crawl-a-quarter-billion-webpages-in-40-hours/](http://www.michaelnielsen.org/ddi/how-to-crawl-a-quarter-billion-webpages-in-40-hours/)

这篇文章中很多的内容是值得参考的比如如何拆分爬取任务的部分，作者的目的是单纯的抓取网页，和我们今天所设计的爬虫相比自然是我们课上讲的架构会更加适合一个真正的爬虫系统。



Q:

![](<.gitbook/assets/image (87).png>)

A: A



Trie 的原理和实现是面试者必须要掌握的，你可以通过下面这个 LintCode 上的练习题进行学习。另外在《九章算法强化班》中，我们也针对这类数据结构及面试中可能会出现的问题进行了更详细和全面的介绍。大家可以在这个班中学到更多与 Trie 有关的知识。



如果你不太理解 1/10000 的概率筛选这个部分的意思的话，这是用 Python 写的伪代码，

```
class QueryService():
    @classmethod
    def should_log():
        return random.randint(0, 9999) == 0

    @classmethod
    def log_query(cls, query):
        if cls.should_log():
            database.query_count_plus_one(query)
```



Prefetch 之前的 http response 可能是这样的：

```
{
  "prefix": "ap",
  "top10": [
    "app store",
    "apple",
    ...
  ]
}
```

有了 prefetch 以后，http response 可能就是这样的：

```
[{
  "prefix": "ap",
  "top10": [
    "app store",
    "apple",
    "amazon",
    ...
  ],
}, {
  "prefix": "app",
  "top10": [
    "app store",
    "apple",
    "apple id",
    ...
  ],
}, ...
]
```



好了，这就是我们这节课的内容了，我们系统架构互动课的课程也到此结束了。最后，希望和你强调几点：

1. 4S分析法很重要，能帮助你有效的分析系统设计问题，但面试时不必拘泥这种分析形式
2. 系统设计最重要的一点就是要学会 Tradeoff，学会分析和比较不同的方法的优劣
3. 要注重 99% 的用户体验，1%的用户很多时候可以忽略
4. 系统设计面试中虽然基本不会让你写代码，但是这门课程要求大家通过写代码的方式去消化我们在课上所学的知识。



Problem:

547

107

582

442

234

1787
