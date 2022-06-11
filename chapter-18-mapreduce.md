# Chapter 18 MapReduce

再补充几个常见的 QA:

Q: Reduce 之后各个key还是可能会在不同地方，那么怎么再把这些 reducer 的结果 sort 并放在一起呢？\
A: Reducer 的结果在全局是不 sort 的。因为很多计算场景下计算结果不需要 sort。如果有 sort 的需求，可以使用外排序算法（External Sorting）进行排序即可。



Q: 系统设计中 map reduce 的问题会以什么形式问？

A: 90% 的概率会问使用 map reduce 来解决比较重的计算问题。10% 的概率会问 map reduce 的原理是怎么样的。所以好好做今天的编程题作业非常重要！



Q: Reduce 的过程全部都在内存里么？是否会装不下？&#x20;

A: 不是的。Reduce 的过程，key 是在内存里的，value list 通常在代码中是一个 iterator 的形式，也就意味着，有可能是从文件里读进来的。很显然全部放在内存肯定是放不下的，特别是对一些很 hot 的 key。



到此为止呢，Google 的三驾马车已经学完了，不知道你是否有收获呢？三驾马车里，GFS 是其他两个系统的基础，是重中之重需要掌握的。Big Table 的设计原理更是直接被当做面试题在多家公司的面经中出现过。Map Reduce 如果你不是面试 Big Data Engineer 的岗位的话，直接问到的概率不是特别大，但是在算法面试中，特别是 Google 的算法面试中，很多时候会出现可以用 Map Reduce 来解决的问题，特别是 Top K Frequent Elements 这个高频算法面试题。如果你能在这类面试中使用 Map Reduce 来解决问题，一定会拿到 Strong Hire ！



Q：

![](<.gitbook/assets/image (75).png>)

A：C

Map 的机器如果没有全部执行完，任何一台 Reduce 的机器所负责的数据段都有可能还有更新。因此 Reduce 的部分是不可以开始的。但是机器可以先启动执行一些程序的初始化操作是可以的。



Q：

![](<.gitbook/assets/image (48).png>)

A: B C E F



Q:

![](<.gitbook/assets/image (28).png>)

A： A C



Problem：&#x20;

499

504

503

549

554

537







