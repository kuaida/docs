## Redis的基本知识

  1. Redis是什么   
    基于BSD开源的使用ANSI C语言编写、支持网络、基于内存持久化的日志型、Key-Value式的数据库   
      * Redis存储的数据是键值对的方式
      * Redis一般作为缓存数据库
      * Redis具有五种数据类型(字符串，哈希，链表，无序集合，有序集合)

  2. Redis的基本使用  
    1. 字符串  
      * 设置 set key value  
      * 获得 get key  
      * 整型自增加1 incr key  
      * 获得所有键 keys *

    2. 哈希h  
      * 设置key对象的field属性的值为value hset key field value  
      * 得到key对象的field属性的值 hget key field  
      * 得到key对象的所有属性和值 hgetall key  

    3. 链表(适合存储社交网站的新鲜事)l  
      * 向链表key左边添加元素 lpush key value [value2 ...]  
      * 向链表key右边添加元素 rpush key value [value2 ...]  
      * 移除key链表左边第一个元素 lpop key  
      * 移除key链表右边第一个元素 rpop key  
      * 获取链表中一段数据 lrange key start end (0最前一个 -1最后一个)
    4. 集合类型(适合存储文章的标签，具有唯一性)s  
      * 集合key中添加元素，若存在则忽略 sadd key member [member2 ...]  
      * 删除集合key中的元素 srem key member [member2 ...]  
      * 返回集合key中所有的元素 smembers key  
      * 多个集合交集运算 sinter key1 key2 [key3 ...]  
      * 多个集合差集运算 sdiff key1 key2 [key3 ...]  
      * 多个集合并集运算 sunion key1 key2 [key3 ...]
    5. 有序集合(通过文章访问量排序)z  
      * 向有序集合key中加入一个或者多个元素和分数，如果元素已经存在，则替换分数 zadd key score member [score member ...]
      * 删除集合中一个或者多个元素 zrem key member [member ...]
      * 按元素分数从小到大顺序返回元素，如需获得对应元素的分数，在尾部加withscores zrange key start end [withscores]
      * 从大到小顺序返回元素 zrevrange key start end [withscores]
  3. Redis数据库桌面管理工具
      [下载地址](http://redisdesktop.com/download)
  4. Redis数据库说明
      * 默认支持16个数据库 编号0~15 默认使用0 选择数据库:SELECT 编号
      * Redis不支持自定义数据库名字，不支持每个数据库设置不同的密码
      * 默认端口6379
      * Redis安装后，默认认证密码
