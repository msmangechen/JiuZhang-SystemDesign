# Chapter 10 分布式文件系统 GFS

## Blackboard

大家好，今天我带着大家一起学习 Google 的三驾马车的：GFS，这可是 Google 的技术立身之本哦！虽然已经很有历史了，但是优秀的技术依然是经久不衰的。学习三驾马车，不仅仅能应对一些公司中直接让你设计分布式系统的原题，也能让你借鉴其中的一些设计理念去设计其他的系统问题。



Q:&#x20;

![](<../.gitbook/assets/image (79).png>)

A: B C E

GFS 采用的是 Master-slave 的架构。他的一些基本设计原理，如 chunk 的设计（对应文件系统中的 block）和普通文件系统是相通的。整套系统的设计是基于一些合理假设的（这些假设都是Google从大量工程实践中总结出来的），其中一条假设就是：“We expect a few million files, each typically 100MB or larger in size"。如果实在需要存很多小文件的话， 其实可以将这些小文件打包成一个大文件然后再存储，只要记录下每个小文件在文件内部的起始字节和大小就行了。



Q:

![](<../.gitbook/assets/image (22).png>)

A: B

这个题大部分同学都会答错，你答对没有呢？硬盘厂家的标准是十进制，而计算机系统中使用的是二进制。所以在硬盘的领域里，1P = 1000T, 1T = 1000G，1G = 1000M。因此你买的 1T 的硬盘在计算机中查看大小时，实际只有 931G。祝黑心硬盘厂家们早日倒闭！



在 Design Lookup Service 这个题中，和我们所学的 GFS 的设计又有什么联系呢？如果你仔细分析不难发现，我们将所有的 key 存储在内存中，将所有的 value 存储在硬盘上的形式，是不是正如我们将所有的 chunk 的 metadata 存储在 master 上，将 chunk 的具体内容存储在 chunk server 上一样？因此，很多系统设计的思想都是相通的，深入理解了这些经典系统的设计原理，解决其他的问题就游刃有余了。



下面分享一道 Facebook 的面经题（详细的解答见下面的文档）：\
如何上传一个很大的系统文件(10G)到很多的 Servers (10k)上， 并且在更新 Servers 后保证系统良好运行。



Q:

![](<../.gitbook/assets/image (2).png>)

A: B D

False Negative 是指 check sum 认为是没问题的，但是可能存在问题。这个是会发生的，比如 1,4 两个数据，check sum = 5，但是 2 + 3 也是 5。所以 check sum 相同不能证明数据一定没有发生变化。但是 check sum 不同就表示原始数据肯定发生了变化。因此 check sum 是存在 False Negative 但不存在 False Positive 的。

\
Q:

![](<../.gitbook/assets/image (40).png>)

A: 一般来说，我们在设计中不要做任何定期扫描全部数据的事情，这个工作量太大了，且很多工作无意义。最好的还是 lazy loading，即用户请求的时候才去计算

### Problem

566
