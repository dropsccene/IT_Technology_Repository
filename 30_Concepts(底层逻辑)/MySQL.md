## SQL
```
在shell内链接：\connect root@localhost:3306
```
### SQL语法
- SQL语句可以单行或多行，以分号结尾。
- SQL语句可以用空格/缩进来增强语句的可读性。
- MySQL数据库的SQL语句不分大小写，关键字建议大写。
- 注释：
```
	- 单行注释：-- 注释内容或 # 注释内容（MySQL特有）
	- 多行注释：/* 注释内容 */
```
### SQL分类
- DDL：数据定义语言，用来定义数据库对象（数据库、表、字段）
- DML：数据操作语言，用来对数据库表中的数据进行增删改
- DQL：数据查询语言，用来查询数据库中表的记录
  DCL：数据控制语言，用来创建数据库用户、控制数据库的访问权限
![[SQL分类.png]]
### DDL
#### DDL-数据库操作
- 查询
```
	- 查询所有数据库
	  SHOW DATABASES;
	- 查询当前数据库
	  SELECT DATABASE();
```
- 创建
```
	  CREATE DATABASE [IF NOT EXISTS] 数据库名 [DEFAULT CHARSET 字符集] [COLLATE 排序规则]
```
- 删除
```
	  DROP DATABASE[IF EXISTS]数据库名;
```
- 使用
```
	  USE 数据库名;
```
#### DDL-表操作
- 查询
```
	- 查询当前数据库所有表
	  SHOW TABLES;
	- 查询表结构
	  DESC 表名;
	- 查询指定表的建表语句
	  SHOW CREATE TABLE 表名;
```
- 创建
```
	- CREATE TABLE 表名(
	    字段1 字段1类型[COMMENT 字段1注释],
	    字段2 字段2类型[COMMENT 字段2注释],
	    ......
	    字段n 字段n类型[COMMENT 字段n注释]
	  )[COMMENT 表注释];
```
- 创建案例
![[DDL-创建表操作.png]]
#### DDL-数据类型
- 主要分为三类：数值、字符串、日期时间类型。
- 数值类型![[MySQL 数据类型 - 数值类型.png]]
- 字符串类型![[MySQL 数据类型 - 字符串类型.png]]
- 日期时间类型![[MySQL 数据类型 - 日期时间类型.png]]
- MySQL创建表案例![[MySQL创建表案例.png]]
- 查看表结构：
```
	- DESCRIBE 你的表名; 
	—- 或者简写 
	- DESC 你的表名;
```
#### DDL - 表操作 - 修改
- 添加字段
```
	- ALTER TABLE 表名 ADD 字段名 类型(长度) [COMMENT 注释] [约束];
```
- 案例：为emp表添加一个新的字段”昵称“为nickname，类型为varchar(20)
- 修改数据类型
```
	- ALTER TABLE 表名 MODIFY 字段名 新数据类型(长度);
```
- 修改字段名和字段类型
```
	- ALTER TABLE 表名 CHANGE 旧字段名 新字段名 类型(长度) [COMMENT 注释] [约束];
```
- 案例：将emp表的nickname字段修改为username，类型为varchar(30)
- 删除字段
```
	- ALTER TABLE 表名 DROP 字段名;
```
- 案例：将emp表中的字段username删除
- 修改表名
```
	- ALTER TABLE 表名 RENAME TO 新表名;
```
- 案例：将emp表中表名修改为employee
- 删除表
```
	- DROP TABLE [IF EXISTS] 表名;
```
- 删除指定表，并重新创建该表（**保留表结构定义**）
```
	- TRUNCATE TABLE 表名;
```
