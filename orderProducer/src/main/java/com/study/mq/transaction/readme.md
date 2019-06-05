**https://blog.csdn.net/qq_31463999/article/details/89788176**
#采用最终一致性原理。
 @ 需要保证以下三要素:
 
### 确认生产者一定要将数据投递到MQ服务器中（采用MQ消息确认机制）
### MQ消费者消息能够正确消费消息，采用手动ACK模式（注意重试幂等性问题）
### 如何保证第一个事务先执行，采用补偿机制，在创建一个补单消费者进行监听，如果订单没有创建成功，进行补单。(如果第一个事务中出错，补单消费者会在重新执行一次第一个事务，例如第一个事务是添加订单表，如果失败在补单的时候重新生成订单记录，由于订单号唯一，所以不会重复)
 