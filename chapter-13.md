# Chapter 13



False Positive: 他说是对的，不一定是对的

False Negative: 他说是错的，不一定是错的



Q:

![](<.gitbook/assets/image (12).png>)

A: B C D E H

Big Table 上的数据，最终都会被存储在 GFS 中。但是因为 Big Table 是主要优化写（写多），GFS 是主要优化读（读多），因此 Big Table 的数据并不会马上就写到 GFS 里，而是积累了一定的数据之后，再批量的写入 GFS。



Q:&#x20;

![](<.gitbook/assets/image (17).png>)

A: A C D E

描述数据的数据是MetaData(元数据)，A Ｃ　ＤＥ是描述文件的数据，而Ｂ是文件它本身（数据本身）



Q：![](<.gitbook/assets/image (72).png>)

A：A B D E

BigTable之所以使用跳跃表，是因为我们需要支持快速的插入和查找，堆是不支持查找的，更加不支持找比某个数大的最小值。这里红黑树和跳跃表都能够做到 LogN 的插入和查找，且在需要有序导出所有数据的时候，都能够在 O(N) 的时间内快速导出。跳跃表唯一的缺点是需要分层记录节点，会耗费比红黑树更多的空间。但是优点是当多线程并发的时候，红黑树因为需要 rebalance，会锁住更多的节点，并发效率不如跳跃表高。更多跳跃表的原理介绍，请见知识点视频。

\




Write Ahead Log(WAL)



TODO:

{% embed url="http://www.larsgeorge.com/2010/01/hbase-architecture-101-write-ahead-log.html" %}

{% embed url="https://en.wikipedia.org/wiki/B-tree" %}

{% embed url="https://www.jianshu.com/p/0371c9569736" %}

Problems:

{% embed url="https://www.lintcode.com/problem/486" %}
486 · Merge K Sorted Arrays
{% endembed %}

{% embed url="https://www.lintcode.com/problem/556" %}
556 · Standard Bloom Filter
{% endembed %}
