---
tags:
  - SQL
PC地址: https://www.nowcoder.com/practice/499b6d01eae342b2aaeaf4d0da61cab0?tpId=199&tags=&title=&difficulty=0&judgeStatus=0&rp=0&sourceUrl=%2Fexam%2Foj%3Ftab%3DSQL%25E7%25AF%2587%26topicId%3D82
状态: 在学
readingDate: 2026-03-19
---

![[SQL2.png]]

## 第一步：先想步骤

1. 要拿数据
2. 拿设备 id、性别、年龄、学校的数据
3. 数据在 user_profile 表中

## 第二步：翻译成 SQL 语句

1. select
2. device_id,gender,age,university
3. from user_profile

## 第三步：编写完整的SQL语句

```sql
select device_id,gender,age,university
from user_profile;
```
