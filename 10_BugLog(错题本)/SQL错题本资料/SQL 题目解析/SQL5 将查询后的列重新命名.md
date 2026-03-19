---
PC地址: https://www.nowcoder.com/practice/0d8f49aeaf7a4e1cb7fecec980712113?tpId=199&tags=&title=&difficulty=0&judgeStatus=0&rp=0&sourceUrl=%2Fexam%2Foj%3Ftab%3DSQL%25E7%25AF%2587%26topicId%3D82
tags:
  - SQL
readingDate: 2026-03-19
---
![[SQL5.png]]

## 第一步:

1. 查看设备ID数据
2. 将设备ID列名改为'user_infos_example'
3. 前两个的数据
4. 数据在user_profile

## 第二步：翻译成sql

1. select device_id
2. **as** user_infos_example
3. limit 2
4. from user_profile

## 第三步：编写完整的SQL

```sql
select device_id as user_infos_example
form user_profile
limit 2;
```


### 为什么要用 AS？这样做有什么好处？

|为什么|好处（真实工作场景）|
|---|---|
|用 AS 改名|报表发给老板/运营时，列名是中文，他们一眼就懂|
|只改输出，不改表结构|安全！数据库里列名不变，以后别人查还是 device_id|
|AS 是全世界标准|其他数据库（PostgreSQL、SQL Server）也认 AS|
|可以一次改很多列|SELECT device_id AS 设备编号, age AS 年龄 ...|

**一句话背下来**： **“想改列名，就在列后面加 AS 新名字”** —— 这就是 MySQL 改名的核武器！