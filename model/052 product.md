## Product

![product](https://github.com/odooht/odoo-docs/blob/master/model/image/product.png)

model|中文名字|note
-----|-------|----
product.template|产品模版|
product.category|产品类别|
product.product|产品变体|
product.packaging|产品包装|

## 产品属性

![product.attribute](https://github.com/odooht/odoo-docs/blob/master/model/image/product.attribute.png)

model|中文名字|note
-----|-------|----
product.attribute|产品属性|
product.attribute.value|产品属性值|
product.template.attribute.line|产品模版属性可配置项|
product.template.attribute.value|产品模版属性值|
product.template.attribute.exclusion|产品属性除外值


## 产品价格

![product.price](https://github.com/odooht/odoo-docs/blob/master/model/image/product.price.png)


model|中文名字|note
-----|-------|----
product.pricelist|价格表|
product.pricelist.item|价格项目|

## 产品供应商

![product.supplier](https://github.com/odooht/odoo-docs/blob/master/model/image/product.supplier.png)


model|中文名字|note
-----|-------|----
product.supplierinfo|产品的供应商信息|


## 说明
* 产品模版 定义各种属性, 成为产品变体
* 直接销售的是产品变体
* 因此在销售/采购/库存管理中说的产品, 都是指产品变体
* 产品属性通常是颜色/规格, 这些不影响包装的属性
* 因此, 产品的包装形式定义在产品模版上
* 产品模版的多种属性的笛卡尔乘积形成多个产品变种
* 无意义的笛卡尔乘积项, 由product.template.attribute.exclusion 过滤掉
* 产品的价格很啰嗦
* 有列表价格和成本价
* 各属性有自己的额外价格
* 产品模版的价格 + 属性价格 = 产品变种的价格
* 产品变种可以直接设定价格
* 产品有多个供应商
* 针对特定客户可以设定特定的价格表
* 初始安装, product.category 3条记录. 可销售 费用类 所有




TBD 2018-12-22

model|field|String|type|note
-----|-----|------|----|----
product.template|name||Char|Name
product.template|sequence||Integer|Sequence
product.template|description||Text|Description
product.template|description_purchase||Text|Purchase Description
product.template|type|Product Type|Selection|[('consu', 'Consumable'),<br/>('service', 'Service')]        
product.template|rental||Boolean|Can be Rent
product.template|categ_id||Many2one|'product.category',<br/>'Product Category'
product.template|currency_id||Many2one|'res.currency','Currency'
product.template|price||Float|Price
product.template|list_price||Float|Sales Price
product.template|lst_price||Float|Public Price
product.template|standard_price||Float|Cost
product.template|volume||Float|Volume
product.template|weight||Float|Weight
product.template|weight_uom_id|Weight Unit of Measure|Many2one|uom.uom
product.template|weight_uom_name|Weight unit of measure label|Char|readonly=True
product.template|sale_ok||Boolean|Can be Sold
product.template|purchase_ok||Boolean|Can be Purchased
product.template|pricelist_id||Many2one|'product.pricelist','Pricelist'
product.template|uom_id||Many2one|'uom.uom', 'Unit of Measure'
product.template|uom_name|Unit of Measure Name|Char|readonly=True
product.template|uom_po_id||Many2one|required=True
product.template|company_id||Many2one|'res.company','Company'
product.template|packaging_ids|Product Packages|One2many|product.packaging
product.template|seller_ids||One2many|
product.template|variant_seller_ids||One2many|
product.template|active||Boolean|Active
product.template|color||Integer|Color Index
product.template|is_product_variant|Is a product variant|Boolean|compute
product.template|attribute_line_ids||One2many|
product.template|product_variant_ids||One2many|required=True
product.template|product_variant_count||Integer|# Product Variants
product.template|barcode||Char|Barcode
product.template|default_code||Char|Internal Reference
product.template|item_ids||One2many|
product.template|image||Binary|Image
product.template|image_medium||Binary|Medium-sized image
product.template|image_small||Binary|Small-sized image


model|field|String|type|note
-----|-----|------|----|----
product.category|name||Char|Name
product.category|complete_name||Char|Complete Name
product.category|parent_id||Many2one|'product.category','Parent Category'
product.category|parent_path||Char|
product.category|child_id||One2many|
product.category|product_count||Integer|# Products


model|field|String|type|note
-----|-----|------|----|----
product.price.history|company_id|Company|Many2one|res.company
product.price.history|product_id||Many2one|'product.product', 'Product'
product.price.history|datetime||Datetime|Date
product.price.history|cost||Float|Cost


model|field|String|type|note
-----|-----|------|----|----
product.product|price||Float|Price
product.product|price_extra||Float|Variant Price Extra
product.product|lst_price||Float|Sale Price
product.product|default_code||Char|Internal Reference
product.product|code||Char|Reference
product.product|partner_ref||Char|Customer Ref
product.product|active||Boolean|Active
product.product|product_tmpl_id||Many2one|'product.template',<br/>'Product Template'
product.product|image_variant||Binary|Variant Image
product.product|image||Binary|Big-sized image
product.product|image_small||Binary|Small-sized image
product.product|image_medium||Binary|Medium-sized image
product.product|is_product_variant||Boolean|compute
product.product|standard_price||Float|Cost
product.product|volume||Float|Volume
product.product|weight||Float|Weight
product.product|pricelist_item_ids||Many2many|'product.pricelist.item',<br/>'Pricelist Items'
product.product|packaging_ids||One2many|'product.packaging',<br/>'product_id','Product Packages'


model|field|String|type|note
-----|-----|------|----|----
product.packaging|name||Char|Package Type
product.packaging|sequence||Integer|Sequence
product.packaging|product_id|Product|Many2one|product.product
product.packaging|qty||Float|Contained Quantity
product.packaging|barcode||Char|Barcode
product.packaging|product_uom_id||Many2one|uom.uom


model|field|String|type|note
-----|-----|------|----|----
product.supplierinfo|name||Many2one|'res.partner','Vendor'
product.supplierinfo|product_name||Char|Vendor Product Name
product.supplierinfo|product_code||Char|Vendor Product Code
product.supplierinfo|sequence||Integer|Sequence
product.supplierinfo|product_uom||Many2one|'uom.uom','Unit of Measure'
product.supplierinfo|min_qty||Float|Minimal Quantity
product.supplierinfo|price||Float|Price
product.supplierinfo|company_id||Many2one|'res.company','Company'
product.supplierinfo|currency_id||Many2one|'res.currency','Currency'
product.supplierinfo|date_start||Date|Start Date
product.supplierinfo|date_end||Date|End Date
product.supplierinfo|product_id||Many2one|'product.product',<br/>'Product Variant'
product.supplierinfo|product_tmpl_id||Many2one|'product.template',<br/>'Product Template'
product.supplierinfo|product_variant_count||Integer|Variant Count
product.supplierinfo|delay||Integer|Delivery Lead Time


model|field|String|type|note
-----|-----|------|----|----
product.attribute|name||Char|Attribute
product.attribute|value_ids||One2many|'product.attribute.value',<br/> 'attribute_id', 'Values'
product.attribute|sequence||Integer|Sequence
product.attribute|attribute_line_ids||One2many|'product.template.attribute.line',<br/> 'attribute_id', 'Lines'
product.attribute|create_variant|Create Variants|Selection|[('no_variant', 'Never'),<br/>('always', 'Always'),<br/>('dynamic', 'Only when the product is added to a sales order')]
        
 
model|field|String|type|note
-----|-----|------|----|----
product.attribute.value|name|Value|Char|
product.attribute.value|sequence|Sequence|Integer|
product.attribute.value|attribute_id|Attribute|Many2one|product.attribute


model|field|String|type|note
-----|-----|------|----|----
product.template.attribute.line|product_tmpl_id|Product Template|Many2one|product.template
product.template.attribute.line|attribute_id|Attribute|Many2one|product.attribute
product.template.attribute.line|value_ids|Attribute Values|Many2many|product.attribute.value
product.template.attribute.line|product_template_value_ids|Product Attribute Values|Many2many|product.template.attribute.value


model|field|String|type|note
-----|-----|------|----|----
product.template.attribute.value|name||Char|Value
product.template.attribute.value|product_attribute_value_id|Attribute Value|Many2one|product.attribute.value
product.template.attribute.value|product_tmpl_id|Product Template|Many2one|product.template
product.template.attribute.value|attribute_id|Attribute|Many2one|product.attribute
product.template.attribute.value|sequence||Integer|Sequence
product.template.attribute.value|price_extra|Attribute Price Extra|Float|
product.template.attribute.value|exclude_for|Exclude for|One2many|


model|field|String|type|note
-----|-----|------|----|----
product.template.attribute.exclusion|product_template_attribute_value_id|Attribute Value|Many2one|product.template.attribute.value
product.template.attribute.exclusion|product_tmpl_id|Product Template|Many2one|product.template
product.template.attribute.exclusion|value_ids|Attribute Values|Many2many|product.template.attribute.value


model|field|String|type|note
-----|-----|------|----|----
product.pricelist|name||Char|Pricelist Name
product.pricelist|active||Boolean|Active
product.pricelist|item_ids||One2many|'product.pricelist.item', 'pricelist_id',<br/>'Pricelist Items'
product.pricelist|currency_id||Many2one|'res.currency', 'Currency'
product.pricelist|company_id||Many2one|'res.company', 'Company'
product.pricelist|sequence||Integer|
product.pricelist|country_group_ids|Country Groups|Many2many|'res.country.group',<br/> 'res_country_group_pricelist_rel',<br/>'pricelist_id', <br/>'res_country_group_id',                                       


model|field|String|type|note
-----|-----|------|----|----
res.country.group|pricelist_ids|Pricelists|Many2many|'product.pricelist',<br/> 'res_country_group_pricelist_rel', <br/>'res_country_group_id',<br/> 'pricelist_id'                               


model|field|String|type|note
-----|-----|------|----|----
product.pricelist.item|product_tmpl_id||Many2one|'product.template',<br/> 'Product Template'
product.pricelist.item|product_id||Many2one|'product.product', 'Product'
product.pricelist.item|categ_id||Many2one|'product.category', <br/>'Product Category'
product.pricelist.item|min_quantity||Integer|Min. Quantity
product.pricelist.item|applied_on||Selection|[('3_global', 'Global'),<br/>('2_product_category', ' Product Category'),<br/>('1_product', 'Product'),<br/>('0_product_variant', 'Product Variant')]     
product.pricelist.item|base||Selection|[('list_price', 'Public Price'),<br/>('standard_price', 'Cost'),<br/>('pricelist', 'Other Pricelist')]
product.pricelist.item|base_pricelist_id||Many2one|'product.pricelist', <br/>'Other Pricelist'
product.pricelist.item|pricelist_id||Many2one|'product.pricelist', 'Pricelist'
product.pricelist.item|price_surcharge||Float|'Price Surcharge'
product.pricelist.item|price_discount||Float|Price Discount
product.pricelist.item|price_round||Float|Price Rounding
product.pricelist.item|price_min_margin||Float|Min. Price Margin
product.pricelist.item|price_max_margin||Float|Max. Price Margin
product.pricelist.item|company_id||Many2one|'res.company', 'Company'
product.pricelist.item|currency_id||Many2one|'res.currency', 'Currency'
product.pricelist.item|date_start||Date|Start Date
product.pricelist.item|date_end||Date|End Date
product.pricelist.item|compute_price||Selection|[('fixed', 'Fix Price'),<br/>('percentage', 'Percentage (discount)'),<br/>('formula', 'Formula')]            
product.pricelist.item|fixed_price||Float|Fixed Price
product.pricelist.item|percent_price||Float|Percentage Price
product.pricelist.item|name||Char|Name
product.pricelist.item|price||Char|Price


model|field|String|type|note
-----|-----|------|----|----
res.partner|property_product_pricelist||Many2one|'product.pricelist', 'Pricelist'



