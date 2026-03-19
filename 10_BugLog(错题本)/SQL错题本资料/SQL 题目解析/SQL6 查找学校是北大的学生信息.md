---
PC地址: https://www.nowcoder.com/practice/7858f3e234bc4d85b81b9a6c3926f49f?tpId=199&tags=&title=&difficulty=0&judgeStatus=0&rp=0&sourceUrl=%2Fexam%2Foj%3Ftab%3DSQL%25E7%25AF%2587%26topicId%3D82
tags:
  - SQL
readingDate: 2026-03-19
---
![[SQL6.png]]

## 第一步

1. 查看设备id和学校的数据
2. 只看北大的学生
3. 数据在user_profile

## 第二步

1. select device_id,university
2. where university = '北京大学'
3. from user_profile

## 第三步：编写完整的SQL

```sql
select device_id,university
from user_profile
where university = '北京大学';
```

## 为什么要这样改？这样做有什么好处？

|改动点|好处（真实工作场景）|
|---|---|
|SELECT 写两列|完全满足运营需求，不会少交作业|
|device_id 在前|输出表格和领导想要的顺序完全一致|
|用单引号 ' '（推荐）|MySQL 最标准写法，少出错|
|不加括号 WHERE ( )|括号可有可无，但不加代码更干净|

**一句话背下来**： **“要返回几列，就在 SELECT 后面写几列，用逗号隔开”** —— 这就是 SELECT 的核心！