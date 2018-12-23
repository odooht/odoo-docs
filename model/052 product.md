
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

product.packaging
* 对产品对包装

product.supplierinfo
* 产品的供应商信息

product.pricelist
* 有多个价格项目

product.pricelist.item
* 针对 产品类别, 产品模版, 产品变种设置价格表


res.partner
* 可以对特定客户设置价格表


product.attribute
product.attribute.value
* 多个属性
* 每个属性有不同的值


product.template.attribute.line
* 产品模版 与属性 及属性值的 对应关系
* 该产品模版有哪些属性, 哪些取值范围

product.template.attribute.value
product.template.attribute.exclusion



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


