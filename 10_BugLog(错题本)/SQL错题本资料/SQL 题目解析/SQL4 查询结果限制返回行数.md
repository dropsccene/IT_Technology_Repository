---
PC地址: https://www.nowcoder.com/practice/c7ad0e2df4f647dfa5278e99894a7561?tpId=199&tags=&title=&difficulty=0&judgeStatus=0&rp=0&sourceUrl=%2Fexam%2Foj%3Ftab%3DSQL%25E7%25AF%2587%26topicId%3D82
tags:
  - SQL
readingDate: 2026-03-19
---

![[SQL4.png]]

## 第一步：想步骤

1. 查看设备 ID 数据
2. 前 2 个的数据
3. 在 user_profile 表

## 第二步：翻译成 SQL

1. select device_id
2. **limit** 2 --> **限制数量**
3. from user_profile

## 第三步：编写完整的 SQL

```sql
select device_id
from user_profile
limit 2;
```

## 为什么要这么写？这样做有什么好处？

| 为什么                  | 好处（真实工作场景）                              |
| ----------------------- | ------------------------------------------------- |
| 用 LIMIT 2 而不是 id<3  | 永远正确！即使表有 100 万行、id 乱序也只取前 2 条 |
| SELECT 只写一列         | 速度超快，不浪费内存                              |
| LIMIT 永远写在最后      | 语法规则：SELECT → FROM → LIMIT（顺序不能乱）     |
| 不需要 ORDER BY（这次） | 题目默认按 id 顺序，前 2 个就是 id=1 和 2         |

**一句话背下来**： **“只要前 N 条，就在最后加 LIMIT N”** —— 这就是 MySQL 的“取前几名”神器！
