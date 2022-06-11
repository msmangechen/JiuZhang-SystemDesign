# Chapter 9 数据库拓展与一致性哈希算法

系统设计中考核的很重要的一部分内容就是对数据库的了解程度。因此无论是使用数据库也好，还是理解数据库的一些机制也好，都十分的重要。在 4S 分析法中的第 4 个 S，也就是 Scale，通常就是再问如何 Scale Database。而 Scale Database 最核心的部分就是数据库的拆分（Sharding）。今天我会带你来深入这一块的知识。

\
Q:

![](<.gitbook/assets/image (54).png>)

A: A C D



Q:

![](<.gitbook/assets/image (56).png>)

A: A C E G H



Q:

![](<.gitbook/assets/image (85).png>)

A: B D

Consistent hashing 和 Load Balancing 不是一个意思。Consistent hashing 会让同样的 Request 去同一个 Server，Load Balancing 可能会让同样的 Request 去不同的 Server。

Web Server 上只存代码不存数据，是 stateless 的，更适合 Load Balancing。而 Database 上存数据，且我们希望每个 Database server 能拆分开存储所有数据，因此 Database 是 stateful 的，更适合 Consistent Hashing。当然如果你想把 Consistent Hashing 用在 Web Server 也是可以的，这样的好处是有时候 Web Server 上会有一些 Local Cache 用与降低 cache miss，那么同样数据的请求经过同一个 Web Server 会更好。



Q:

![](<.gitbook/assets/image (73).png>)

A: A

根据数据的新旧程度来拆分的话，新数据的访问次数比旧数据的访问次数是要明显多的，会导致数据访问不均匀的问题。 这种方法并不会导致存储不均匀，最多只有最新的一台机器的数据相对少一些，其他的机器都还是均匀的。也不会导致不知道数据去哪台机器取，比如根据 id 来拆分，0\~99在1号机器，1-199 在2号机器的话，根据 id 可以算出对应的机器是哪个。



Q:

![](<.gitbook/assets/image (30).png>)

A: A



Q:

![](<.gitbook/assets/image (25).png>)

A: A

Heap 只能找全局最大最小。



Q:

![](<.gitbook/assets/image (90).png>)

A: A C E

Backup 一般一天做一次，但是这个完全是因人而异，不是强制的。 Backup 存储的是离线数据，无法分摊在线读请求。 虽然 Replica 很强大，但是 Backup 也是很有必要的，可以认为是一个双保险。且可以服务于一些离线数据计算，这样不会给在线数据库带来压力。



Q:

![](<.gitbook/assets/image (24).png>)

A: B



Q:

![](<.gitbook/assets/image (14).png>)

A: A



还记得 News Feed 是什么么？News Feed 是指我关注的人的信息流汇总，也就是你朋友圈里看到的数据。News Feed Table 大概有如下一些 columns：

```
id - primary key， 系统自动生成的unique id
owner_id - Foreign key，放在谁的 news feed 里
post_id - Foreign key，帖子的 id
posted_by_user_id - Foreign key，谁发的
created_at - timestamp，啥时候发的，用于排序
...
```

Timeline 是某个人发的所有的帖子的汇总。就是点到某个人的朋友圈以后看到的他/她发的所有帖子。TImeline 其实就是 Post Table 按照时间排序，里大致有如下一些 columns:

```
id - primary key，系统自动生成的 unique id
user_id - foreign key， 谁发的
content - text，发了啥
created_at - timestamp，啥时候发的
...
```

如果你不太记得了，就去第一节免费试听课《设计新鲜事系统 Design News Feed System》里再看看吧



这节课的主要内容就讲到这里了，不知道你是否对什么是数据库的拆分有了更深入的了解呢？本节课的学习难点是 Consistent Hashing 这个算法，你可以再反复学习一下这个部分的内容，也可以看一些网上的相关介绍材料进行补充。下面是我为大家筛选的一些有用材料：

1. [https://afghl.github.io/2016/07/04/consistent-hashing.html](https://afghl.github.io/2016/07/04/consistent-hashing.html)
2. [http://blog.codinglabs.org/articles/consistent-hashing.html](http://blog.codinglabs.org/articles/consistent-hashing.html)
3. [https://juejin.im/entry/6844903478171533320](https://juejin.im/entry/6844903478171533320)



给同学们讲了很多跟数据库有关的知识了，是时候开始做一些真正的实战练习了。在后面的补充内容中，会讲解两个高频的系统设计问题，《设计访问限制器 RateLimiter》和《设计Datadog》，尤其是访问限制器，既可以作为算法面试题又可以作为系统设计面试题。



Rate Limiter其他算法的做法： https://mp.weixin.qq.com/s/Uk90GWr6VQdPQJr7hJE4wg



有一个开源的 Datadog，叫做 [Graphite](https://graphiteapp.org/)，是很多厂家用的数据收集系统。如果感兴趣你可以在网上搜一下关于 Graphite 的更多的内容，也可以自己下载来搭建一个试试看。配合前端的数据显示软件 [Grafana](https://grafana.com/) 会更好。



Problem:

128&#x20;

519

520

526

215

505
