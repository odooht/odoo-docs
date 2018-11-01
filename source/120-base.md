/addons/base/base.sql

base.sql,  推测 该文件 被废弃了。

```
insert into res_currency (id, name, symbol) VALUES (1, 'EUR', '€');
insert into res_company (id, name, partner_id, currency_id) VALUES (1, 'My Company', 1, 1);
insert into res_partner (id, name, company_id) VALUES (1, 'My Company', 1);
insert into res_users (id, login, password, active, partner_id, company_id) VALUES (1, 'admin', 'admin', true, 1, 1);
insert into res_groups (id, name) VALUES (1, 'Employee');
```

货币 / 公司 / Partner / User / Group ， 各一条数据。id=1
SupperUser 对应的partner，partner_id = ? 目前是疑问。

Data：
/addons/base/base_data.xml

```
main_partner,res.partner, My Company
main_company, res.company, My Company, partner_id=main_partner
partner_root,res.partner, Administrator,company_id=main_company
user_root,res.users,partner_id=base.partner_root,company_id=main_company
default_user, res.users
main_partner,res.partner, company_id=main_company
public_partner,res.partner, 
public_user,res.users
```

+ 创建 公司main_company，同时增加一个参与人main_partner
+ 创建 用户user_root，同时增加一个参与人partner_root。该用户管理上述公司。
+ 创建 用户 default_user。新增用户时，从这儿复制权限==需要确认该功能。
+ 创建 用户 public_user。未激活。如果激活了 是什么？


/addons/base/res/res_partner_data.xml
+ res.partner.title，5条记录
+ res.partner.industry，若干个 行业

res.company 公司
- 几乎所有的其他模型都有一个字段叫做 company_id 。没有 company_id的 是否应该特别说明一下？
- 以后不特别说明，则该模型是 公司专属的。而不属于任何公司的模型 称为公共模型。

- 早期设计odoo8时， res.comapny 继承自 res.partner。现在odoo10以后，取消了继承关系。
- 但是一些属性依然放在 res.partner 里

- 公司自己构成上下级层级关系。parent_id / child_ids
- res.users与res.company是 多对多关系。公司有多个用户，允许这些用户访问我公司的数据。
- 公司有唯一的货币。货币是公共模型。

model|field|type|ref|string|note
-----|-----|----|---|------|----
res.company|parent_id|Many2one|res.company|Parent Company|母公司
res.company|child_ids|One2many|res.company, parent_id|Child Companies|子公司
res.company|partner_id|Many2one|res.partner|Partner|参与人, 引入一些计算列
res.company|currency_id|Many2one|res.currency|Currency|货币
res.company|user_ids|Many2many|res.users|Accepted Users|允许的用户
res.company|bank_ids|One2many|res.partner.bank, company_id|Bank Accounts|银行账户
res.company|name|Char|related, partner_id.name|Company Name|名称唯一



res.users 用户模型
继承自 res.partner，
密码字段是加密的不可读。
通过res.group 模型，给用户分配权限。
用户当前仅供职于一家公司，但是可以访问多家公司的数据。
用户每次登陆，记录日志。


res.partner 参与人模型
这是个大杂烩，客户、供应商、客户供应商的联系人、地址都是它。公司、员工、用户 等 基于它。
res.partner.category（公共模型） ， 参与人分类。
res.partner.title（公共模型）， 当 参与人是自然人时，其头衔。
res.users，user_id 当参与人是客户时，其销售经理。
res.users，user_ids ，参与人对应的所有 登陆账号。
res.partner.bank，参与人的银行账号。
res.partner.industry（公共模型），参与人是公司时，行业类型。
res.country，res.country.state，参与人对应的 国家和 州/省



res.country，res.country.state，res.country.group, res.currency 是公共模型。
res.country.state 属于某个国家。
国家按照不同的分类方法 构成不同的组
国家有货币。货币 有汇率。汇率指的是 对应于 欧元的汇率。欧元是1号货币。


res.bank 是公共模型。
参与人 以 某币种 在某银行 开设银行账户。
参与人是  公司专属模型，故  银行账户也是 公司专属模型。


综上，在 资源中，语言、国家、货币、州、银行、参与人分类、参与人行业类型、参与人头衔、
这些是 公共模型。
公共模型，应该有  supperuser 操作？
