---
tags:
  - SQL
PC地址: https://www.nowcoder.com/practice/009d8067d2df47fea429afe2e7b9de45?tpId=199&tqId=1971219&sourceUrl=%2Fexam%2Foj%3Ftab%3DSQL%25E7%25AF%2587%26topicId%3D82
---
![[SQL18.png]]

# 🎯 SQL 编写完整思路：从需求到代码的每一步

---

## 一、先读题目，明确需求 📋

### 题目要求分析：

```
┌─────────────────────────────────────────────────────────────┐
│                      题目需求拆解                            │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  需求1：按性别和学校分组                                     │
│        → 需要 GROUP BY gender, university                   │
│                                                             │
│  需求2：统计每组用户数量                                     │
│        → 需要 COUNT() 聚合函数                              │
│                                                             │
│  需求3：计算平均活跃天数                                     │
│        → 需要 AVG(active_days_within_30)                    │
│                                                             │
│  需求4：计算平均发帖数                                       │
│        → 需要 AVG(question_cnt)                             │
│                                                             │
│  需求5：结果保留1位小数                                      │
│        → 需要 ROUND(..., 1)                                 │
│                                                             │
│  需求6：输出列名有特定要求                                   │
│        → 需要 AS 别名                                       │
│                                                             │
│  需求7：按性别、学校排序                                     │
│        → 需要 ORDER BY gender, university                   │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## 二、逐步构建 SQL 语句 🏗️

### 第1步：确定数据从哪来

```sql
-- 思考：数据存储在哪个表？
-- 答案：user_profile 表

FROM user_profile
```

**为什么？** 所有查询都必须指定数据来源，这是 SQL 的基础。

---

### 第2步：确定要显示哪些字段

```sql
-- 思考：题目要求输出什么？
-- 答案：性别、学校、用户数、平均活跃天数、平均发帖数

SELECT gender, university
FROM user_profile
```

**为什么先写这两个？** 因为它们是分组字段，不是计算出来的，先确定基础字段。

---

### 第3步：添加聚合计算

```sql
-- 思考：用户数怎么算？
-- 答案：用 COUNT() 统计行数

SELECT gender, university, COUNT(gender)
FROM user_profile

-- 思考：平均活跃天数怎么算？
-- 答案：用 AVG() 求平均值

SELECT gender, university, COUNT(gender), AVG(active_days_within_30)
FROM user_profile

-- 思考：平均发帖数怎么算？
-- 答案：用 AVG() 求平均值

SELECT gender, university, COUNT(gender), 
       AVG(active_days_within_30), 
       AVG(question_cnt)
FROM user_profile
```

**为什么用聚合函数？** 因为我们要对每组数据进行统计计算，不是显示单行数据。

---

### 第4步：添加分组

```sql
-- 思考：按什么分组？
-- 答案：按性别和学校分组

SELECT gender, university, COUNT(gender), 
       AVG(active_days_within_30), 
       AVG(question_cnt)
FROM user_profile
GROUP BY gender, university
```

**⚠️ 关键规则：** SELECT 中出现的非聚合字段（gender, university）必须出现在 GROUP BY 中！

```
┌─────────────────────────────────────────────────────────────┐
│                    GROUP BY 核心规则                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ✅ 正确：                                                   │
│  SELECT gender, university, COUNT(*)                        │
│  GROUP BY gender, university                                │
│  （SELECT 中的非聚合字段都在 GROUP BY 中）                    │
│                                                             │
│  ❌ 错误：                                                   │
│  SELECT gender, university, COUNT(*)                        │
│  GROUP BY gender                                            │
│  （university 缺失！会报错）                                 │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

### 第5步：添加格式处理（保留小数）

```sql
-- 思考：题目要求保留几位小数？
-- 答案：1位小数

SELECT gender, university, COUNT(gender), 
       ROUND(AVG(active_days_within_30), 1), 
       ROUND(AVG(question_cnt), 1)
FROM user_profile
GROUP BY gender, university
```

**为什么用 ROUND？** 因为 AVG() 计算结果可能是多位小数，题目要求格式化输出。

```
ROUND(数值, 小数位数)
   │       │
   │       └── 1 表示保留1位小数
   │
   └── 要处理的数值表达式
```

---

### 第6步：添加列别名

