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
  `create_date` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
	`modify_id` varchar(20) DEFAULT NULL COMMENT '修改人ID',
	`modify_date` TIMESTAMP NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP COMMENT '修改时间',
  PRIMARY KEY (`file_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='活动文件表';
```

### 修改字段

```sql
ALTER TABLE train.activity MODIFY COLUMN `create_time` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '发布时间';

ALTER TABLE train.activity DROP COLUMN activity_image;

ALTER TABLE train.activity DROP COLUMN video;

ALTER TABLE train.activity DROP COLUMN cover_picture;

ALTER TABLE train.activity DROP COLUMN file;

```