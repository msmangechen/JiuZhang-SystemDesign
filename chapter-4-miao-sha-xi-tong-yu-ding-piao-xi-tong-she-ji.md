# Chapter 4 秒杀系统与订票系统设计

CDN: [https://www.cloudflare.com/learning/cdn/what-is-a-cdn/](https://www.cloudflare.com/learning/cdn/what-is-a-cdn/)

### 需要解决问题：

* Large flow and high concurrency 瞬时大流量高并发
* Over sale 有限库存，不能超卖
  * 使用UPDATE语句自带的行锁（DB row lock）
* Malicious ticket grab 黄牛恶意请求
* 固定时间开启
* Purchase limit 严格限购

### 需求拆解：

Business side 商家侧

买家侧

### Service：

* Monolithic 单体架构
  * 问题：
    * 前后端耦合（coupling），服务压力较大
    * 各功能模块耦合严重
    * 系统复杂，一个模块的升级需要导致整个服务器升级
    * 扩展性（expandability）差，难以针对某个模块单独扩展
    * 开发协作（cooperation）困难，都在开发一个代码仓库（repository）
    * 级联故障（cascading failure），一个模块的故障导致整个服务不可用
    * 陷入某种单一技术和语言中（eg.只能用java）
    * 数据库崩溃导致整个DB不可用
* Microservice 微服
  * 拆分服务：
    * Seckill service 秒杀服务 -> 秒杀DB
    * Commodity info & stock service 商品信息和库存服务 -> 商品DB
    * Order service 订单服务 -> 订单DB
    * Payment service支付服务 -> 支付DB

### Storage：

DB design:

* commodity\_info
* seckill\_info
* stock\_info
* order\_info



Index:

作用：加快查找速度



### Redis

![](<.gitbook/assets/image (10).png>)

内存(memory)读取速度 > 磁盘(disk)读取速度