```sql
-- 思考：输出列名有要求吗？
-- 答案：有！user_num, avg_active_day, avg_question_cnt

SELECT gender, 
       university, 
       COUNT(gender) AS user_num, 
       ROUND(AVG(active_days_within_30), 1) AS avg_active_day, 
       ROUND(AVG(question_cnt), 1) AS avg_question_cnt
FROM user_profile
GROUP BY gender, university
```

**为什么用 AS？**

1. 让输出列名更有意义
2. 符合题目要求的列名格式
3. 方便后续引用（如在 ORDER BY 中）

---

### 第7步：添加排序

```sql
-- 思考：结果需要排序吗？
-- 答案：需要！按 gender 和 university 升序

SELECT gender, 
       university, 
       COUNT(gender) AS user_num, 
       ROUND(AVG(active_days_within_30), 1) AS avg_active_day, 
       ROUND(AVG(question_cnt), 1) AS avg_question_cnt
FROM user_profile
GROUP BY gender, university
ORDER BY gender, university
```

**为什么用 ORDER BY？**

1. 让结果更有规律，便于查看
2. 符合题目输出要求
3. ASC 升序可省略（默认就是升序）

---

### 第8步：检查是否需要筛选条件

```sql
-- 思考：需要 WHERE 筛选吗？
-- 答案：不需要！题目没有要求筛选特定性别或学校

-- 如果有筛选条件，应该加在 GROUP BY 之前
-- 例如：只统计男性用户
WHERE gender = 'male'
```

**⚠️ 重要：** 本题没有筛选条件，所以**不需要 WHERE 子句**！

---

## 三、完整代码（最终版）✅

```sql
SELECT gender, 
       university, 
       COUNT(gender) AS user_num, 
       ROUND(AVG(active_days_within_30), 1) AS avg_active_day, 
       ROUND(AVG(question_cnt), 1) AS avg_question_cnt
FROM user_profile
GROUP BY gender, university
ORDER BY gender, university;
```

---

## 四、SQL 执行顺序详解 🔄

```
┌─────────────────────────────────────────────────────────────────┐
│                      SQL 执行顺序（重要！）                      │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  第1步：FROM                                                     │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ 从 user_profile 表读取所有数据                            │   │
│  │ 共 8 行数据                                              │   │
│  └─────────────────────────────────────────────────────────┘   │
│                            ↓                                    │
│  第2步：WHERE（本题没有）                                         │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ 如果有筛选条件，在这里过滤行                              │   │
│  │ 例如：WHERE gender = 'male'                              │   │
│  └─────────────────────────────────────────────────────────┘   │
│                            ↓                                    │
│  第3步：GROUP BY                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ 按 gender + university 分组                               │   │
│  │ 分成 5 组：                                              │   │
│  │ female-北京大学, female-浙江大学, male-北京大学,           │   │
│  │ male-复旦大学, male-山东大学                              │   │
│  └─────────────────────────────────────────────────────────┘   │
│                            ↓                                    │
│  第4步：SELECT（聚合计算）                                        │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ 对每组计算：                                            │   │
│  │ COUNT(gender) → 用户数                                   │   │
│  │ AVG(active_days_within_30) → 平均活跃天数                │   │
│  │ AVG(question_cnt) → 平均发帖数                           │   │
│  │ ROUND(..., 1) → 保留1位小数                              │   │
│  └─────────────────────────────────────────────────────────┘   │
│                            ↓                                    │
│  第5步：ORDER BY                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ 按 gender 升序，再按 university 升序排序                   │   │
│  │ female 在前，male 在后                                    │   │
│  └─────────────────────────────────────────────────────────┘   │
│                            ↓                                    │
│  第6步：返回结果                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ 最终输出 5 行数据                                         │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 五、你的错误代码 vs 正确代码对比 ⚠️

|对比项|你的代码 ❌|正确代码 ✅|
|---|---|---|
|WHERE 用法|`WHERE GROUP BY`|无 WHERE（或 `WHERE 条件` + `GROUP BY`）|
|列别名|无别名|`AS user_num` 等|
|语法结构|WHERE 后直接跟 GROUP BY|GROUP BY 独立成句|

### 错误原因分析：

```
┌─────────────────────────────────────────────────────────────┐
│                    错误根源分析                              │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  你的理解：                                                  │
│  "WHERE 是用来引出 GROUP BY 的"  ❌                          │
│                                                             │
│  正确理解：                                                  │
│  "WHERE 是用来筛选行的，GROUP BY 是用来分组的"  ✅            │
│  两者是独立的子句，不能连用！                                │
│                                                             │
│  类比理解：                                                  │
│  WHERE 就像"过滤器"（过滤不需要的行）                        │
│  GROUP BY 就像"分类器"（把数据分成不同的组）                  │
│  先过滤，再分类，是两个独立步骤！                            │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## 六、WHERE 使用场景详解 🎯

