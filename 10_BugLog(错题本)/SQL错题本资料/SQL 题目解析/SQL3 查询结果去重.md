---
tags:
  - SQL
readingDate: 2026-03-19
PC地址: https://www.nowcoder.com/practice/82ebd89f12cf48efba0fecb392e193dd?tpId=199&tags=&title=&difficulty=0&judgeStatus=0&rp=0&sourceUrl=%2Fexam%2Foj%3Ftab%3DSQL%25E7%25AF%2587%26topicId%3D82
---
![[SQL3.png]]

## 第一步：先想步骤

1. 查看学校数据
2. 取出学校的去重数据
3. 数据在user_profile

## 第二步：翻译成SQL语句

1. select university
2. **distinct**  --> 返回唯一不同的值，去除重复项。
3. from user_profile

## 第三步：编写完整的SQL语句

```sql
select distinct university
from user_profile;
```

## 注意：

1. `DISTINCT` 必须紧跟 `select`后面
2. 多列去重时，只有”所有列都相同“才算重复
3. 如果表非常大（百万行），DISTINCT 会变慢（以后学索引再优化）