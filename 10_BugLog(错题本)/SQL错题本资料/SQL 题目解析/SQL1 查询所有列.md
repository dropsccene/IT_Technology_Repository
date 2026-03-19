---
tags:
  - SQL
readingDate: 2026-03-19
状态: 在学
PC地址: https://www.nowcoder.com/practice/f9f82607cac44099a77154a80266234a?tpId=199&tags=&title=&difficulty=0&judgeStatus=0&rp=0&sourceUrl=%2Fexam%2Foj%3Ftab%3DSQL%25E7%25AF%2587%26topicId%3D82
---
![[SQL1.png]]

## 第一步：先想步骤

1. 要取数据。
2. 取全部数据。
3. 数据在 uesr_profile 表中。

## 第二步：翻译成 SQL 语句

1. 要取数据。--> 用 **select**。
2. 取全部数据。 --> 用`*`表示全部/所有。
3. 数据在 uesr_profile 表中。 --> **from** user_profile；

## 第三步：编写完整的SQL语句

```SQL
select *
from user_profile;
```
