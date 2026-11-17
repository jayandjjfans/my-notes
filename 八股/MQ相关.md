# MQ相关

##### Kafka如何保证消息不丢失？

发送：

1.Kafka默认异步，可调整为同步
2.异步回调函数里重试
3.设置retries参数在服务器或网络异常时重试

存储

1.磁盘持久化（异步刷盘可能丢失）
2.partition副本集(仍然需要结合ACKS参数保证)
3.acks=0   不需要等待响应即认为发送成功
  acks=1    leader收到数据后就返回响应
  acks=-1/all    所有follower同步完数据再响应

消费

1.auto.commit.offset=false，手动提交偏移量；消息过程中异常，恢复后从上次提交的偏移量继续消费
2.offset值可以调整，重新消费

