

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


