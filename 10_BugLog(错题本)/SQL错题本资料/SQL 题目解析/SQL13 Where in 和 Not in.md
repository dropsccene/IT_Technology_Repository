---
PC地址: https://www.nowcoder.com/practice/0355033fc2244cdaa09b2bd6e794c762?tpId=199&tags=&title=&difficulty=0&judgeStatus=0&rp=0&sourceUrl=%2Fexam%2Foj%3Ftab%3DSQL%25E7%25AF%2587%26topicId%3D82
tags:
  - SQL
---
![[SQL13.png]]

## 第一步

1. 查看所有行
2. 筛选出北大、复旦、山大的所有数据
3. 数据在user_profile
## 第二步

1. select device_id,gender,age,university,gpa
2. where university in (`北京大学`,`复旦大学`,`山东大学`)
3. from user_profile

## 第三步

```sql
select device_id,gender,age,university,gpa
from user_profile
where university in ('北京大学','复旦大学','山东大学')；
```

## 四、`IN` 操作符详解 📊

### 语法：

```sql
WHERE 字段名 IN (值1, 值2, 值3, ...);
```

### 本质：

```
IN ('A', 'B', 'C')  =  = 'A' OR = 'B' OR = 'C'
```

### 示例：


```sql
-- 查年龄是 20、21、23 岁的用户
WHERE age IN (20, 21, 23);

-- 查省份是北京、上海、浙江的用户
WHERE province IN ('Beijing', 'Shanghai', 'ZheJiang');

-- 查设备ID是 2138、3214、6543 的用户
WHERE device_id IN (2138, 3214, 6543);
```

---

## 五、`IN` vs `OR` 对比表

| 维度      | IN 写法 | OR 写法 |
| ------- | ----- | ----- |
| 代码行数    | 1 行   | 多行    |
| 可读性     | 高     | 一般    |
| 维护成本    | 低     | 高     |
| 性能      | 一样    | 一样    |
| **推荐度** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐   |