---
PC地址: https://www.nowcoder.com/practice/be54223075cc43ceb20e4ce8a8e3e340?tpId=199&tags=&title=&difficulty=0&judgeStatus=0&rp=0&sourceUrl=%2Fexam%2Foj%3Ftab%3DSQL%25E7%25AF%2587%26topicId%3D82
tags:
  - SQL
readingDate: 2026-03-19
---
![[SQL8.png]]

## 第一步

1. 查看设备ID、性别、年龄
2. 年龄在20岁及以上且23岁以下的数据
3. 数据在user_profile

## 第二步

1. select device_id,gender,age
2. where age >= 20 and age <= 23 或者 where age BETWEEN 20 and 23
3. from user_profile

## 第三步

```sql
select device_id,gender,age
from user_profile
where age between 20 and 23;
```


## 补充

`BETWEEN` 就是 `>= 且 <=` 的**快捷写法**，专门用来查"区间"。

### BETWEEN 的 4 大好处 🌟

|好处|说明|示例|
|---|---|---|
|**1. 代码更简洁**|少写重复字段名|`age BETWEEN 20 AND 23` vs `age >= 20 AND age <= 23`|
|**2. 可读性更强**|一眼看出是区间查询|看到 BETWEEN 就知道在查范围|
|**3. 不易出错**|不会漏写字段或搞错方向|不用担心情写成 `age >= 20 AND age >= 23`|
|**4. 性能相同**|数据库内部优化后一样快|执行效率没区别|
