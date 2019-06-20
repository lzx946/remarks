## 小程序加积分日志

- 创建积分表

```sql
CREATE TABLE `credit_log` (
  `credit_log_id` varchar(20) NOT NULL COMMENT '日志ID',
  `member_id` varchar(20) NOT NULL COMMENT '会员ID',
  `credit` int(10) NOT NULL DEFAULT '0' COMMENT '加减分分值',
	`type` VARCHAR(1) NOT NULL COMMENT '积分变动类型（0=确认到场改变积分；1==评论改变积分）',
	`activity_id` VARCHAR(20) DEFAULT NULL COMMENT '活动ID',
	`dynamic_id` VARCHAR(20) DEFAULT NULL COMMENT '评论ID（type=1时不为空）',
	`application_id` VARCHAR(20) DEFAULT NULL COMMENT '报名信息ID（type=0时不为空）',
  `week_credit_before` int(10) DEFAULT NULL COMMENT '操作前周积分',
  `week_credit_after` int(10) DEFAULT NULL COMMENT '操作后周积分',
  `quarter_credit_before` int(10) DEFAULT NULL COMMENT '操作前季度积分',
  `quarter_credit_after` int(10) DEFAULT NULL COMMENT '操作后季度积分',
  `total_credit_before` int(10) NOT NULL DEFAULT '0' COMMENT '操作前总积分',
  `total_credit_after` int(10) NOT NULL DEFAULT '0' COMMENT '操作后总积分',
  `remark` varchar(255) NOT NULL DEFAULT '' COMMENT '操作备注/详情',
  `cancel_flag` varchar(1) NOT NULL DEFAULT '1' COMMENT '是否可以取消，1==可以，0==不可以',
  `del_flag` varchar(1) NOT NULL DEFAULT '1' COMMENT '逻辑删除用（置0）',
  `create_date` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP,
  `create_id` varchar(20) DEFAULT NULL,
  `modify_date` timestamp NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP,
  `modify_id` varchar(20) DEFAULT NULL,
  PRIMARY KEY (`credit_log_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='积分日志表';

ALTER TABLE cloud_train.application ADD COLUMN confirm_time TIMESTAMP NULL DEFAULT NULL COMMENT '确认到场时间';

ALTER TABLE cloud_train.credit_log ADD COLUMN cancel VARCHAR(1) NOT NULL DEFAULT '0' COMMENT '操作是否撤销';
```