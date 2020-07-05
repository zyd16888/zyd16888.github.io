## 数据结构
1. string
    - 键值对
    - 小于1MB、加倍扩容，大于1MB、以1MB增加，最大512MB
2. list 
    - 快速链表结构
    - 插入删除快、时间复杂度O(1)
    - 索引定位慢、时间复杂度O(n)
    - 双向索引
3. hash(字典)
    - 数组加链表
    - 渐进式 rehash、保留新旧两个hash
    - 值只能是字符串
4. set(集合)
    - 键值对无序、唯一
    - 内部实现为字典、值为NULL
5. zset(有序集合、有序列表) 
    - 内部value的唯一性
    - 每个value一个score，排序权重
    - 内部实现用条约列表

## 通用规则
1. `create if not exists` 如果容器不存在，就创建一个
2. `drop if no elements` 如果容器中没有元素，立即删除容器
3. 所有数据结构都可以设置过期时间

## 分布式锁

### 死锁问题
使用`setnx`指令,增加过期时间防止死锁

```
> setnx lock:codehole true
OK
> expire lock:codehole 5
... do something critical ...
> del lock:codehole
```
同时执行
```
> set lock:codehole true ex 5 nx
OK
... do something critical ...
> del lock:codehole
```

### 超时问题

执行逻辑太长超出锁的超时限制

### 可重入性

线程在持有锁的情况下再次加锁，一个锁支持同一线程的多次加锁

```python
import redis
import threading

locks = threading.local()
locks.redis = {}

def key_for(user_id):
    return "account_{}".format(user_id)
def _look(client, key):
    return bool(client.set(key, True, nx=True, ex=5))
def _unlock(client, key):
    client.delete(key)
def lock(client, user_id):
    key = key_for(user_id)
    if key in locks.redis:
        locks.redis[key] += 1
        return True
    ok = _lock(client, key)
    if not ok:
        return False
    locks.redis[key] = 1
    return True
def unlock(client, user_id):
    key = key_for(user_id)
    if key in locks.redis:
        locks.redis[key] -= 1
        if locks.redis[key] <= 0:
            del locks.redis[key]
        return True
    return False

client = redis.StrictRedis()
print "lock", lock(client, "codehole")
print "lock", lock(client, "codehole")
print "unlock", unlock(client, "codehole")
print "unlock", unlock(client, "codehole")

```