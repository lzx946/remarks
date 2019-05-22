## 【ID1000128】确认订单页面提醒

### 添加“确认订单页面说明”字段

```sql
ALTER TABLE mall_goods_sku ADD COLUMN confirm_order_description VARCHAR(255) DEFAULT NULL COMMENT '确认订单页面说明';
```

### MallGoodsDto中，添加confirmOrderDescription字段

```java
private String confirmOrderDescription;//确认订单页面说明
```

### saveSku接口,添加以下代码

```java
        if(map.getConfirmOrderDescription()!=null&&!StringUtil.isEmpty(map.getConfirmOrderDescription())){
            if(map.getConfirmOrderDescription().length()>200) {
                return ResultDtoFactory.toNack("请添加200字以内的说明");
            }
        }
```

### dao层：saveMallGoodsSku和modifyMallGoodsSku方法，添加confirm_order_description字段

```sql
    //添加商品sku
    @Insert("INSERT INTO mall_goods_sku (sku_id,spu_id,original_price,current_price,additional_proceeds,sku_stock,sales_volume,merchant_id," +
            "item_name,subtitle,images,unit,use_range,sku_remark,confirm_order_description,time_show_flag,sku_is_deleted,create_id,remark_template,choose_emp_flag," +
            "notice_name,notice_content,allow_pay_type,stock_type,choose_date_num,emp_max_distance,create_date,max_emp_num,batch_id) " +
            "VALUES(#{sku_id},#{spu_id},#{original_price},#{current_price},#{additional_proceeds},#{sku_stock},#{sales_volume},#{merchant_id}," +
            "#{item_name},#{subtitle},#{images},#{unit},#{use_range},#{sku_remark},#{confirmOrderDescription},#{time_show_flag},'1',#{create_id},#{remarkTemplate},#{chooseEmpFlag}," +
            "#{noticeName},#{noticeContent},#{allowPayType},#{stockType},#{chooseDateNum},#{empMaxDistance},now(),#{maxEmpNum},#{batchId})")
    void saveMallGoodsSku(MallGoodsDto map);


    //修改商品sku
    @Update("update mall_goods_sku set original_price=#{original_price},current_price=#{current_price},item_name=#{item_name},subtitle=#{subtitle},images=#{images}," +
            "unit=#{unit},use_range=#{use_range},sku_remark=#{sku_remark},confirm_order_description=#{confirmOrderDescription},modify_id=#{modify_id},remark_template=#{remarkTemplate},choose_emp_flag=#{chooseEmpFlag}," +
            "notice_name=#{noticeName},notice_content=#{noticeContent},allow_pay_type=#{allowPayType},stock_type=#{stockType},sku_stock=#{stock},choose_date_num=#{chooseDateNum}," +
            "emp_max_distance=#{empMaxDistance},max_emp_num=#{maxEmpNum},batch_id=#{batchId}, supplement_price=#{supplement_price}" +
            "  where sku_id=#{sku_id}")
    void modifyMallGoodsSku(MallGoodsDto map);
```