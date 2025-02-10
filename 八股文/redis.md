redis 数据结构有哪些

# String（字符串）
最基本的数据类型，可以存储文本、整数或二进制数据。

常用命令：SET, GET, INCR, DECR。

# List（列表）

有序的字符串集合，支持从两端插入或删除元素。

常用命令：LPUSH, RPUSH, LPOP, RPOP, LRANGE。

# Set（集合）

无序且不重复的字符串集合。

常用命令：SADD, SREM, SMEMBERS, SINTER, SUNION。

# Sorted Set（有序集合）

类似于 Set，但每个元素关联一个分数（score），用于排序。

常用命令：ZADD, ZREM, ZRANGE, ZSCORE, ZRANK。

# Hash（哈希）

键值对集合，适合存储对象。

常用命令：HSET, HGET, HMSET, HMGET, HGETALL。

# Bitmap（位图）

通过位操作存储布尔值，常用于高效存储和操作二进制数据。

常用命令：SETBIT, GETBIT, BITCOUNT, BITOP。

# HyperLogLog

用于基数统计（估算集合中不重复元素的数量）。

常用命令：PFADD, PFCOUNT, PFMERGE。

# Geospatial（地理空间）

存储地理位置信息，支持地理空间查询。

常用命令：GEOADD, GEOPOS, GEODIST, GEORADIUS。

# Stream（流）

用于日志类数据的存储和消费，支持消息队列功能。

常用命令：XADD, XREAD, XRANGE, XGROUP。