## Account

![account](https://github.com/odooht/odoo-docs/blob/master/model/image/account.png)


model|中文名字|note
-----|-------|----
account.account.type|科目类型|
account.account.tag|科目标签|
account.account|科目|
account.group|科目分组|
account.journal|账本|
account.tax.group|税分组|
account.tax|税|


model|field|String|type|note
-----|-----|------|----|----
account.account.type|name|Account Type|Char|
account.account.type|include_initial_balance|Bring Accounts Balance Forward|Boolean|
account.account.type|type||Selection|
account.account.type|internal_group|Internal Group|Selection|


model|field|String|type|note
-----|-----|------|----|----
account.account.tag|name||Char|
account.account.tag|applicability||Selection|
account.account.tag|color||Integer|
account.account.tag|active||Boolean|


model|field|String|type|note
-----|-----|------|----|----
account.account|name||Char|required=True, index=True
account.account|currency_id|Account Currency|Many2one|res.currency
account.account|code||Char|required=True, index=True
account.account|deprecated||Boolean|index=True, default=False
account.account|user_type_id|Type|Many2one|account.account.type
account.account|internal_type||Selection|store=True, readonly=True
account.account|internal_group|Internal Group|Selection|store=True, readonly=True
account.account|last_time_entries_checked|Latest Invoices & Payments Matching Date|Datetime|readonly=True, copy=False
account.account|reconcile|Allow Reconciliation|Boolean|
account.account|tax_ids|Default Taxes|Many2many|
account.account|note||Text|
account.account|company_id|Company|Many2one|res.company
account.account|tag_ids|Tags|Many2many|'account.account.tag', 'account_account_account_tag'
account.account|group_id||Many2one|'account.group'
account.account|opening_debit|Opening debit|Monetary|
account.account|opening_credit|Opening credit|Monetary|


model|field|String|type|note
-----|-----|------|----|----
account.group|parent_id||Many2one|account.group
account.group|parent_path||Char|index=True
account.group|name||Char|required=True
account.group|code_prefix||Char|


model|field|String|type|note
-----|-----|------|----|----
account.journal|name|Journal Name|Char|required=True
account.journal|code|Short Code|Char|required=True
account.journal|active||Boolean|default=True
account.journal|type||Selection|required=True
account.journal|type_control_ids||Many2many|
account.journal|account_control_ids|Account Types Allowed|Many2many|'account.account', 'account_account_type_rel', 'journal_id', 'account_id'
account.journal|default_credit_account_id|Accounts Allowed|Many2one|'account.account', 'account_account_type_rel', 'journal_id', 'account_id'
account.journal|default_debit_account_id|Default Credit Account|Many2one|account.account
account.journal|update_posted|Allow Cancelling Entries|Boolean|account.account
account.journal|group_invoice_lines|Group Invoice Lines|Boolean|
account.journal|sequence_id|Entry Sequence|Many2one|
account.journal|refund_sequence_id|Credit Note Entry Sequence|Many2one|ir.sequence
account.journal|sequence||Integer|
account.journal|sequence_number_next|Next Number|Integer|
account.journal|refund_sequence_number_next|Credit Notes: Next Number|Integer|
account.journal|currency_id|Currency|Many2one|res.currency
account.journal|company_id|Company|Many2one|res.company
account.journal|refund_sequence|Dedicated Credit Note Sequence|Boolean|default=False
account.journal|inbound_payment_method_ids|For Incoming Payments|Many2many|
account.journal|outbound_payment_method_ids|For Outgoing Payments|Many2many|
account.journal|at_least_one_inbound||Boolean|
account.journal|at_least_one_outbound||Boolean|
account.journal|profit_account_id|Profit Account|Many2one|account.account
account.journal|loss_account_id|Loss Account|Many2one|account.account
account.journal|belongs_to_company||Boolean|Belong to the user\'s current company
account.journal|company_partner_id||Many2one|res.partner
account.journal|bank_account_id|Account Holder|Many2one|res.partner.bank
account.journal|bank_statements_source|Bank Feeds|Selection|
account.journal|bank_acc_number||Char|readonly=False
account.journal|bank_id||Many2one|res.bank
account.journal|post_at_bank_rec|Post At Bank Reconciliation|Boolean|
account.journal|alias_id|Alias|Many2one|mail.alias
account.journal|alias_domain||Char|Alias domain
account.journal|alias_name||Char|Alias Name for Vendor Bills


model|field|String|type|note
-----|-----|------|----|----
res.partner.bank|journal_id|Account Journal|One2many|'account.journal', 'bank_account_id'


model|field|String|type|note
-----|-----|------|----|----
account.tax.group|name||Char|required=True, translate=True
account.tax.group|sequence||Integer|


model|field|String|type|note
-----|-----|------|----|----
account.tax|name|Tax Name|Char|required=True
account.tax|type_tax_use|Tax Scope|Selection|required=True, default="sale"
account.tax|amount_type|Tax Computation|Selection| required=True, oldname='type'
account.tax|active|Company|Boolean|res.company
account.tax|company_id|Company|Many2one|res.company
account.tax|children_tax_ids|Children Taxes|Many2many|'account.tax', 'account_tax_filiation_rel', 'parent_tax', 'child_tax'
account.tax|sequence||Integer|required=True
account.tax|amount||Float|required=True
account.tax|account_id|Tax Account|Many2one|account.account
account.tax|refund_account_id|Tax Account on Credit Notes|Many2one|account.account
account.tax|description|Label on Invoices|Char|
account.tax|price_include|Included in Price|Boolean|default=False
account.tax|include_base_amount|Affect Base of Subsequent Taxes|Boolean|default=False
account.tax|analytic|Include in Analytic Cost|Boolean|
account.tax|tag_ids|Tags|Many2many|'account.account.tag', 'account_tax_account_tag'
account.tax|tax_group_id|Tax Group|Many2one|account.tax.group
account.tax|hide_tax_exigibility|'Hide Use Cash Basis Option|Boolean| readonly=True
account.tax|tax_exigibility|Tax Due|Selection|default='on_invoice'
account.tax|cash_basis_account_id|Tax Received Account|Many2one|account.account
account.tax|cash_basis_base_account_id|Base Tax Received Account|Many2one|account.account
account.tax|_sql_constraints|||