### 什么时候需要 WHERE？

```
┌─────────────────────────────────────────────────────────────┐
│                    WHERE 使用判断流程                        │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  题目是否要求筛选特定数据？                                   │
│           │                                                 │
│     ┌─────┴─────┐                                           │
│     │           │                                           │
│    是          否                                           │
│     │           │                                           │
│     ↓           ↓                                           │
│  需要 WHERE   不需要 WHERE                                   │
│     │           │                                           │
│  例如：        例如：                                        │
│  只统计男性    统计所有性别                                   │
│  只统计某大学  统计所有大学                                   │
│  只统计活跃用户 统计所有用户                                  │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### 本题判断：

```
题目要求：按性别和学校分组统计所有用户
         ↓
    没有筛选特定性别或学校
         ↓
    不需要 WHERE 子句！
```

---

## 七、常见错误及修正 ⚠️

|错误类型|错误代码|错误原因|正确代码|
|---|---|---|---|
|WHERE 误用|`WHERE GROUP BY`|WHERE 后不能跟 GROUP BY|删除 WHERE|
|缺少别名|`COUNT(gender)`|列名不符合要求|`COUNT(gender) AS user_num`|
|GROUP BY 不全|`GROUP BY gender`|university 缺失|`GROUP BY gender, university`|
|ROUND 位置错|`ROUND(AVG(..., 1))`|参数位置错误|`ROUND(AVG(...), 1)`|
|ORDER BY 顺序错|`ORDER BY university, gender`|顺序与要求相反|`ORDER BY gender, university`|

---

## 八、记忆模板 📝

```
┌─────────────────────────────────────────────────────────────┐
│                    GROUP BY 查询模板                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  SELECT 分组字段1,                                           │
│         分组字段2,                                           │
│         聚合函数1 AS 别名1,                                  │
│         聚合函数2 AS 别名2                                   │
│  FROM 表名                                                   │
│  WHERE 筛选条件（可选，没有就删除）                            │
│  GROUP BY 分组字段1, 分组字段2                               │
│  HAVING 组筛选条件（可选，没有就删除）                          │
│  ORDER BY 排序字段1, 排序字段2;                              │
│                                                             │
│  ⚠️ 注意：                                                   │
│  1. SELECT 中的非聚合字段必须出现在 GROUP BY 中               │
│  2. WHERE 在 GROUP BY 之前，不能用聚合函数                    │
│  3. HAVING 在 GROUP BY 之后，可以用聚合函数                   │
│  4. 没有筛选条件时，不要写 WHERE                              │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## 九、动手练习 💡

### 尝试修改以下需求：

|需求|需要添加/修改什么|
|---|---|
|只统计男性用户|添加 `WHERE gender = 'male'`|
|只显示用户数>1的组|添加 `HAVING COUNT(*) > 1`|
|按用户数降序排序|修改 `ORDER BY user_num DESC`|
|保留2位小数|修改 `ROUND(..., 2)`|
|统计总活跃天数|将 `AVG()` 改为 `SUM()`|

---

## 十、总结回顾 🎯

```
┌─────────────────────────────────────────────────────────────┐
│                    本题关键要点                              │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ✅ 1. 没有筛选条件 → 不需要 WHERE                            │
│                                                             │
│  ✅ 2. 按 gender + university 分组 → GROUP BY 两个字段        │
│                                                             │
│  ✅ 3. SELECT 中的非聚合字段必须在 GROUP BY 中出现            │
│                                                             │
│  ✅ 4. 聚合函数 + ROUND + AS 别名 → 格式化和命名              │
│                                                             │
│  ✅ 5. ORDER BY 在最后 → 按题目要求排序                       │
│                                                             │
│  ❌ 6. WHERE 不能直接跟 GROUP BY → 这是语法错误！             │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

**现在理解了吗？** 写 SQL 就像搭积木，每一步都有明确的目的和顺序！🧱

有任何问题继续问我！🚀