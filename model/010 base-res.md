
## Partner 相关模型

![res.partner](https://github.com/odooht/odoo-docs/blob/master/model/image/res.partner.png)

model|中文名字|note
-----|-------|----
res.partner.category|业务伙伴标签|递归的树状结构, 可以分级定义多级标签
res.partner.title|业务伙伴头衔|
res.partner.industry|业务伙伴行业类型|
res.partner|业务伙伴|地址<br>客户,供应商,员工<br>个人,公司<br>都在该模型中



## Partner 银行账户模型

![res.partner.bank](https://github.com/odooht/odoo-docs/blob/master/model/image/res.partner.bank.png)

model|中文名字|note
-----|-------|----
res.bank|银行|
res.partner.bank|业务伙伴的银行账号|

## Partner 地址模型

![res.partner.geo](https://github.com/odooht/odoo-docs/blob/master/model/image/res.partner.geo.png)

model|中文名字|note
-----|-------|----
res.country.group|国家分组
res.country|国家|
res.country.state|省
res.city|城市|需要安装 base\_address\_city <br> 安装中国会计以后, 可以再安装 中国城市数据 <br>l10n\_cn, l10n\_city
res.currency|货币|
res.currency.rate|汇率|以第一条数据 欧元为基础货币<br>其他数据相对于第一条数据进行汇率折算


## Users 模型

![res.users](https://github.com/odooht/odoo-docs/blob/master/model/image/res.users.png)

model|中文名字|note
-----|-------|----
res.groups|权限组模型|
res.users.log|用户登录日志|
res.users|用户模型|继承自res.partner模型



## Company 模型

![res.company](https://github.com/odooht/odoo-docs/blob/master/model/image/res.company.png)

model|中文名字|note
-----|-------|----
res.company|公司|


## 说明
* res.partner
* type, customer, supplier, employee, is\_company
* 几个布尔字段, 对联系人进行分类
* 联系人或 各种地址. 客户,供应商,员工. 个人还是公司. 
* 若为 个人, 则 parent\_id 为其所属公司
* 若为 公司, 则 child\_ids 为公司下的个人
* 以此可以管理 公司客户和 个人客户, 并管理公司客户对应的联系人
* user\_id 是负责该客户的我公司的销售员
* category_id 注意是多对多字段. 可以给partner 增加 tag
* partner 对应国家,省,城市, 其中城市是字符串
* 可以使用一个扩展模块 base\_address\_city , 定义 city模型
* 被 res.users 模型继承
* user\_ids, 表示该partner的所有登录账号


* 权限组模型
* 根据 ir.module.category, 对权限组进行分类
* 指明对 model 和 rule 的访问权限

* 用户登录日志
* 仅有 create\_uid, create\_date 4个字段
* 用户每次登录会记录一条日志

* 用户模型
* company_ids 指明管理哪些公司

* res.company
* 单公司应用场景下, 指的是自己的公司
* 多公司应用场景下, 则平台服务于多家公司
* 多数模型都有一个字段 comapny\_id, 确定该数据属于哪家公司
* 一些没有 comapny\_id 的模型, 则明确该模型的数据由平台维护, 我们称其为公共模型
* 这些模型: 语言、国家、货币、州、银行、参与人分类、参与人行业类型、参与人头衔, 是公共模型
* 通过 parent\_id 和 child\_ids, 构成父子结构
* 关联 res.partner 模型, 构成一对一关系
* user_ids 指明管理该公司的账户

* 初始安装
* 创建一家公司 同时在 partner模型中有对应记录
* 创建一个用户 admin


model|field|String|type|note
-----|-----|------|----|----
res.partner|name|Name|Char|
res.partner|display\_name||Char|compute
res.partner|date||Date|
res.partner|title||Many2one|res.partner.title
res.partner|parent\_id|Related Company|Many2one|res.partner
res.partner|parent\_name||Char|parent\_id.name
res.partner|child\_ids|Contacts|Many2many|res.partner
res.partner|ref|Internal Reference|Char|
res.partner|lang|Language|Selection|
res.partner|tz|Timezone|Selection|
res.partner|tz\_offset|Timezone|Char|compute
res.partner|user\_id|Salesperson|Many2one|res.users
res.partner|vat|TIN|Char|Tax Identification Number
res.partner|bank\_ids||One2many|res.partner.bank,partner\_id
res.partner|website||Char|
res.partner|comment||text|
res.partner|category\_id|Tags|Many2many|res.partner.category
res.partner|credit\_limit||Float|
res.partner|barcode||Char|
res.partner|active||Boolean|
res.partner|customer||Boolean|
res.partner|supplier||Boolean|
res.partner|employee||Boolean|
res.partner|function|Job Position|Char|
res.partner|type|Address Type|Selection|[('contact', 'Contact'),<br>('invoice', 'Invoice address'),<br>('delivery', 'Shipping address'),<br>('other', 'Other address')]
res.partner|street||Char|
res.partner|street2||Char|
res.partner|zip||Char|
res.partner|city||Char|
res.partner|state\_id||Many2one|res.country.state
res.partner|country\_id||Many2one|res.country.state
res.partner|email||Char|
res.partner|email\_formatted||Char|compute
res.partner|phone||Char|
res.partner|mobile||Char|
res.partner|is\_company||Boolean|
res.partner|industry\_id||Many2one|res.partner.industry
res.partner|company\_id||Many2one|res.company
res.partner|color||Integer|
res.partner|user\_ids||One2many|
res.partner|contact\_address||Char|compute
res.partner|company_name||Char|
res.partner|image||Binary|
res.partner|image\_medium||Binary|
res.partner|image\_small||Binary|

model|field|string|type|relation|note
-----|-----|------|----|--------|----
res.partner.category|name||Char||required=True, <br/>translate=True
res.partner.category|color||Integer||
res.partner.category|parent\_id|Parent Category|Many2one|res.partner.category|index=True, <br>ondelete='cascade'
res.partner.category|child\_ids|Child Tags|One2many|res.partner.category,parent\_id|
res.partner.category|active||Boolean||default=True, <br/>The active field allows you to hide the category without removing it.
res.partner.category|parent\_path||Char||
res.partner.category|partner\_ids||Many2many|res.partner|

model|field|string|type|note
-----|-----|------|----|----
res.partner.title|name|Title|Char|
res.partner.title|shortcut|Abbreviation|Char|

model|field|string|type|note
-----|-----|------|----|----
res.partner.industry|name||Char|
res.partner.industry|full_name||Char|
res.partner.industry|active||Boolean|

model|field|string|type|note
-----|-----|------|----|----
res.bank|name||Char|
res.bank|street||Char|
res.bank|street2||Char|
res.bank|zip||Char|
res.bank|city||Char|
res.bank|state||Many2one|res.country.state
res.bank|country||Many2one|res.country
res.bank|email||Char|
res.bank|phone||Char|
res.bank|active||Boolean|
res.bank|bic|Bank Identifier Code|Char|


model|field|string|type|note
-----|-----|------|----|----
res.partner.bank|acc\_type||Selection|Bank account type: <br>Normal or IBAN. <br>Inferred from the bank account number.
res.partner.bank|acc\_number||Char|Account Number
res.partner.bank|sanitized\_acc\_number||Char|Sanitized Account Number
res.partner.bank|acc\_holder\_name||Char|Account Holder Name
res.partner.bank|partner\_id||Many2one|res.partner
res.partner.bank|bank\_id||Many2one|res.bank
res.partner.bank|bank\_name||Char|bank\_id.name
res.partner.bank|bank\_bic||Char|bank\_id.bic
res.partner.bank|sequence||Integer|
res.partner.bank|currency\_id||Many2one|res.currency
res.partner.bank|company\_id||Many2one|res.company
res.partner.bank|qr\_code\_valid||Boolean|


model|field|string|type|note
-----|-----|------|----|----
res.country|name||Char|
res.country|code|Country Code|Char|
res.country|currency\_id||Many2one|
res.country|image||Binary|
res.country|phone\_code||Integer|Country Calling Code
res.country|country\_group\_ids||Many2many|res.country.group
res.country|state\_ids||One2many|res.country.state, country_id

model|field|string|type|note
-----|-----|------|----|----
res.country.group|name||Char|
res.country.group|country\_ids||Many2many|res.country

model|field|string|type|note
-----|-----|------|----|----
res.country.state|country\_id||Many2one|res.country
res.country.state|name||Char|
res.country|code|State Code|Char|


model|field|string|type|note
-----|-----|------|----|----
res.currency|name||Char|
res.currency|symbol||Char|
res.currency|rate||Float|
res.currency|rate_ids||One2many|res.currency.rate
res.currency|rounding||Float|
res.currency|active||Boolean|
res.currency|date||Date|

model|field|string|type|note
-----|-----|------|----|----
res.currency.rate|name||Date|
res.currency.rate|rate||Float|The rate of the currency to the currency of rate 1
res.currency.rate|currency\_id||Many2one|res.currency
res.currency.rate|company\_id||Many2one|res.company



model|field|string|type|note
-----|-----|------|----|----
res.users|partner\_id||Many2one|res.partner \_inherits
res.users|login||Char|
res.users|password||Char|
res.users|new\_password||Char|
res.users|active||Boolean|
res.users|groups\_id||Many2many|res.groups
res.users|log\_ids||One2many|res.users.log, create\_uid
res.users|login\_date||Datetime|log\_ids.create\_date
res.users|share||Boolean|compute
res.users|companies\_count||Integer|compute
res.users|tz\_offset||Char|compute
res.users|company\_id||Many2one|res.company
res.users|company\_ids||Many2many|res.company
res.users|name||Char|partner\_id.name
res.users|email||Char|partner\_id.name


model|function|args|return|note
-----|--------|------|----|----
res.users|change\_password|old\_passwd, new\_passwd|boolean|


model|field|string|type|note
-----|-----|------|----|----
res.users.log|create_uid||Many2one|res.users


model|field|string|type|note
-----|-----|------|----|----
res.groups|name||Char|
res.groups|users||Many2many|res.users
res.groups|model\_access||One2many|ir.model.access, group\_id
res.groups|rule\_groups||Many2many|ir.rule
res.groups|comment||Text|
res.groups|category\_id||Many2one|ir.module.category
res.groups|color||Integer|
res.groups|full\_name||Char|compute
res.groups|share||Boolean|


model|field|string|type|note
-----|-----|------|----|----
res.company|name||Char|
res.company|sequence||Integer|
res.company|parent\_id||Many2one|res.company
res.company|child\_ids||One2many|res.company
res.company|partner\_id||Many2one|res.partner
res.company|logo||Binary|partner\_id.image
res.company|logo\_web||Binary|compute
res.company|currency\_id||Many2one|res.currency
res.company|user\_ids|Accepted Users|Many2many|res.users
res.company|account\_no|Account No.|Char|
res.company|street||Char|
res.company|street2||Char|
res.company|zip||Char|
res.company|city||Char|
res.company|state\_id||Many2one|res.country.state
res.company|bank\_ids|Bank Accounts|One2many|res.partner.bank
res.company|country\_id||Many2one|res.country
res.company|email||Char|
res.company|phone||Char|
res.company|website||Char|
res.company|vat||Char|
res.company|company_registry||Char|



需要安装 base\_address\_city

model|field|string|type|note
-----|-----|------|----|----
res.country|enforce_cities||Boolean|


model|field|string|type|note
-----|-----|------|----|----
res.city|name||Char|
res.city|zipcode||Char|
res.city|country\_id||Many2one|res.country
res.city|state\_id||Many2one|res.country.state

model|field|String|type|note
-----|-----|------|----|----
res.partner|country\_enforce\_cities||Boolean|country\_id.enforce\_cities
res.partner|city\_id||Many2one|res.city


