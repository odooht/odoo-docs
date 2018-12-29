## analytic

![analytic](https://github.com/odooht/odoo-docs/blob/master/model/image/analytic.png)


model|中文名字|note
-----|-------|----
account.analytic.distribution|分配|
account.analytic.tag|标签|
account.analytic.group|分组|
account.analytic.account|核算科目|
account.analytic.line|核算明细|


TBD 2018-12-22

model|field|String|type|note
-----|-----|------|----|----
account.analytic.distribution|account_id|Analytic Account|Many2one|account.analytic.account
account.analytic.distribution|percentage|Percentage|Float|
account.analytic.distribution|name|Name|Char|
account.analytic.distribution|tag_id|Parent tag|Many2one|account.analytic.tag


model|field|String|type|note
-----|-----|------|----|----
account.analytic.tag|name|Analytic Tag|Char|
account.analytic.tag|color||Integer|Color Index
account.analytic.tag|active||Boolean|
account.analytic.tag|active_analytic_distribution||Boolean|Analytic Distribution
account.analytic.tag|analytic_distribution_ids|Analytic Accounts|One2many|account.analytic.distribution
account.analytic.tag|company_id|Company|Many2one|res.company


model|field|String|type|note
-----|-----|------|----|----
account.analytic.group|name||Char|
account.analytic.group|description||Text|Description
account.analytic.group|parent_id|Parent|Many2one|account.analytic.group
account.analytic.group|parent_path||Char|
account.analytic.group|children_ids|Childrens|One2many|account.analytic.group
account.analytic.group|complete_name||Char|Complete Name
account.analytic.group|company_id|Company|Many2one|res.company


model|field|String|type|note
-----|-----|------|----|----
account.analytic.account|name|Analytic Account|Char|
account.analytic.account|code|Reference|Char|
account.analytic.account|active||Boolean|Active
account.analytic.account|group_id|Group|Many2one|account.analytic.group
account.analytic.account|line_ids|Analytic Lines|One2many|'account.analytic.line', 'account_id'
account.analytic.account|company_id|Company|Many2one|res.partner
account.analytic.account|balance|Balance|Monetary|
account.analytic.account|debit|Debit|Monetary|
account.analytic.account|credit|Credit|Monetary|
account.analytic.account|currency_id|Currency|Many2one|


model|field|String|type|note
-----|-----|------|----|----
account.analytic.line|name||Char|Description
account.analytic.line|date||Date|Date
account.analytic.line|amount||Monetary|Amount
account.analytic.line|unit_amount||Float|Quantity
account.analytic.line|product_uom_id|Unit of Measure|Many2one|uom.uom
account.analytic.line|account_id||Many2one|'account.analytic.account',<br/>'Analytic Account'
account.analytic.line|partner_id|Partner|Many2one|res.partner
account.analytic.line|user_id|User|Many2one|res.users
account.analytic.line|tag_ids|Tags|Many2many|'account.analytic.tag', 'account_analytic_line_tag_rel',<br/> 'line_id', 'tag_id'
account.analytic.line|company_id|Company|Many2one|res.company
account.analytic.line|currency_id|Currency|Many2one|
account.analytic.line|group_id||Many2one|account.analytic.group



