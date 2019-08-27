### 小程序备注

- 一期添加后台管理账号

```sql
INSERT INTO cloud_train.`user` (id,job_id,username,login_id,miss_count,password,login_count,gender,phone,status,del_flag,create_time) VALUES ('5',NULL,'陈真明','13984458201','0','38e6f0f6c2432f64251d9ef8a7f5fad3','0','2','13984458201','1','1',now());
INSERT INTO cloud_train.user_role (id,user_id,role_id,del_flag,create_date) VALUES ('5','5','0','1',now());

INSERT INTO cloud_train.`user` (id,job_id,username,login_id,miss_count,password,login_count,gender,phone,status,del_flag,create_time) VALUES ('6',NULL,'张丽洋','18367135663','0','38e6f0f6c2432f64251d9ef8a7f5fad3','0','2','18367135663','1','1',now());
INSERT INTO cloud_train.user_role (id,user_id,role_id,del_flag,create_date) VALUES ('6','6','0','1',now());
```


# 小程序二期

### 建表

```sql
CREATE TABLE `activity_file` (
  `file_id` varchar(20) NOT NULL COMMENT '文件表ID',
  `activity_id` varchar(20) NOT NULL COMMENT '活动ID',
  `file_name` varchar(255) NOT NULL COMMENT '文件名',
  `file_type` varchar(5) NOT NULL COMMENT '活动文件类型,对应ActivityFileEnum类',
  `url` varchar(255) NOT NULL COMMENT '文件url',
  `del_flag` varchar(1) NOT NULL DEFAULT '1' COMMENT '逻辑删除（置0）',
  `create_id` varchar(20) NOT NULL COMMENT '创建人ID',
  `create_date` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `modify_id` varchar(20) DEFAULT NULL COMMENT '修改人ID',
  `modify_date` timestamp NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP COMMENT '修改时间',
  PRIMARY KEY (`file_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='活动文件表';

CREATE TABLE `activity_file_finish_log` (
  `finish_log_id` varchar(20) NOT NULL COMMENT '完成记录ID',
  `file_id` varchar(20) NOT NULL COMMENT '文件ID',
  `member_id` varchar(20) NOT NULL COMMENT '会员ID',
  `del_flag` varchar(1) NOT NULL DEFAULT '1' COMMENT '逻辑删除（置0）',
  `create_id` varchar(20) NOT NULL COMMENT '创建人ID',
  `create_date` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `modify_id` varchar(20) DEFAULT NULL COMMENT '修改人ID',
  `modify_date` timestamp NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP COMMENT '修改时间',
  PRIMARY KEY (`finish_log_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='活动文件完成记录表';

CREATE TABLE `dynamic_file` (
  `file_id` varchar(20) NOT NULL COMMENT '活动动态信息文件id（评论/打卡信息文件id）',
  `dynamic_id` varchar(20) NOT NULL COMMENT '活动动态信息id',
  `file_name` varchar(50) DEFAULT NULL COMMENT '文件名',
  `url` varchar(255) NOT NULL COMMENT '文件url',
  `file_type` varchar(5) NOT NULL COMMENT '文件类型，（DynamicFileTypeEnum）',
  `duration` varchar(20) DEFAULT NULL COMMENT '时长（音频）',
  `del_flag` varchar(1) NOT NULL DEFAULT '1' COMMENT '逻辑删除（置0）',
  `create_id` varchar(20) NOT NULL COMMENT '创建人ID',
  `create_date` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `modify_id` varchar(20) DEFAULT NULL COMMENT '修改人ID',
  `modify_date` timestamp NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP COMMENT '修改时间',
  PRIMARY KEY (`file_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='活动动态信息相关文件表（评论/打卡信息文件表）';

CREATE TABLE `member_credit_log` (
  `credit_log_id` varchar(20) NOT NULL COMMENT '积分记录ID',
  `member_id` varchar(20) NOT NULL COMMENT '白名单会员ID',
  `activity_id` varchar(20) NOT NULL COMMENT '活动id',
  `object_id` varchar(20) NOT NULL COMMENT '获取积分项ID',
  `object_type` varchar(5) NOT NULL COMMENT '获取积分项类型（CreditLogObjectTypeEnum）',
  `credit` int(11) NOT NULL DEFAULT '0' COMMENT '获得积分',
  `del_flag` varchar(1) NOT NULL DEFAULT '1' COMMENT '逻辑删除（置0）',
  `create_id` varchar(20) NOT NULL COMMENT '创建人ID',
  `create_date` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `modify_id` varchar(20) DEFAULT NULL COMMENT '修改人ID',
  `modify_date` timestamp NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP COMMENT '修改时间',
  PRIMARY KEY (`credit_log_id`),
  KEY `member_id_index` (`member_id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='会员获取积分记录表';

CREATE TABLE `activity_member` (
  `id` varchar(20) NOT NULL COMMENT '活动会员对应表id',
  `activity_id` varchar(20) NOT NULL COMMENT '活动id',
  `member_id` varchar(20) NOT NULL COMMENT '会员id',
  `is_must` char(1) NOT NULL DEFAULT '1' COMMENT '逻辑删除用（置0）',
  `standard_flag` varchar(2) NOT NULL DEFAULT '0' COMMENT '是否达标0=否，1=是',
  `del_flag` char(1) NOT NULL,
  `create_time` datetime NOT NULL ON UPDATE CURRENT_TIMESTAMP COMMENT '创建时间',
  `create_id` varchar(20) DEFAULT NULL COMMENT '创建人ID',
  `modify_time` datetime DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP COMMENT '修改时间',
  `modify_id` varchar(20) DEFAULT NULL COMMENT '修改人ID'
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='活动会员对应表';

```

### 修改字段

```sql
ALTER TABLE train.activity MODIFY COLUMN `create_time` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '发布时间';

ALTER TABLE train.activity DROP COLUMN activity_image;

ALTER TABLE train.activity DROP COLUMN video;

ALTER TABLE train.activity DROP COLUMN cover_picture;

ALTER TABLE train.activity DROP COLUMN file;

ALTER TABLE dynamic MODIFY COLUMN `clock_time` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '评论/打卡时间';

ALTER TABLE dynamic ADD COLUMN `useful` varchar(2) NOT NULL DEFAULT '0' COMMENT '是否有效0=否，1=是';

ALTER TABLE dynamic DROP COLUMN `image`;

ALTER TABLE dynamic DROP COLUMN `audio`;

```

```sql
SELECT wl.username,wl.phone
FROM member_credit_log mcl 
LEFT JOIN activity a ON a.id = mcl.activity_id 
LEFT JOIN white_list wl ON wl.id = mcl.member_id 
WHERE mcl.del_flag = '1' AND a.del_flag = '1' AND wl.del_flag = '1' 
GROUP BY wcl.member_id,wcl.activity_id 
ORDER BY mcl.member_id,


SELECT mcl.member_id,mcl.date,IFNULL(mcl.count_code * a.credit,0) msu_creadit,wl.username,wl.phone
FROM (
	SELECT member_id,activity_id,DATE_FORMAT(create_date,'%Y-%m') date,count(activity_id) count_code
	FROM member_credit_log 
	
	WHERE del_flag = '1'
	GROUP BY member_id,activity_id,DATE_FORMAT(create_date,'%Y-%m') 
) mcl
LEFT JOIN activity a ON a.id = mcl.activity_id AND a.del_flag = '1'
LEFT JOIN white_list wl ON wl.id = mcl.member_id AND wl.del_flag = '1' 
WHERE 1=1 
GROUP BY mcl.member_id,mcl.date;
```