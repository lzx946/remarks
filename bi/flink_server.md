

```sql

CREATE TABLE `daily_user_statistics` (
  `id` varchar(20) NOT NULL COMMENT 'ID',
  `new_users_num` int(11) NOT NULL DEFAULT '0' COMMENT '新增用户数',
  `active_users_num` int(11) NOT NULL DEFAULT '0' COMMENT '活跃用户数',
  `launch_num` int(11) NOT NULL DEFAULT '0' COMMENT '启动次数',
  `new_user_orders_num` int(11) NOT NULL DEFAULT '0' COMMENT '新用户下单数',
  `old_user_orders_num` int(11) NOT NULL DEFAULT '0' COMMENT '老用户下单数',
  `user_orders_num` int(11) NOT NULL DEFAULT '0' COMMENT '总下单数',
  `date_str` varchar(10) NOT NULL DEFAULT '' COMMENT '统计日期',
  `create_date` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `modify_date` timestamp NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP COMMENT '修改时间',
  PRIMARY KEY (`id`),
  UNIQUE KEY `date_str` (`date_str`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='每日用户统计';

CREATE TABLE `statistics_user` (
  `id` varchar(20) NOT NULL COMMENT 'ID',
  `app_id` varchar(64) NOT NULL DEFAULT '' COMMENT '应用ID',
  `cid` varchar(64) NOT NULL DEFAULT '' COMMENT '设备号',
  `user_id` varchar(64) NOT NULL DEFAULT '' COMMENT '用户ID',
  `date_str` varchar(10) NOT NULL DEFAULT '' COMMENT '统计日期',
  `create_date` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `modify_date` timestamp NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP COMMENT '修改时间',
  PRIMARY KEY (`id`),
  UNIQUE KEY `unique_user_id` (`app_id`,`cid`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='统计用户';

CREATE TABLE `basic_statistics` (
  `id` varchar(20) NOT NULL COMMENT 'ID',
  `pv` int(11) NOT NULL DEFAULT '0' COMMENT '浏览量',
  `uv` int(11) NOT NULL DEFAULT '0' COMMENT '独立用户数量',
  `vv` int(11) NOT NULL DEFAULT '0' COMMENT '访问量',
  `independent_ip` int(11) NOT NULL DEFAULT '0' COMMENT '独立IP数量',
  `date_str` varchar(10) NOT NULL DEFAULT '' COMMENT '统计日期',
  `create_date` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `modify_date` timestamp NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP COMMENT '修改时间',
  PRIMARY KEY (`id`),
  UNIQUE KEY `date_str` (`date_str`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='基本指标统计';

```