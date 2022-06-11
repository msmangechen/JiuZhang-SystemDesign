# Catalog

第一章【直播】2022春招系统设计面试揭秘+现场mock

* System Design 面试揭秘
* 如何提升System Design 能力
* 现场mock interview+深入复盘
* Q\&A

第二章【互动】走进系统设计 & 新鲜事系统

* 什么是系统设计 What is System Design
* 系统设计中常见的问题是什么 How we ask System Design in Interview
* 怎样回答系统设计问题 How to answer System Design Question
* 系统设计的 4S 分析法 4S in System Design
* 系统设计的知识点构成 Basic Knowledge of System Design
* 设计推特 Design a Twitter

第三章【直播】秒杀系统与订票系统设计

* 高并发场景下引发的常见问题
* 了解数据一致性
* 什么是动静分离
* 读写分离如何实现
* 如何防止超卖

第四章【视频】秒杀系统与订票系统设计（南帝老师主讲）

* 高并发场景下引发的常见问题
* 了解数据一致性
* 什么是动静分离
* 读写分离如何实现
* 如何防止超卖

第五章【互动】从用户系统设计中学习数据库与缓存

* 通过设计用户系统了解：
* 用户系统的特点是什么？
* 什么是会话 Session?
* 什么是数据库，什么是缓存，他们之间如何配合？
* 什么是 Cache Through 什么是 Cache Aside
* NoSQL 与 SQL 数据库的优劣比较与选取标准

第六章【互动】网站系统，API设计与短网址

* 网站系统的基本构成
* API 设计问题
* 什么是 RestAPI
* 实战真题
  * What happen if you visit www.google.com?
  * How to design tiny url?
  * 如何设计 News Feed API
  * 如何设计 mention 功能
  * 如何做翻页 Pagination
* 关键词：Web, Consistent Hashing, Memcached, Tiny url.

第七章【直播】优惠券系统设计

* 了解优惠券的种类
* 介绍优惠券的核心流程
* 分析优惠券系统的难点
* 如何解决使用优惠券时会出现的分布式问题
* 如何解决优惠券系统的高并发问题
* 表单结构设计，数据库优化
* 优化：快过期券提醒与发券接口限流保护

第八章【视频】优惠券系统设计（南帝老师主讲）

* 了解优惠券的种类
* 介绍优惠券的核心流程
* 分析优惠券系统的难点
* 如何解决使用优惠券时会出现的分布式问题
* 如何解决优惠券系统的高并发问题
* 表单结构设计，数据库优化
* 优化：快过期券提醒与发券接口限流保护

第九章【互动】数据库拓展与一致性哈希算法

* 什么是数据库拆分
* 横向拆分 vs 纵向拆分 Horizontal Sharding vs Vertical Sharding
* 一致性哈希算法的两个版本
* 实战真题：如何设计限流器 Rate Limiter
* 实战真题：如何设计实时数据系统 Data Dog

第十章【互动】分布式文件系统 GFS

* &#x20;以 GFS 为例系统学习分布式文件系统，了解如下内容：
  * Master Slave 的设计模式
  * 分布式文件系统的读写流程
  * 怎么处理分布式系统中的failure 和recovery 的问题.
  * 如何做replica, check sum 检查
  * 了解consistent hash和sharding的实际应用

第十一章【直播】文档协同编辑系统设计

* websocket 在协同编辑中的应用
* 了解什么是协同编辑
* 协同编辑的几种实现方案
* 如何解决编辑冲突问题
* 了解 OT（ Operational Transformation）原理

第十二章【视频】文档协同编辑系统设计（南帝老师主讲）

* websocket 在协同编辑中的应用
* 了解什么是协同编辑
* 协同编辑的几种实现方案
* 如何解决编辑冲突问题
* 了解 OT（ Operational Transformation）原理

第十三章【互动】分布式数据库 Big Table

* 通过设计分布式数据库系统Bigtable了解如下内容：
* Big Table 的原理与实现
* 了解NoSQL Database如何进行读写操作的,以及相应的优化
* 了解如何建立index
* 学习Bloom Filter的实现原理
* Master Slave 的设计模式

第十四章【互动】聊天系统 IM System

* 聊天系统中的 Pull vs Push
* 讲解一种特殊的 Service - Realtime Service
* 用 channel 优化群聊
* 如何限制多机登录
* 用户在线状态的获取与查询 Online Status

第十五章【直播】视频流系统设计

* 视频切分和断点续传如何实现
* 如何在架构设计中节省带宽
* 小文件存储之视频切片与缩略图存储
* 了解视频预加载
* 了解 CDN 的基本原理

第十六章【视频】视频流系统设计（南帝老师主讲）

* 视频切分和断点续传如何实现
* 如何在架构设计中节省带宽
* 小文件存储之视频切片与缩略图存储
* 了解视频预加载
* 了解 CDN 的基本原理

第十七章【互动】基于地理位置的信息系统

* 系统学习LBS相关系统设计的核心要点：
* 地理位置信息存储与查询常用算法之 Geohash
* 如何设计 Uber
* 关键点：学会设计 Uber 以后可以轻松解决设计 Facebook Nearby 和 Yelp

第十八章【互动】分布式计算 Map Reduce

* 学习Map Reduce 的应用与原理
* 了解如何多台机器并行解决算法问题
* 掌握Map和Reduce的原理
* 通过三个题目掌握MapReduce算法实现：
* WordCount
* InvertedIndex
* Anagram

第十九章【直播】推特搜索系统设计 Twitter Search

* 推特的海量推文数据如何存储
* 如何快速搜索
* 对搜索结果进行排名
* 搜索系统容错能力

第二十章【视频】推特搜索系统设计 Twitter Search（南帝老师主讲）

* 推特的海量推文数据如何存储
* 如何快速搜索
* 对搜索结果进行排名
* 搜索系统容错能力

第二十一章【互动】爬虫系统与搜索建议系统

通过对爬虫系统设计 (Web Crawler) 与 搜索建议系统设计 (Google Suggestion) 了解如下内容：

* 多线程
* 生产者消费者模型
* 爬虫系统的演化：单线程，多线程，分布式
* Trie 结构的原理及应用
* 如何在系统设计中使用 Trie

第二十二章【互动】系统设计的核心必考知识点：数据库索引与事务（增）

* Mysql 索引的原理
* 索引的分类
* 索引的基本使用原则
* 事务的概念和原理
* 事务的应用场景

第二十三章【直播】评论系统设计 Comment system

* 如何设计评论区API
* 评论全文搜索功能
* 异步任务
* 动态缓存
* 如何实现评论赞数和踩数

第二十四章【视频】评论系统设计 Comment system（西毒老师主讲）

* 如何设计评论区API
* 评论全文搜索功能
* 异步任务
* 动态缓存
* 如何实现评论赞数和踩数
