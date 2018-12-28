



crm.team
* 销售团队模型
* 类型, sales 和 website
* 有队长, 有成员

## crm.team

![sales.team](https://github.com/odooht/odoo-docs/blob/master/model/image/sales.team.png)

model|中文名字|note
-----|-------|----
crm.team|销售团队|




初始安装
* crm.team 创建两条记录
* xmlid = sales\_team.team\_sales\_department
* xmlid = sales\_team.salesteam\_website\_sales


* res.groups 创建两条记录
* xmlid = sales\_team.group\_sale\_salesman
* xmlid = sales\_team.group\_sale\_manager




TBD 2018-12-22



model|field|String|type|note
-----|-----|------|----|----
res.users|sale_team_id||Many2one|'crm.team', "User's Sales Team"


model|field|String|type|note
-----|-----|------|----|----
res.partner|team_id||Many2one|'crm.team', 'Sales Team'


model|field|String|type|note
-----|-----|------|----|----
crm.team|name||Char|Sales Team
crm.team|active||Boolean|default=True
crm.team|company_id|Company|Many2one|
crm.team|currency_id|Currency|Many2one|res.currency
crm.team|user_id|Team Leader|Many2one|res.users
crm.team|member_ids|Channel Members|One2many|'res.users', 'sale_team_id'
crm.team|favorite_user_ids|Favorite Members|Many2many|
crm.team|is_favorite|Show on dashboard|Boolean|compute
crm.team|reply_to|Reply-To|Char|
crm.team|color|Color Index|Integer|
crm.team|team_type|Team Type|Selection|default='sales'
crm.team|dashboard_button_name|Dashboard Button|Char|
crm.team|dashboard_graph_data||Text|compute
crm.team|dashboard_graph_type|Type|Selection|[('line', 'Line'),<br/>('bar', 'Bar'),]    
crm.team|dashboard_graph_model|Content|Selection|
crm.team|dashboard_graph_group|Group by|Selection| default='day'
crm.team|dashboard_graph_period|Scale|Selection|default='month'





