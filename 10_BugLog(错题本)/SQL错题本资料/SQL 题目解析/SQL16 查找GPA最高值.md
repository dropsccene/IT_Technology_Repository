---
PC地址: https://www.nowcoder.com/practice/4e22fc5dbd16414fb2c7683557a84a4f?tpId=199&tags=&title=&difficulty=0&judgeStatus=0&rp=0&sourceUrl=%2Fexam%2Foj%3Ftab%3DSQL%25E7%25AF%2587%26topicId%3D82
tags:
  - SQL
---
![[SQL16.png]]

## 第一步

1. 查看gpa最高值
2. 筛选复旦大学的学生的数据
3. 结果保留小数点后面1位
4. 数据在user_profile

## 第二步

1. select max(gpa)
2. where university = '复旦大学'
3. round(max(gpa),1)
4. from user_profile

## 第三步

```sql
select round(max(gpa),1)
from user_profile
where university = '复旦大学';
```


# 📋 题目完整总结：复旦大学最高GPA查询

---

## 一、题目信息 🎯

|项目|内容|
|---|---|
|**题目目标**|查询复旦大学学生的最高GPA|
|**输出要求**|结果保留到小数点后1位|
|**输出列名**|`gpa`|
|**数据表**|`user_profile`|
|**筛选条件**|`university = '复旦大学'`|

---

## 二、数据样例 📊

```
┌────┬──────────┬──────┬────────────┬───────┐
│ id │ device_id│ gender│ university │  gpa  │
├────┼──────────┼──────┼────────────┼───────┤
│ 1  │ 2138     │ male │ 北京大学   │ 3.4   │
│ 2  │ 3214     │ male │ 复旦大学   │ 3.8   │ ← 最大值
│ 3  │ 5432     │ female│ 复旦大学  │ 3.5   │
│ 4  │ 2315     │ female│ 浙江大学  │ 3.6   │
│ 5  │ 5423     │ male │ 复旦大学   │ 3.1   │
└────┴──────────┴──────┴────────────┴───────┘
```

**预期输出：**

```
┌──────┐
│ gpa  │
├──────┤
│ 3.8  │
└──────┘
```

---

## 三、正确代码 ✅

```sql
SELECT ROUND(MAX(gpa), 1) AS gpa
FROM user_profile
WHERE university = '复旦大学';
```

---

## 四、解题思路 🧠

```
┌─────────────────────────────────────────────────────────┐
│                    解题步骤                              │
├─────────────────────────────────────────────────────────┤
│  1️⃣ 确定目标：取最大值 → MAX(gpa)                       │
│  2️⃣ 确定表：用户信息表 → FROM user_profile              │
│  3️⃣ 确定条件：复旦大学 → WHERE university = '复旦大学'   │
│  4️⃣ 格式要求：保留1位小数 → ROUND(..., 1)               │
│  5️⃣ 列名要求：输出列名为gpa → AS gpa                    │
└─────────────────────────────────────────────────────────┘
```

---

## 五、关键知识点 📝

|知识点|关键字/函数|作用|
|---|---|---|
|聚合函数|`MAX()`|取最大值|
|数值处理|`ROUND()`|保留小数位|
|条件筛选|`WHERE`|过滤数据|
|列别名|`AS`|重命名输出列|
|字符串匹配|`=`|精确匹配|

---

## 六、易错点提醒 ⚠️

|易错点|错误写法|正确写法|
|---|---|---|
|缺少列别名|`SELECT ROUND(MAX(gpa),1)`|`SELECT ROUND(MAX(gpa),1) AS gpa`|
|ROUND位置错|`ROUND(MAX(gpa, 1))`|`ROUND(MAX(gpa), 1)`|
|字符串无引号|`WHERE university = 复旦大学`|`WHERE university = '复旦大学'`|
|表名错误|`FROM user_profiles`|`FROM user_profile`|
|字段名错误|`MAX(GPA)`|`MAX(gpa)`|

---

## 七、代码拆解 🔍

```sql
-- 第1部分：选择什么（取最大值+保留1位小数+列别名）
SELECT ROUND(MAX(gpa), 1) AS gpa

-- 第2部分：从哪来（数据表）
FROM user_profile

-- 第3部分：筛选条件（复旦大学）
WHERE university = '复旦大学';
```

---

## 八、扩展练习 💡

|变体需求|SQL代码|
|---|---|
|最低GPA|`SELECT ROUND(MIN(gpa), 1) AS gpa FROM user_profile WHERE university = '复旦大学'`|
|平均GPA|`SELECT ROUND(AVG(gpa), 1) AS gpa FROM user_profile WHERE university = '复旦大学'`|
|学生人数|`SELECT COUNT(*) AS cnt FROM user_profile WHERE university = '复旦大学'`|
|所有学校最高GPA|`SELECT university, ROUND(MAX(gpa), 1) AS gpa FROM user_profile GROUP BY university`|

---

## 九、记忆口诀 📖

```
┌────────────────────────────────────────────────┐
│  聚合查询三步走：                               │
│  1. SELECT + 聚合函数 (MAX/MIN/AVG/COUNT)      │
│  2. FROM + 表名                               │
│  3. WHERE + 筛选条件                          │
│                                                 │
│  格式要求别忘记：                               │
│  ROUND(字段, 小数位) + AS 列名                 │
└────────────────────────────────────────────────┘
```

---

## 十、一张图总结 🎯

```
                        题目：复旦大学最高GPA
                                  │
                    ┌─────────────┼─────────────┐
                    │             │             │
                用什么函数     从哪张表     什么条件
                    │             │             │
                 MAX(gpa)    user_profile   university='复旦大学'
                    │
                    ▼
                格式处理
                    │
            ROUND(..., 1) + AS gpa
                    │
                    ▼
            SELECT ROUND(MAX(gpa), 1) AS gpa
            FROM user_profile
            WHERE university = '复旦大学';
```

---

**总结完成！** 这道题是SQL聚合函数的基础入门题，掌握后可以做更多变体练习。🚀
