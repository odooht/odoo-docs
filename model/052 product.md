## Product

![product](https://github.com/odooht/odoo-docs/blob/master/model/image/product.png)

model|中文名字|note
-----|-------|----
product.template|产品模版|
product.category|产品类别|
product.product|产品变体|
product.packaging|产品包装|

## 产品属性

![product](https://github.com/odooht/odoo-docs/blob/master/model/image/product.attribute.png)

model|中文名字|note
-----|-------|----
product.attribute|产品属性|
product.attribute.value|产品属性值|
product.template.attribute.line|产品模版属性可配置项|
product.template.attribute.value|产品模版属性值|
product.template.attribute.exclusion|产品属性除外值

## 产品价格

![product](https://github.com/odooht/odoo-docs/blob/master/model/image/product.price.png)


model|中文名字|note
-----|-------|----
product.pricelist|价格表|
product.pricelist.item|价格项目|

## 产品价格

![product](https://github.com/odooht/odoo-docs/blob/master/model/image/product.supplier.png)


model|中文名字|note
-----|-------|----
product.supplierinfo|产品的供应商信息|




初始安装
* product.category 3条记录
* 可销售 费用类 所有

product.template
* 产品模版
* 分为 服务类, 消耗品, 库存类
* 可销售 可租赁 可采购
* 销售单位和采购单位可以不一致
* 有多种包装形式, 通过产品变种计算而得
* 有多个供应商
* 有多个属性
* 属性的排列组合, 构成多个变种
* 价格组成, 有多个项目

product.category
* parent\_id, child\_id 注意没有s
* 父子结构
* 

product.product
* 每个产品变种是 产品模版的一个特例
* 好几个价格 需要再梳理下
* 产品属性值
* 有多种包装形式



TBD 2018-12-22

model|field|String|type|note
-----|-----|------|----|----
product.template||||



model|field|String|type|note
-----|-----|------|----|----
product.category||||


model|field|String|type|note
-----|-----|------|----|----
product.price.history||||


model|field|String|type|note
-----|-----|------|----|----
product.product||||



model|field|String|type|note
-----|-----|------|----|----
product.packaging||||


model|field|String|type|note
-----|-----|------|----|----
product.supplierinfo||||


model|field|String|type|note
-----|-----|------|----|----
product.attribute||||


model|field|String|type|note
-----|-----|------|----|----
product.attribute.value||||


model|field|String|type|note
-----|-----|------|----|----
product.template.attribute.line||||


model|field|String|type|note
-----|-----|------|----|----
product.template.attribute.value||||


model|field|String|type|note
-----|-----|------|----|----
product.template.attribute.exclusion||||


model|field|String|type|note
-----|-----|------|----|----
product.pricelist||||


model|field|String|type|note
-----|-----|------|----|----
res.country.group||||


model|field|String|type|note
-----|-----|------|----|----
product.pricelist.item||||


model|field|String|type|note
-----|-----|------|----|----
res.partner||||


model|field|String|type|note
-----|-----|------|----|----
product.product||||


model|field|String|type|note
-----|-----|------|----|----
product.product||||


model|field|String|type|note
-----|-----|------|----|----
product.product||||


