### 电商系统如何防止库存超卖?

###### 方案一

使用Redis分布式锁或者Zookeeper分布式锁,加锁扣减库存操作，缺点是性能不高。

###### 方案二

基于Redis Lua脚本 原子化库存查询+库存扣减操作


###### 方案三

基于redis 队列(List)
通过pop扣减库存，缺点是如果秒杀商品数量过大，会消耗大量内存

###### 方案四

基于数据库Version乐观锁，先查询库存版本号，同过版本号去修改库存，失败轮训重试，缺点是会消耗大量CPU