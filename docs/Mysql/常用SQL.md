# 常用SQL
### DDL
**库的创建:**
create database if not exists 数据库名;

**字符集修改:**
alter database 库名 character set 字符集；

**库删除:**
drop database if exists 库名;

**创建表:**

``` mysql

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

**增加一个列：**
ALTER TABLE user ADD COLUMN username varchar(20) DEFAULT '' COMMENT '用户姓名';

**修改字段类型：**
ALTER TABLE USER MODIFY names varchar(100);

**修改字段名称：**
ALTER TABLE USER CHANGE 原字段名字  新的字段名字 字段类型;

**添加字段并指定位置：**
ALTER TABLE USER ADD 字段 字段类型  AFTER 字段;

**创建索：**
CREATE [UNIQUE] INDEX username ON USER(username);

**删除索引：**
DROP INDEX idxname

**添加主键：**
ALTER TABLE USER ADD PRIMARY KEY(user_id);

**删除主键：**
ALTER TABLE USER DROP PRIMARY KEY(user_id);
