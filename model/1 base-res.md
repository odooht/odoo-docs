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

model|field|string|type|note
-----|-----|------|----|----
res.partner.category|name||Char|
res.partner.category|color||Integer|
res.partner.category|parent\_id|Parent Category|Many2one|res.partner.category
res.partner.category|child\_ids|Child Tags|One2many|res.partner.category
res.partner.category|active||Boolean|
res.partner.category|parent\_path||Char|
res.partner.category|partner\_ids||Many2many|res.partner

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
res.bank|state||Many2one|'res.country.state'
res.bank|country||Many2one|'res.country'
res.bank|email||Char|
res.bank|phone||Char|
res.bank|active||Boolean|
res.bank|bic|Bank Identifier Code|Char|


model|field|string|type|note
-----|-----|------|----|----
res.users|partner_id||Many2one|res.partner \_inherits
res.users|login||Char|
res.users|password||Char|
res.users|new\_password||Char|



