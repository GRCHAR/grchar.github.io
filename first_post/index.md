# Redis 命令大全


Redis 是一个开源的键值对存储数据库，支持多种数据结构。本文整理了常用的 Redis 命令，方便快速查阅。

## 🔑 基础命令

### 键操作

| 命令  | 语法  | 描述  |
| --- | --- | --- |
| DEL | `DEL key [key ...]` | 删除一个或多个键 |
| EXISTS | `EXISTS key` | 检查键是否存在 |
| EXPIRE | `EXPIRE key seconds` | 设置键的过期时间（秒） |
| KEYS | `KEYS pattern` | 查找匹配模式的键（生产环境慎用） |
| TTL | `TTL key` | 查看键剩余生存时间 |
| TYPE | `TYPE key` | 获取键存储的数据类型 |

示例：

SET mykey "Hello"  
EXPIRE mykey 60  
TTL mykey # 返回剩余秒数

---

## 🧮 数据结构命令

### 字符串（String）

| 命令  | 语法  | 描述  |
| --- | --- | --- |
| SET | `SET key value [EX seconds]` | 设置键值 |
| GET | `GET key` | 获取值 |
| INCR | `INCR key` | 值自增1 |
| APPEND | `APPEND key value` | 追加字符串 |
| STRLEN | `STRLEN key` | 获取字符串长度 |

### 列表（List）

| 命令  | 语法  | 描述  |
| --- | --- | --- |
| LPUSH | `LPUSH key element [element ...]` | 左侧插入元素 |
| RPOP | `RPOP key` | 移除并获取最后一个元素 |
| LRANGE | `LRANGE key start stop` | 获取列表片段 |
| LINDEX | `LINDEX key index` | 通过索引获取元素 |

### 哈希（Hash）

| 命令  | 语法  | 描述  |
| --- | --- | --- |
| HSET | `HSET key field value` | 设置哈希字段值 |
| HGET | `HGET key field` | 获取字段值 |
| HGETALL | `HGETALL key` | 获取所有字段和值 |
| HDEL | `HDEL key field [field ...]` | 删除字段 |

### 集合（Set）

| 命令  | 语法  | 描述  |
| --- | --- | --- |
| SADD | `SADD key member [member ...]` | 添加元素 |
| SMEMBERS | `SMEMBERS key` | 获取所有元素 |
| SINTER | `SINTER key [key ...]` | 求多个集合的交集 |
| SISMEMBER | `SISMEMBER key member` | 判断元素是否存在 |

### 有序集合（Sorted Set）

| 命令  | 语法  | 描述  |
| --- | --- | --- |
| ZADD | `ZADD key score member [score member ...]` | 添加带分数的元素 |
| ZRANGE | `ZRANGE key start stop [WITHSCORES]` | 按索引范围获取元素 |
| ZREVRANK | `ZREVRANK key member` | 获取元素的逆序排名 |

---

## 🛠️ 高级功能

### 事务

MULTI # 开始事务  
SET a 100  
SET b 200  
EXEC # 执行事务

### 发布订阅

SUBSCRIBE channel # 订阅频道  
PUBLISH channel "message" # 发布消息

### 持久化

SAVE # 同步保存数据到磁盘  
BGSAVE # 后台保存数据

---

## 🖥️ 服务器管理

| 命令  | 描述  |
| --- | --- |
| `INFO` | 查看服务器信息 |
| `CONFIG GET *` | 获取配置参数 |
| `CLIENT LIST` | 查看连接的客户端 |
| `FLUSHALL` | 删除所有数据库数据（慎用） |

---

## 📚 附录

1. 使用 `HELP` 命令获取实时帮助：HELP @list # 查看列表相关命令帮助
2. 推荐使用 `SCAN` 代替 `KEYS` 遍历键
3. 事务不保证原子性，执行中出错不会回滚已执行命令
  提示：建议结合 Redis 官方文档（https://redis.io/commands）获取最新命令信息。

