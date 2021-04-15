

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

```sql

-- ----------------------------
-- 同步数据库
-- ----------------------------

-- 字段修改
ALTER TABLE daily_user_statistics ADD COLUMN `new_register_user_num` int(11) NOT NULL DEFAULT 0 COMMENT '新注册用户数量' AFTER new_users_num;
ALTER TABLE daily_user_statistics CHANGE COLUMN `active_users_num` `order_new_user_num` int(11) NOT NULL DEFAULT '0' COMMENT '下单新用户数量';
ALTER TABLE daily_user_statistics CHANGE COLUMN `launch_num` `order_old_user_num` int(11) NOT NULL DEFAULT '0' COMMENT '下单老用户数量';

-- 先清空表数据
TRUNCATE TABLE statistics_user;

-- 字段修改
ALTER TABLE statistics_user MODIFY COLUMN `cid` varchar(64) DEFAULT NULL COMMENT '设备号';
ALTER TABLE statistics_user MODIFY COLUMN `user_id` varchar(64) DEFAULT NULL COMMENT '用户ID';

-- 索引修改
ALTER TABLE statistics_user DROP INDEX `unique_user_id`;
ALTER TABLE statistics_user ADD UNIQUE INDEX `unique_cid` (`app_id`, `cid`);
ALTER TABLE statistics_user ADD UNIQUE INDEX `unique_user_id` (`app_id`, `user_id`);

-- 老用户数据插入统计用户表
INSERT INTO statistics_user (id, app_id, cid, user_id, date_str)
SELECT ID, 'zjialianH5', ID, ID, '2021-04-02' FROM member WHERE TO_DAYS(CREATE_DATE) < TO_DAYS('2021-04-02');


-- 下单日志丢失，手动补齐统计数据（重新跑完后再跑这几条sql）
UPDATE daily_user_statistics SET order_new_user_num = 12, order_old_user_num = 102, new_user_orders_num = 12, old_user_orders_num = 129, user_orders_num = 141 WHERE date_str = '2021-04-02';
UPDATE daily_user_statistics SET order_new_user_num = 9, order_old_user_num = 65, new_user_orders_num = 13, old_user_orders_num = 76, user_orders_num = 89 WHERE date_str = '2021-04-03';
UPDATE daily_user_statistics SET order_new_user_num = 7, order_old_user_num = 89, new_user_orders_num = 7, old_user_orders_num = 104, user_orders_num = 111 WHERE date_str = '2021-04-04';
UPDATE daily_user_statistics SET order_new_user_num = 15, order_old_user_num = 82, new_user_orders_num = 15, old_user_orders_num = 96, user_orders_num = 111 WHERE date_str = '2021-04-05';

-- 2021-04-06下单统计
UPDATE daily_user_statistics SET order_new_user_num = 8, order_old_user_num = 78, new_user_orders_num = 8, old_user_orders_num = 102, user_orders_num = 110 WHERE date_str = '2021-04-06';

-- 新注册用户
UPDATE daily_user_statistics SET new_register_user_num = 6 WHERE date_str = '2021-04-02';
UPDATE daily_user_statistics SET new_register_user_num = 12 WHERE date_str = '2021-04-03';
UPDATE daily_user_statistics SET new_register_user_num = 4 WHERE date_str = '2021-04-04';
UPDATE daily_user_statistics SET new_register_user_num = 6 WHERE date_str = '2021-04-05';
UPDATE daily_user_statistics SET new_register_user_num = 9 WHERE date_str = '2021-04-06';





-- ----------------------------
-- 以上数据可以拿到正是环境同步
-- ----------------------------



-- 下单日志丢失，手动补齐统计数据（重新跑完后再跑这几条sql）
UPDATE daily_user_statistics SET new_register_user_num = 6, order_new_user_num = 12, order_old_user_num = 102, new_user_orders_num = 12, old_user_orders_num = 129, user_orders_num = 141 WHERE date_str = '2021-04-02';
UPDATE daily_user_statistics SET new_register_user_num = 12, order_new_user_num = 9, order_old_user_num = 65, new_user_orders_num = 13, old_user_orders_num = 76, user_orders_num = 89 WHERE date_str = '2021-04-03';
UPDATE daily_user_statistics SET new_register_user_num = 4, order_new_user_num = 7, order_old_user_num = 89, new_user_orders_num = 7, old_user_orders_num = 104, user_orders_num = 111 WHERE date_str = '2021-04-04';
UPDATE daily_user_statistics SET new_register_user_num = 6, order_new_user_num = 15, order_old_user_num = 82, new_user_orders_num = 15, old_user_orders_num = 96, user_orders_num = 111 WHERE date_str = '2021-04-05';
UPDATE daily_user_statistics SET new_register_user_num = 9, order_new_user_num = 8, order_old_user_num = 78, new_user_orders_num = 8, old_user_orders_num = 102, user_orders_num = 110 WHERE date_str = '2021-04-06';

UPDATE daily_user_statistics SET new_register_user_num = 7 WHERE date_str = '2021-04-07';
UPDATE daily_user_statistics SET new_register_user_num = 7 WHERE date_str = '2021-04-08';






UPDATE daily_user_statistics SET new_user_orders_num = 11, old_user_orders_num = 80, user_orders_num = 91 WHERE date_str = '2021-04-01';
UPDATE daily_user_statistics SET new_user_orders_num = 12, old_user_orders_num = 129, user_orders_num = 141 WHERE date_str = '2021-04-02';
UPDATE daily_user_statistics SET new_user_orders_num = 13, old_user_orders_num = 76, user_orders_num = 89 WHERE date_str = '2021-04-03';
UPDATE daily_user_statistics SET new_user_orders_num = 7, old_user_orders_num = 104, user_orders_num = 111 WHERE date_str = '2021-04-04';
UPDATE daily_user_statistics SET new_user_orders_num = 15, old_user_orders_num = 96, user_orders_num = 111 WHERE date_str = '2021-04-05';


```