

```sql

CREATE TABLE `manager_login_admin` (
  `login_id` varchar(20) NOT NULL COMMENT '登录ID',
  `manager_id` varchar(20) DEFAULT NULL COMMENT '管理员ID',
  `status` varchar(30) NOT NULL COMMENT 'ManagerLoginAdminStatusEnum',
  `remark` varchar(200) DEFAULT NULL COMMENT '备注、失败原因等',
  `create_date` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP,
  `modify_date` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  PRIMARY KEY (`login_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='商户管理员登录PC管理后台';

```