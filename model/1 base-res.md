

model|field|中文名|type|comodel|note
-----|-----|-----|----|-------|----
res.users|login|登录名|Char||
res.users|password|密码|Char||
res.users|partner_id|参与人|Many2one|res.partner 继承自参与人|

model|field|name|中|type|comodel|note
-----|-----|----|-----|----|-------|----
res.partner|name|Name|名称|Char||
res.partner|display\_name||名称|Char|compute|
res.partner|date|||Date||
res.partner|title|||Many2one|res.partner.title|
res.partner|parent\_id|Related Company||Many2one|res.partner|
res.partner|parent\_name|||Char|parent\_id.name|
res.partner|child\_ids|Contacts||Many2many|res.partner|
res.partner|ref|Internal Reference||Char||
res.partner|lang|Language||Selection||
res.partner|tz|Timezone||Selection||
res.partner|tz\_offset|Timezone||Char|compute|
res.partner|user\_id|Salesperson||res.users||
res.partner|vat|TIN||Char|Tax Identification Number|
res.partner|bank\_ids|||One2many|res.partner.bank,partner\_id|
res.partner|website|||Char||
res.partner|comment|||text||
res.partner|category\_id|Tags||Many2many|res.partner.category|
res.partner|credit\_limit|||Float||
res.partner|barcode|||Char||
res.partner|active|||Boolean||
res.partner|customer|||Boolean||
res.partner|supplier|||Boolean||
res.partner|employee|||Boolean||
res.partner|function|Job Position||Char||
res.partner|type|Address Type||Selection|[('contact', 'Contact'),('invoice', 'Invoice address'),('delivery', 'Shipping address'),('other', 'Other address')]|
res.partner|street|||Char||
res.partner|street2|||Char||
res.partner|zip|||Char||
res.partner|city|||Char||
res.partner|state\_id|||Many2one|res.country.state|
res.partner|country\_id|||Many2one|res.country.state|
res.partner|email|||Char||
res.partner|email\_formatted|||Char|compute|
res.partner|phone|||Char||
res.partner|mobile|||Char||
res.partner|is\_company|||Boolean||
res.partner|industry\_id|||Many2one|res.partner.industry|
res.partner|company\_id|||Many2one|res.company|
res.partner|color|||Integer||
res.partner|user\_ids|||One2many||
res.partner|contact\_address|||Char|compute|
res.partner|company_name|||Char||
res.partner|image|||Binary||
res.partner|image\_medium|||Binary||
res.partner|image\_small|||Binary||



