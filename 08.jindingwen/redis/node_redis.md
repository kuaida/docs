## 在node中使用Redis
  1. 安装Redis数据库到本地
```
wget http://download.redis.io/redis-stable.tar.gz
tar xzf redis-stable.tar.gz
cd redis-stable
make
cd src
./redis-server
```
  2. 在node项目中安装redis包
```
npm install redis
```
  3. 引入redis库，创建redis客户端
```js
const redis = require('redis');
const client= redis.createClient(options);
```   
    上述的options是redis的配置信息，一般包括:  
      host:127.0.0.1
      port:6379
      password: 在 < 2.5版本的redis中使用auth_pass
  4. 存储和获得数据
    * 单值set和get(用于缓存字符串类型)  
      ```js
      client.set('key','value'[,callback(err,thisData)])
      client.get('key',callback(err,replay){});
      ```
    * 多值set和get(缓存对象形式的数据)  
      ```js
      client.hmset('key',{one:"one",two:[1,2,3]}[,callback(err,thisData)]);
      client.hmset('key',"one","oneValue","two","twoValue"[,callback(err,thisData)]);
      ```   
      上述两种设置的效果相同，对于同一个key，后面设置的值会合并前面的值。  
      ```js
      client.hgetall('key',callback(err,this.Data){})
      ```
      退出Redis
      ```js
      client.quit()
      ```
    * 设置过期时间  
      ```js
      client.expire('key',秒数);
      ```
### 在本项目中的使用，只需要：
```js
  const redis = require('../reids');
  //设置字符串形式
  redis.set('key','value');
  //这是过去时间 10s
  redis.expire('key',10);
  redis.get('key',(err,replay)=>{
    console.log(replay);
  });
  //存储对象
  reids.hmset('key',{a:'a'});
  reids.hgetall('key',(err,replay)=>{
    console.log(replay);
  });
```
