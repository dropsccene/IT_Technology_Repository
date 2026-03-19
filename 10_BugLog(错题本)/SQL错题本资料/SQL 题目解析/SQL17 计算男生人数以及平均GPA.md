---
PC地址: https://www.nowcoder.com/practice/7d9a7b2d6b4241dbb5e5066d7549ca01?tpId=199&tags=&title=&difficulty=0&judgeStatus=0&rp=0&sourceUrl=%2Fexam%2Foj%3Ftab%3DSQL%25E7%25AF%2587%26topicId%3D82
tags:
  - SQL
---
![[SQL17.png]]

## 第一步

1. 查看男性用户个数，gpa
2. 筛选男性用户有多少个以及**他们**的平均gpa是多少
3. 数据在user_profile

## 第二步

1. select  count(gender = 'male') and avg(gpa)
2. from user_profile
3. where gender = 'male'

## 第三步

```sql
select  count(gender = 'male') and avg(gpa)
from user_profile
where gender = 'male';
```
## 问题分析

|问题点|你的代码|正确写法|
|---|---|---|
|缺少WHERE条件|无筛选|`WHERE gender = 'male'`|
|统计对象|所有用户|只统计男性用户|