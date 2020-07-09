
## 查询家政企业数量和明细

```sql

SELECT * FROM SWJ_V_SCJGJ_QYHZNR 
WHERE XKJYXM LIKE '%普通货运%' 
	 OR XKJYXM LIKE '%仓储理货%' 
	 OR XKJYXM LIKE '%搬家运输%' 
	 OR XKJYXM LIKE '%城市快运%' 
	 OR XKJYXM LIKE '%陪护服务%' 
	 OR XKJYXM LIKE '%月嫂陪护%' 
	 OR XKJYXM LIKE '%医院后勤服务%'
	 OR XKJYXM LIKE '%生活照料%'
	 OR XKJYXM LIKE '%康复护理%'
	 OR XKJYXM LIKE '%日间照料%'
	 OR XKJYXM LIKE '%助援服务%'
	 OR XKJYXM LIKE '%社区居家养老服务%'
	 OR XKJYXM LIKE '%家政服务%'
	 OR XKJYXM LIKE '%物业管理%'
	 OR XKJYXM LIKE '%下水道专业疏通%'
	 OR XKJYXM LIKE '%提供劳务服务%'
	 OR XKJYXM LIKE '%水箱清洗%'
	 OR XKJYXM LIKE '%家电维修%';
	 
	 
SELECT COUNT(DISTINCT UNISCID) FROM SWJ_V_SCJGJ_QYHZNR 
WHERE XKJYXM LIKE '%普通货运%' 
	 OR XKJYXM LIKE '%仓储理货%' 
	 OR XKJYXM LIKE '%搬家运输%' 
	 OR XKJYXM LIKE '%城市快运%' 
	 OR XKJYXM LIKE '%陪护服务%' 
	 OR XKJYXM LIKE '%月嫂陪护%' 
	 OR XKJYXM LIKE '%医院后勤服务%'
	 OR XKJYXM LIKE '%生活照料%'
	 OR XKJYXM LIKE '%康复护理%'
	 OR XKJYXM LIKE '%日间照料%'
	 OR XKJYXM LIKE '%助援服务%'
	 OR XKJYXM LIKE '%社区居家养老服务%'
	 OR XKJYXM LIKE '%家政服务%'
	 OR XKJYXM LIKE '%物业管理%'
	 OR XKJYXM LIKE '%下水道专业疏通%'
	 OR XKJYXM LIKE '%提供劳务服务%'
	 OR XKJYXM LIKE '%水箱清洗%'
	 OR XKJYXM LIKE '%家电维修%';


SELECT * FROM SWJ_V_SCJGJ_QYHZNR WHERE JYFW LIKE '%家政%';


```