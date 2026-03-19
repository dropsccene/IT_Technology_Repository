---
PC地址: https://www.nowcoder.com/practice/08c9846a423540319eea4be44e339e35?tpId=199&tags=&title=&difficulty=0&judgeStatus=0&rp=0&sourceUrl=%2Fexam%2Foj%3Ftab%3DSQL%25E7%25AF%2587%26topicId%3D82
tags:
  - SQL
readingDate: 2026-03-19
---

![[SQL10.png]]

## 第一步

1. 查看设备 ID、性别、年龄、学校
2. 筛选出所有年龄值不为空
3. 数据在 user_profile 中

## 第二步

1. select device_id,gender,age,university
2. where age is not null
3. from user_profile
## 第三步

```sql
select device_id,gender,age,university
from user_profile
where age is not null;
```

## NULL 值查询：为什么 `!= null` 是错的？

### 一、直接答案：你的代码有 1 个致命错误 ⚠️

表格

|错误|你的写法|正确写法|
|---|---|---|
|**NULL 比较错误**|`age != null` ❌|`age IS NOT NULL` ✅|

### 修正后的代码：

```
SELECT device_id, gender, age, university
FROM user_profile
WHERE age IS NOT NULL;  -- 年龄不为空
```

---

## 二、第一性原理：为什么 `!= null` 行不通？

### 🤔 核心问题：NULL 不是值，是"未知"！


```
┌─────────────────────────────────────────────────
│  普通值：21、25、30... → 可以比较 (=, !=, >, <)    │
│                                                 │
│  NULL：表示"不知道"、"没有值" → 不能用普通比较运算符  │
│                                                 │
│  哲学问题：你能说"未知 != 未知"吗？不能！因为都不知道  │
└─────────────────────────────────────────────────
```

### SQL 的三值逻辑：

```
普通逻辑：TRUE / FALSE

SQL 逻辑：TRUE / FALSE / UNKNOWN (NULL 导致)

age != NULL  →  结果是 UNKNOWN，不是 TRUE！
WHERE 只保留 TRUE 的行，UNKNOWN 被过滤掉！
```

---

## 三、费曼学习法：用大白话解释 NULL

### 📦 想象一个盒子

表格

|场景|盒子里有什么|SQL 怎么写|
|---|---|---|
|年龄是 21 岁|盒子里有数字 21|`age = 21`|
|年龄不是 21 岁|盒子里有数字，但不是 21|`age != 21`|
|**年龄未知**|**盒子是空的，不知道有没有东西**|`age IS NULL`|
|**年龄已知**|**盒子里有东西（不管是什么）**|`age IS NOT NULL`|

> **核心**：NULL 不是"空盒子"，是"不知道盒子里有没有东西"！

---

## 四、NULL 查询的 4 种标准写法 📝

|需求|错误写法 ❌|正确写法 ✅|
|---|---|---|
|年龄为空|`age = null`|`age IS NULL`|
|年龄不为空|`age != null`|`age IS NOT NULL`|
|年龄是空或 20 岁|`age = null OR age = 20`|`age IS NULL OR age = 20`|
|年龄不是空且不是 20 岁|`age != null AND age != 20`|`age IS NOT NULL AND age != 20`|

---

## 五、为什么设计成这样？🤔

### 历史原因 + 逻辑严谨性

```
假设：age != NULL 能工作

问题：NULL != NULL 应该返回什么？
- 返回 TRUE？但两个都不知道，怎么确定不相等？
- 返回 FALSE？但两个都不知道，怎么确定相等？

结论：NULL 和任何值比较（包括 NULL 自己）都返回 UNKNOWN！
```

### 验证：


```
SELECT NULL = NULL;    -- 返回 NULL (不是 TRUE！)
SELECT NULL != NULL;   -- 返回 NULL (不是 TRUE！)
SELECT NULL IS NULL;   -- 返回 TRUE ✅
```

---

## 六、实战对照表 📊

|中文描述|错误写法|正确写法|
|---|---|---|
|年龄为空|`age = null`|`age IS NULL`|
|年龄不为空|`age != null`|`age IS NOT NULL`|
|学校为空|`university = null`|`university IS NULL`|
|学校不为空|`university != null`|`university IS NOT NULL`|
|年龄为空或学校为空|`age = null OR university = null`|`age IS NULL OR university IS NULL`|
