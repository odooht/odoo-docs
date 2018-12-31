## Account Bank Statement

![account.move](https://github.com/odooht/odoo-docs/blob/master/model/image/account.bank.statement.png)


model|中文名字|note
-----|-------|----
||



TBD 2018-12-22

model|field|String|type|note
-----|-----|------|----|----
account.cashbox.line|coin_value|Coin/Bill Value|Float|required=True, digits=0
account.cashbox.line|number|Number of Coins/Bills|Integer|
account.cashbox.line|subtotal|Subtotal|Float|digits=0, readonly=True
account.cashbox.line|cashbox_id|Cashbox|Many2one|account.bank.statement.cashbox


model|field|String|type|note
-----|-----|------|----|----
'account.bank.statement.cashbox||||

model|field|String|type|note
-----|-----|------|----|----
account.bank.statement.closebalance||||



model|field|String|type|note
-----|-----|------|----|----
account.bank.statement|name|Reference|Char|copy=False, readonly=True
account.bank.statement|reference|External Reference|Char|copy=False, readonly=True
account.bank.statement|date||Date|required=True
account.bank.statement|date_done|Closed On|Datetime|
account.bank.statement|balance_start|Starting Balance|Monetary|
account.bank.statement|balance_end_real||Monetary|Ending Balance
account.bank.statement|accounting_date|Accounting Date|Date|
account.bank.statement|state|Status|Selection|('open', 'New'), ('confirm', 'Validated')
account.bank.statement|currency_id|Currency|Many2one|res.currency
account.bank.statement|journal_id|Journal|Many2one|account.journal
account.bank.statement|journal_type||Selection|
account.bank.statement|company_id|Company|Many2one|res.company
account.bank.statement|total_entry_encoding||Monetary|Transactions Subtotal
account.bank.statement|balance_end||Monetary|Computed Balance
account.bank.statement|difference||Monetary|
account.bank.statement|line_ids|Statement lines|One2many|'account.bank.statement.line', 'statement_id'
account.bank.statement|move_line_ids|Entry lines|One2many|'account.move.line', 'statement_id'
account.bank.statement|move_line_count||Integer|
account.bank.statement|all_lines_reconciled||Boolean|
account.bank.statement|user_id|Responsible|Many2one|res.users
account.bank.statement|cashbox_start_id|Starting Cashbox|Many2one|account.bank.statement.cashbox
account.bank.statement|cashbox_end_id|Ending Cashbox|Many2one|account.bank.statement.cashbox
account.bank.statement|is_difference_zero|Is zero|Boolean|


model|field|String|type|note
-----|-----|------|----|----
account.bank.statement.line|name|Label|Char|required=True
account.bank.statement.line|date||Date|required=True
account.bank.statement.line|amount|Journal's Currency|Monetary|
account.bank.statement.line|journal_currency_id||Many2one|res.currency
account.bank.statement.line|partner_id|Partner|Many2one|res.partner
account.bank.statement.line|account_number|Bank Account Number|Char|
account.bank.statement.line|bank_account_id|Bank Account|Many2one|res.partner.bank
account.bank.statement.line|account_id|Counterpart Account|Many2one|account.account
account.bank.statement.line|statement_id|Statement|Many2one|account.bank.statement
account.bank.statement.line|journal_id|Journal|Many2one|account.journal
account.bank.statement.line|partner_name||Char|
account.bank.statement.line|ref|Reference|Char|
account.bank.statement.line|note|Notes|Text|
account.bank.statement.line|sequence||Integer|index=True
account.bank.statement.line|company_id|Company|Many2one|res.company
account.bank.statement.line|journal_entry_ids||One2many|'account.move.line', 'statement_line_id', 'Journal Items'
account.bank.statement.line|amount_currency||Monetary|
account.bank.statement.line|currency_id||Many2one|
account.bank.statement.line|state|Status|Selection|
account.bank.statement.line|move_name|Journal Entry Name|Char|readonly=True,default=False, copy=False,



