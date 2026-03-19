---
PC地址:
tags:
  - SQL
---

![[SQL14.png]]

## 第一步

1. 查看ID，性别，年龄，学校，gpa
2. 筛选gqa在3.5以上的山东大学的用户或gpa在3.8以上的复旦大学的用户数据
3. 取出的数据按照device_id升序排列
4. 数据在user_profile

## 第二步

1. select device_id,gender,age,university,gpa
2. where (gpa > 3.5 and university = '山东大学') or (gpa > 3.8 and university = '复旦大学')
3. order by device_id asc
4. from user_profile

## 第三步

```sql
select device_id,gender,age,university,gpa
from user_profile
where (gpa > 3.5 and university = '山东大学') or (gpa > 3.8 and university = '复旦大学')
order by device_id asc;
```

---
# 🎯 SQL 排序关键字：`ORDER BY`

## 一、直接答案

|功能|关键字|示例|
|---|---|---|
|**排序**|`ORDER BY`|`ORDER BY age`|
|升序|`ASC` (默认)|`ORDER BY age ASC`|
|降序|`DESC`|`ORDER BY age DESC`|

---

## 二、基础语法

```sql
SELECT 字段1, 字段2, ...
FROM 表名
ORDER BY 排序字段 [ASC|DESC];
```

---

## 三、费曼学习法：用大白话解释

### 📚 想象整理书架

|场景|说法|SQL 写法|
|---|---|---|
|按年龄从小到大|升序|`ORDER BY age ASC`|
|按年龄从大到小|降序|`ORDER BY age DESC`|
|默认不写|自动升序|`ORDER BY age` = `ORDER BY age ASC`|

> **口诀**：`ASC` = 上升，`DESC` = 下降

---

## 四、实战示例

### 1️⃣ 单字段升序（默认）

```sql
-- 按年龄从小到大排序
SELECT device_id, age, university
FROM user_profile
ORDER BY age;
```

### 2️⃣ 单字段降序

```sql
-- 按年龄从大到小排序
SELECT device_id, age, university
FROM user_profile
ORDER BY age DESC;
```

### 3️⃣ 多字段排序

```sql
-- 先按学校排序，学校相同再按年龄排序
SELECT device_id, university, age
FROM user_profile
ORDER BY university, age;
```

### 4️⃣ 多字段不同方向

```sql
-- 学校升序，年龄降序
SELECT device_id, university, age
FROM user_profile
ORDER BY university ASC, age DESC;
```

---

## 五、排序方向对比表 📊

|关键字|全称|方向|示例|
|---|---|---|---|
|`ASC`|Ascending|升序（小→大）|`ORDER BY age ASC`|
|`DESC`|Descending|降序（大→小）|`ORDER BY age DESC`|

### 效果对比：

```
年龄数据：25, 20, 23, 21

ORDER BY age ASC  →  20, 21, 23, 25
ORDER BY age DESC →  25, 23, 21, 20
```

---

## 六、常见排序场景

|数据类型|升序效果|降序效果|
|---|---|---|
|数字|1, 2, 3, 4, 5|5, 4, 3, 2, 1|
|日期|2024-01-01 → 2024-12-31|2024-12-31 → 2024-01-01|
|字符串|A, B, C, D|D, C, B, A|
|NULL 值|通常排最前|通常排最后|

---

## 七、核心心法：排序口诀 📝

```
┌────────────────────────────────────────────────┐
│  排序关键字 → ORDER BY                         │
│                                                 │
│  升序 → ASC (可以省略，默认就是升序)             │
│  降序 → DESC (必须写出来)                       │
│                                                 │
│  记住口诀：                                     │
│  "ORDER 排顺序，ASC 升 DESC 降"                 │
│  不写方向 = 升序                               │
└────────────────────────────────────────────────┘
```

---

## 八、常见陷阱 ⚠️

|陷阱|错误写法|正确写法|
|---|---|---|
|拼写错误|`ORDER` ❌|`ORDER BY` ✅|
|方向写反|`ORDER BY age ASC` 想降序 ❌|`ORDER BY age DESC` ✅|
|多字段忘记逗号|`ORDER BY a b` ❌|`ORDER BY a, b` ✅|
|在 WHERE 前用|`ORDER BY age WHERE...` ❌|`WHERE... ORDER BY age` ✅|

---

## 九、SQL 语句执行顺序

```
1. FROM (从哪张表)
2. WHERE (筛选条件)
3. GROUP BY (分组)
4. HAVING (分组后筛选)
5. SELECT (选哪些字段)
6. ORDER BY (排序) ← 最后执行！
7. LIMIT (限制条数)
```

> **注意**：`ORDER BY` 是**最后执行**的，所以可以用 `SELECT` 里的别名！

```sql
-- 可以用别名排序
SELECT age AS 年龄
FROM user_profile
ORDER BY 年龄 DESC;  -- ✅ 可以这样写
```

---

## 十、总结：一张图记住排序

```
                    ORDER BY 排序
                         │
        ┌────────────────┴────────────────┐
        │                                 │
       升序                              降序
       ASC                               DESC
        │                                 │
   ORDER BY age                      ORDER BY age DESC
   (默认，可省略)                      (必须写)
```

---
