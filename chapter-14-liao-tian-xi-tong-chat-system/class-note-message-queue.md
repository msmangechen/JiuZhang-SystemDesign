# Class note - Message queue

### RabbitMQ

Highly available (mirrored) queue:

双master，一个挂了另一个可以立刻顶上，也可以用于分摊读和写

{% embed url="https://www.rabbitmq.com/ha.html" %}

用到MQ的例子：

* 订火车票

功能：

* 设定task优先级
* 设定不同的queue（排队不在一起排）
