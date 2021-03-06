### 缓存雪崩   缓存击穿   缓存穿透

- 缓存雪崩
  - 问题：大量的key设置了相同的过期时间，导致缓存在同一时间全部失效，造成DB瞬时请求增大，压力的剧增
  - 解决：可以给缓存过期的时间加上一个随机值，使得键值在过期时间分布开，不会集中到同一时刻失效；
- 缓存击穿
  - 问题：一个存在的key，在失效的瞬间，有大量的请求抵达，同样造成数据库的压力剧增；
  - 解决：可设置一个短期的key来锁定当前key的访问，是一个锁的实现，使用SETNX来实现；
- 缓存穿透
  - 问题：访问一个不存在的key，缓存起不到作用，请求都到达DB；
  - 解决：
    - 在数据库中找不到也将空值设置进入缓存，有效的时间设置较短；
    - 维护一个bitmap，用于存储可以访问的key，不存在的key值直接被过滤掉；