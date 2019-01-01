包含文件:  
account_payment.py  



## Account Payment

![account.payment](https://github.com/odooht/odoo-docs/blob/master/model/image/account.payment.png)


model|中文名字|note
-----|-------|----
account.payment.method|支付方式|
account.payment|收付款单|
account.abstract.payment|收付款单.基础模型|
account.register.payments|收付款单.导航模型|


## 说明
* 包括收款单和付款单
* 与销售发票对应的是收款单
* 与采购账单对应的是付款单
* 收付款单自动生成会计凭证
* 收付款科目对应现金或银行存款,决定于账簿account.journal


TBD 2018-12-22

model|field|String|type|note
-----|-----|------|----|----
account.payment.method|name||Char|required=True, translate=True
account.payment.method|code||Char|required=True
account.payment.method|payment_type||Selection|('inbound', 'Inbound'), ('outbound', 'Outbound')


model|field|String|type|note
-----|-----|------|----|----
account.abstract.payment|invoice_ids|Invoices|Many2many|account.invoice
account.abstract.payment|multi|Multi|Boolean|
account.abstract.payment|payment_type|Payment Type|Selection|('outbound', 'Send Money'), ('inbound', 'Receive Money')
account.abstract.payment|payment_method_id|Payment Method Type|Many2one|account.payment.method
account.abstract.payment|payment_method_code||Char|
account.abstract.payment|partner_type||Selection|('customer', 'Customer'), ('supplier', 'Vendor')
account.abstract.payment|partner_id|Partner|Many2one|res.partner
account.abstract.payment|amount|'Payment Amount|Monetary|required=True
account.abstract.payment|currency_id|Payment Date|Many2one|required=True, copy=False
account.abstract.payment|payment_date|Payment Date|Date|
account.abstract.payment|communication|Memo|Char|
account.abstract.payment|journal_id|||
account.abstract.payment|hide_payment_method|Payment Journal|Many2one|account.journa
account.abstract.payment|payment_difference||Boolean|
account.abstract.payment|payment_difference_handling||Monetary|readonly=True
account.abstract.payment|writeoff_account_id|Difference Account|Many2one|account.account
account.abstract.payment|writeoff_label|Journal Item Label|Char|default='Write-Off'
account.abstract.payment|partner_bank_account_id|Recipient Bank Account|Many2one|res.partner.bank
account.abstract.payment|show_partner_bank_account||Boolean|


model|field|String|type|note
-----|-----|------|----|----
account.register.payments|group_invoices|Group Invoices|Boolean|
account.register.payments|show_communication_field||Boolean|


model|field|String|type|note
-----|-----|------|----|----
account.payment|company_id|Company|Many2one|res.company
account.payment|name||Char|readonly=True, copy=False
account.payment|state|Status|Selection|('draft', 'Draft'), ('posted', 'Posted'), ('sent', 'Sent'), ('reconciled', 'Reconciled'), ('cancelled', 'Cancelled')
account.payment|payment_type||Selection|
account.payment|payment_reference||Char|
account.payment|move_name|Journal Entry Name|Char|readonly=True,default=False, copy=False,
account.payment|destination_account_id||Many2one|account.account
account.payment|destination_journal_id|Transfer To|Many2one|account.journal
account.payment|invoice_ids|Invoices|Many2many|copy=False, readonly=True
account.payment|reconciled_invoice_ids|Reconciled Invoices|Many2many|Many2manye
account.payment|has_invoices||Boolean|readonly=True

