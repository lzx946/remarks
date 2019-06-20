### 小程序备注

- 一期添加后台管理账号

```sql
INSERT INTO cloud_train.`user` (id,job_id,username,login_id,miss_count,password,login_count,gender,phone,status,del_flag,create_time) VALUES ('5',NULL,'陈真明','13984458201','0','38e6f0f6c2432f64251d9ef8a7f5fad3','0','2','13984458201','1','1',now());
INSERT INTO cloud_train.user_role (id,user_id,role_id,del_flag,create_date) VALUES ('5','5','0','1',now());

INSERT INTO cloud_train.`user` (id,job_id,username,login_id,miss_count,password,login_count,gender,phone,status,del_flag,create_time) VALUES ('6',NULL,'张丽洋','18367135663','0','38e6f0f6c2432f64251d9ef8a7f5fad3','0','2','18367135663','1','1',now());
INSERT INTO cloud_train.user_role (id,user_id,role_id,del_flag,create_date) VALUES ('6','6','0','1',now());
```