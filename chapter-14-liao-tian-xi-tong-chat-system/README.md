# Chapter 14 聊天系统 Chat system

Q:&#x20;

![](<../.gitbook/assets/image (46).png>)

A: ABE



Q: 在聊天软件中发送的消息，是通过 Message Queue 进行存储和传递的么？

A: 不是

消息队列（Message Queue）的用于存储和派发“任务消息”的，一个任务一般是一件做起来比较慢的事情，而不是一条具体的用户之间互发的消息。比如任务可以是“群发一条消息给 500 个人”。这个任务执行起来较慢因此需要放到 Message Queue 里，然后由某个专门执行任务的进程领取并执行。



Q:

![](<../.gitbook/assets/image (31).png>)

A: A C E



Q:

\


![](<../.gitbook/assets/image (76).png>)

A: B D F



Q:

![](<../.gitbook/assets/image (60).png>)

A: C



Q:

![](<../.gitbook/assets/image (88).png>)

A: A



Q:

![](<../.gitbook/assets/image (11).png>)

A: B C



Q:

![](<../.gitbook/assets/image (26).png>)

A: C



Q:

![](<../.gitbook/assets/image (16).png>)

A: D



Q:

![](<../.gitbook/assets/image (1).png>)

A: A



Q:

![](<../.gitbook/assets/image (52).png>)

A: D



Q:

![](<../.gitbook/assets/image (33).png>)

A: A



Q:

![](<../.gitbook/assets/image (18).png>)

A: D

因为 channel 是一个 key-value 的存储结构，value 是一个 set，支持用户上下线（增删），所以 Redis 是可以很好支持 value 是 set 的一种 key-value 结构。



Q:

![](<../.gitbook/assets/image (71).png>)

A: A C



Q: 用户关闭 APP 以后还能通过 channel service 收到提醒么？

A: 不能

不能。用户关闭 APP 以后，socket 就断开了， Push Server 会通知 channel server 将用户从对应的 channel 里移除。因此无法再通过 channel 找到这个用户并推送消息。但是用户上线以后，可以通过 MessageService 主动的 pull 得到新信息。因为 channel service & push service 都只是一个提醒的作用，而不是存数据作用。所有的信息都还是会存在 MessageService 里因此还是可以被主动获取到的。\


Q: &#x20;

![](<../.gitbook/assets/image (55).png>)

A: A B C

is\_online 可以通过 `last_updated_at` 获取到，因此不需要重复存储



Q:

![](<../.gitbook/assets/image (3).png>)

A: A

一般来说，我们在设计中不要做任何定期扫描全部数据的事情，这个工作量太大了，且很多工作无意义。最好的还是 lazy loading，即用户请求的时候才去计算



Q:

![](<../.gitbook/assets/image (62).png>)

A: CD

Message Queue 的作用是做任务纷发，Message Queue 自己不做存储。一般来说，放到 Message Queue 里的是参数信息，用一些参数来描述一个任务。一个执行任务的进程通过拿到这些参数来执行完整的任务。一般我们放到 Message Queue 里的都是执行起来较慢的任务，或者需要和外部 API 通信的任务。和外部 API 通信较慢且需要失败重试的，异步任务一般都有重试机制。

选项 A 是错误的，因为 Message Queue 不是用来做存储的。

选项 B 是错误的，因为只需要单纯的创建数据库记录，是一个和数据库的内部通信，不需要通过 Message Queue。

选项 C 是正确的，因为当一个群很大的时候，我们需要更新每个用户的新消息状态，为每个用户都创建消息提醒，并推送消息通知，这个过程是较慢的且可以有一定延迟的，所以适合 Message Queue。

选项 D 是正确的，因为这是一个外部 API 通信（和 GCM 或者 APNS 通信），且可能会失败，需要重试机制。



Q:

![](<../.gitbook/assets/image (6).png>)

A: B

不可以！！一个 Table 的 Primary Key 是会被其他 Table 的数据引用的（Foreign Key），这里有一个限制是，primary key 不可以被随意更改。否则的话，凡是引用到了这个被更改的 primary key 的数据都需要改，这会带来很大的效率问题。而 participant\_hash\_code 在群成员加入或者离开的时候需要被重新计算，是一个经常会变动和修改的值。&#x20;

假设一个群里有 10万条信息，message 是引用了 thread 的 primary key 的（记录这条message在哪个thread里发的），如果一个人加群退群导致这个 primary key 要改，这10万条信息的引用全都要改，那就太慢了。



Problems:

1. [1786](https://www.lintcode.com/problem/1786/)

