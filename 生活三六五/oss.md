## 创建统一文件映射索引表

```sql
-- 文件映射关系索引表
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

-- 文件迁移日志表
CREATE TABLE `file_transfer_log` (
  `log_id` varchar(20) NOT NULL,
  `table_name` varchar(50) NOT NULL COMMENT '迁移的表名',
  `column_id_name` varchar(50) NOT NULL COMMENT '主键字段名',
  `column_id_value` varchar(20) NOT NULL COMMENT '主键字段值',
  `column_url_name` varchar(50) NOT NULL COMMENT '文件路径字段名',
  `original_file_key` varchar(2000) NOT NULL COMMENT '原来的key（ftp文件路径）',
  `new_file_key` varchar(2000) DEFAULT NULL COMMENT '新文件key（oss文件路径）',
  `file_id` varchar(1000) DEFAULT NULL COMMENT '文件ID，关联file_mapping表的file_id',
  `del_flag` varchar(1) NOT NULL DEFAULT '1' COMMENT '逻辑删除0：删除　1：未删除',
  `create_id` varchar(20) DEFAULT NULL COMMENT '创建人',
  `modify_id` varchar(20) DEFAULT NULL COMMENT '修改人',
  `create_date` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `modify_date` timestamp NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP COMMENT '修改时间',
  PRIMARY KEY (`log_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='文件迁移日志表';

```

## 需要替换的接口

|原接口|现接口|
|:---:|:---:|
|/mall/main/addImage/{source}|/mall/file/upload/{source}|
|/mall/main/addVideo/{source}|/mall/file/upload/{source}|
|/mall/main/addImage2/{source}|/mall/file/upload/{source}|
|/mall/main/addXls|/mall/file/upload/54|
|/order/orderAppEmp/addMp3|/mall/file/upload/52|
|/order/eContract/uploadContractTemplate|/mall/file/upload/51|
|/user/memberInfo/updateHeadImage|/mall/file/upload/50|
 
 
## 需要确认接口还有用吗

/mall/empCredit/getEmpIDPhotos
/getEmpIDPhotosTest