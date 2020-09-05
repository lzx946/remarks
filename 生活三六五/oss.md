## 创建统一文件映射索引表

```sql

CREATE TABLE `file_mapping` (
  `file_id` varchar(20) NOT NULL,
  `file_key` varchar(255) NOT NULL,
  `del_flag` varchar(1) NOT NULL DEFAULT '1' COMMENT '逻辑删除0：删除　1：未删除',
  `create_id` varchar(20) DEFAULT NULL COMMENT '创建人',
  `modify_id` varchar(20) DEFAULT NULL COMMENT '修改人',
  `create_date` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `modify_date` timestamp NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP COMMENT '修改时间',
  PRIMARY KEY (`file_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='文件映射关系索引表';

```