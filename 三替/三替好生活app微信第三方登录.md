


```sql

-- 已同步上线

CREATE TABLE `bind_code` (
  `id` varchar(20) NOT NULL,
  `object_type` varchar(20) NOT NULL COMMENT '对象类型',
  `object_id` varchar(20) NOT NULL COMMENT '对象ID',
  `code_type` varchar(20) NOT NULL COMMENT 'code类型',
  `code` varchar(50) DEFAULT NULL COMMENT 'code',
  `source` varchar(50) DEFAULT NULL COMMENT '来源,域名',
  `app_id` varchar(64) DEFAULT NULL COMMENT 'appID',
  `create_date` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP,
  `modify_date` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  PRIMARY KEY (`id`),
  UNIQUE KEY `type` (`object_type`,`object_id`,`code_type`,`source`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='第三方登录绑定管理';

```