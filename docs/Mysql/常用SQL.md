# 常用SQL
### DDL
**库的创建:**```mysql create database if not exists 数据库名;```

**字符集修改:**
```mysql
alter database 库名 character set 字符集；
```

**库删除:**

	drop database if exists 库名;

**创建表:**

```mysql

	CREATE TABLE `scs_group_send` (
	
	  `id` int(11) unsigned NOT NULL AUTO_INCREMENT COMMENT '主键id',
	
	  `num` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '群发人数',
	
	  `group_name` varchar(50) COLLATE utf8_unicode_ci NOT NULL DEFAULT '' COMMENT '群名称',
	
	  `group_id` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '群id',
	
	  `itime` int(11) NOT NULL DEFAULT '0' COMMENT '创建时间',
	
	  `utime` int(11) NOT NULL DEFAULT '0' COMMENT '最新更新时间',
	
	  `dtime` int(11) NOT NULL DEFAULT '0' COMMENT '删除时间',
	
	  `datastatus` tinyint(1) NOT NULL DEFAULT '1' COMMENT '0删除1正常2停用',
	
	  PRIMARY KEY (`id`),
	
	  KEY `GroupName` (`group_name`),
	
	  KEY `GroupID` (`group_id`)
	
	) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci COMMENT='群发管理'
```

**删除新表：**

	DROP TABLE tabname;

**增加一个列：**

	ALTER TABLE user ADD COLUMN username varchar(20) DEFAULT '' COMMENT '用户姓名';

**修改字段类型：**

	ALTER TABLE USER MODIFY names varchar(100);

**修改字段名称：**

	ALTER TABLE USER CHANGE 原字段名字  新的字段名字 字段类型;

**添加字段并指定位置：**

	ALTER TABLE USER ADD 字段 字段类型  AFTER 字段;

**创建索引：**

	CREATE [UNIQUE] INDEX username ON USER(username);

**删除索引：**

	DROP INDEX idxname

**添加主键：**

	ALTER TABLE USER ADD PRIMARY KEY(user_id);

**删除主键：**

	ALTER TABLE USER DROP PRIMARY KEY(user_id);

##查询

**子查询：**

	SELECT a,b,c FROM a WHERE a IN (SELECT d FROM b ) 或者: SELECT a,b,c FROM a WHERE a IN (1,2,3)

**左连接查询：**

	SELECT student.name,class.sex,class.xuehao FROM class LEFT JOIN student ON class.id=student.cid;

**if判断查询：**

	SELECT *,IF(salary>2000,'high','low') AS statu FROM salary;

	SELECT CASE  salary  WHEN salary<=2000 THEN 'low' ELSE 'high' END FROM salary;

**mysql差集：**

	SELECT a FROM table1 ONE LEFT JOIN table2 two ON table1.id = table2.id WHERE one.a != two.a;

**分组聚合(group)：**

	SELECT `student`, AVG(`score`) AS `avg_score` FROM `courses` WHERE student='张三' GROUP BY `student` HAVING AVG(`score`) >= 60 ORDER BY `avg_score` DESC;

**CONCAT的使用：**

	SELECT CONCAT(username,'wsq') AS new_name FROM `user`;

	SELECT CONCAT(NAME," nianling is" ,age) FROM class; 

**左连接和group by一起使用的例子：**

	SELECT h.* , COUNT(lh.id) cishu FROM abap_hg AS h LEFT JOIN abap_hg_log AS lh ON h.uc_x = lh.uc_x WHERE h.uc_x != '' GROUP BY h.uc_x ORDER BY cishu DESC LIMIT 0 , 30

**求和、平均、最大、最小值：**

	SELECT SUM(age) FROM biao;

	SELECT AVG(age) FROM biao;

	SELECT MAX(id) FROM biao;

	SELECT MIN(age) FROM biao;

