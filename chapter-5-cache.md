# Chapter 5 Cache

Q:

![](<.gitbook/assets/image (13).png>)

A: C



Q:![](<.gitbook/assets/image (21).png>)

A: A B C

Memcached 不能持久化存储数据，不适合用来存储用户信息



Q:

![](<.gitbook/assets/image (20).png>)

A: B C

缓存的目的是让访问变得更快。文件系统的访问比网络访问快，一些耗时很长的计算得到的结果也可以缓存在文件中，但是文件系统的访问速度和数据库的访问速度基本上是差不多，所以一般不会用文件系统来做数据库的缓存，意义不大。



Redis和Memcached整体对比

1. 性能对比：由于Redis只使用单核，而Memcached可以使用多核，所以平均每一个核上Redis在存储小数据时比Memcached性能更高。而在100k以上的数据中，Memcached性能要高于Redis，虽然Redis最近也在存储大数据的性能上进行优化，但是比起Memcached，还是稍有逊色。
2. 内存使用效率对比：使用简单的key-value存储的话，Memcached的内存利用率更高，而如果Redis采用hash结构来做key-value存储，由于其组合式的压缩，其内存利用率会高于Memcached。&#x20;
3. Redis支持服务器端的数据操作：Redis相比Memcached来说，拥有更多的数据结构和并支持更丰富的数据操作，通常在Memcached里，你需要将数据拿到客户端来进行类似的修改再set回去。这大大增加了网络IO的次数和数据体积。在Redis中，这些复杂的操作通常和一般的GET/SET一样高效。所以，如果需要缓存能够支持更复杂的结构和操作，那么Redis会是不错的选择。



Q:

![](<.gitbook/assets/image (50).png>)

A: A B C D&#x20;



Q:

![](<.gitbook/assets/image (49).png>)

A: C

不可能。程序的执行是顺序执行的，第一个语句执行出错以后，第二个语句就不会执行了，用户会收到整个 setUser 操作失败的信息。



Q:

![](<.gitbook/assets/image (8).png>)

A: A B C

多机器的话自然而然也是多进程的。



Q:

![](<.gitbook/assets/image (82).png>)

A: B

加锁以后只能保证在同一个数据上的操作顺序执行，但是无法执行“回滚”，也就是说如果第一个操作成功，第二个操作失败了，也会导致数据的不一致。 另外互斥锁（mutex）是多线程内共享的，多进程内无法共享。如果要加锁，只能使用分布式锁，比如 Zookeeper，但是这会导致读取效率急剧降低。得不偿失。



Q:

![](<.gitbook/assets/image (44).png>)

A: D

hit rate = cache hit / (cache hit + cache miss)



Q: ![](<.gitbook/assets/image (70).png>)

A: A

通常用UUID来作为Session Key(Session Token)，UUID(Universal Unique ID): UUID是由一组32位数的16进制数字所构成，所以UUID理论上的总数为16^32=2^128，约等于3.4 x 10^38。也就是说若每纳秒产生1兆个UUID，要花100亿年才会将所有UUID用完。所以通俗的称之为宇宙爆炸都不会出现重复的ID字段。



Q:

![](<.gitbook/assets/image (29).png>)

A: B

首先 Cookie 的大小 HTTP 协议是有限制的。其次因为每次 Request 都要带上 Cookie 里的内容，因此 Cookie 里存的东西是越少越好而不是越多越好。



Q:&#x20;

![](<.gitbook/assets/image (83).png>)

A: B

做 lazy loading 就好了。因为有 expire\_at，无需主动删除，被动删除即可，即在用户登陆的时候发现过期了再删。



Q:&#x20;

![](<.gitbook/assets/image (69).png>)

A: C



Q:

![](<.gitbook/assets/image (61).png>)

A: A

查询 A 的所有好友不会变慢，因为依然是 select \* from friendship where user\_id1=A or user\_id2=A。



Q: ![](<.gitbook/assets/image (39).png>)

A: B



Q:![](<.gitbook/assets/image (86).png>)

A: A B C



Q:![](<.gitbook/assets/image (77).png>)

A: B



Q:![](<.gitbook/assets/image (64).png>)

A:B C D E

多元组比较大小时，先比较第一项的大小，当第一项相等时比较第二项的大小，以此类推。 比如 (1, 100) 和 (2, 1) 进行比较，这两个多元组的第一项分别是1和2，因为1 < 2，所以 (1, 100) < (2, 1)。如果第一项相等，比如 (1,2) 和 (1,3) 进行比较，因为第一项相等，所以比较第二项，因为2 < 3，所以 (1,2) < (1,3)。 A选项和（1,2）比较，第一项相等，第二项小于2，故不满足； B，C，D选项和（1,2）比较，第一项相等，第二项大于等于2，和（2,3）比较，第一项小于2，不必比较第二项，故也满足； E选项，和（1,2）比较，第一项大于1，和（2,3）比较，第一项相等，第二项比3小，故满足。 F选项，和（2,3）比较，第一项大于2，故不满足。 因此（1,2），（1,3），（1,4），……，（2,3），（2,2），（2,1），……都是正确的column。



让我来考考你有没有掌握今天所学的 session 和 cookie 的知识。如果一个用户没有进行登录或者注册，如何识别两次 Request 来自同一个用户呢？（认真思考 1 分钟再继续哦！）

你是不是想说，可以根据 IP Address？

错！IP Address 是不可以的，因为在同一个局域网下的不同用户会共享同一个对外的 IP Address。

正确的做法，是为用户生成一个 uuid （Universal Unique ID）作为他的标识，有很多库函数可以生成这个 uuid，这是一个字符串，可以认为不同的用户一定会生成不同的 uuid。服务器端生成这个 uuid 之后返回给浏览器端，浏览器端存储在 cookie 里，之后每次请求都会带上。如果服务器发现 cookie 里没有这个 uuid 就说明可能是一个新用户，就为其分配新的 uuid，否则不改变这个 uuid。这样我们就可以用 uuid 来识别一个未登录的用户了。

这样的方法如果你清空 cookie 或者换了浏览器以后，可能会被分配到一个新的 uuid，那么你之前的 requests 和之后的 requests 就可能会被服务器识别为两个不同的用户。这个是没有办法解决的了。因为神仙也无法知道你换了浏览器以后坐在电脑前的是不是还是你自己。



Problem\
134

560

502

538
