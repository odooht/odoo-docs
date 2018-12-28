TBD 2018-12-22

model|field|String|type|note
-----|-----|------|----|----
account.move|name|Number|Char|required=True, copy=False, default='/'
account.move|ref|Reference|Char| copy=False
account.move|date||Date|required=True
account.move|journal_id|Journal|Many2one|account.journal
account.move|currency_id|Currency|Many2one|res.currency
account.move|state|Status|Selection|[('draft', 'Unposted'), ('posted', 'Posted')]
account.move|line_ids|Journal Items|One2many|'account.move.line', 'move_id'
account.move|partner_id|Partner|Many2one|res.partner
account.move|amount||Monetary|store=True
account.move|narration|Internal Note|Text|
account.move|company_id|Company|Many2one|res.company
account.move|matched_percentage||Float|Percentage Matched
account.move|dummy_account_id|Account|Many2one|account.account
account.move|tax_cash_basis_rec_id|Tax Cash Basis Entry of|Many2one|account.partial.reconcile
account.move|auto_reverse|Reverse Automatically|Boolean|
account.move|reverse_date|Reversal Date|Date|
account.move|reverse_entry_id|Reverse entry|Many2one|account.move
account.move|tax_type_domain||Char|store=False


model|field|String|type|note
-----|-----|------|----|----
account.move.line|name|Label|Char|
account.move.line|quantity||Float|
account.move.line|product_uom_id|Unit of Measure|Many2one|uom.uom
account.move.line|product_id|Product|Many2one|product.product
account.move.line|debit||Monetary|
account.move.line|credit||Monetary|
account.move.line|balance||Monetary|
account.move.line|debit_cash_basis||Monetary|
account.move.line|credit_cash_basis||Monetary|
account.move.line|balance_cash_basis||Monetary|
account.move.line|amount_currency||Monetary|
account.move.line|company_currency_id|Company Currency|Many2one|res.currency
account.move.line|currency_id|Currency|Many2one|res.currency
account.move.line|amount_residual|Residual Amount|Monetary| store=True
account.move.line|amount_residual_currency|Residual Amount in Currency|Monetary| store=True
account.move.line|tax_base_amount|Base Amount|Monetary|store=True
account.move.line|account_id|Account|Many2one|account.account
account.move.line|move_id|Journal Entry|Many2one|account.move
account.move.line|narration|Narration|Text|readonly=False
account.move.line|ref|Reference|Char|store=True, copy=False, index=True, readonly=False
account.move.line|payment_id|Originator Payment|Many2one|account.payment
account.move.line|statement_line_id|Bank statement line reconciled with this entry|Many2one|account.bank.statement
account.move.line|statement_id|Statement|Many2one|account.bank.statement
account.move.line|reconciled||Boolean|
account.move.line|full_reconcile_id|Matching Number|Many2one|account.full.reconcile
account.move.line|matched_debit_ids|Matched Debits|One2many|'account.partial.reconcile', 'credit_move_id'
account.move.line|matched_credit_ids|Matched Credits|One2many|'account.partial.reconcile', 'debit_move_id'
account.move.line|journal_id|Journal|Many2one|account.journal
account.move.line|blocked|No Follow-up|Boolean| default=False
account.move.line|date_maturity|Due date|Date|index=True, required=True,
account.move.line|date|Date|Date|index=True, store=True, copy=False, readonly=False
account.move.line|analytic_line_ids|Analytic lines|One2many|'account.analytic.line', 'move_id'
account.move.line|tax_ids|Taxes|Many2many|account.tax
account.move.line|tax_line_id|Originator tax|Many2one|account.tax
account.move.line|analytic_account_id|Analytic Account|Many2one|account.analytic.account
account.move.line|analytic_tag_ids|Analytic Tags|Many2many|account.analytic.tag
account.move.line|company_id|Company|Many2one|res.company
account.move.line|counterpart||Char|Counterpart
account.move.line|invoice_id||Many2one|account.invoice
account.move.line|partner_id|Partner|Many2one|res.partner
account.move.line|user_type_id||Many2one|account.account.type
account.move.line|tax_exigible|Appears in VAT report|Boolean|default=True
account.move.line|parent_state||Char|
account.move.line|recompute_tax_line||Boolean|
account.move.line|tax_line_grouping_key||Char|


model|field|String|type|note
-----|-----|------|----|----
account.partial.reconcile|debit_move_id||Many2one|account.move.line
account.partial.reconcile|credit_move_id||Many2one|account.move.line
account.partial.reconcile|amount||Monetary|
account.partial.reconcile|amount_currency|Amount in Currency|Monetary|
account.partial.reconcile|currency_id|Currency|Many2one|res.currency
account.partial.reconcile|company_currency_id|Company|Many2one|res.company
account.partial.reconcile|company_id||Many2one|account.full.reconcile
account.partial.reconcile|full_reconcile_id|Full Reconcile|Many2one|account.full.reconcile
account.partial.reconcile|max_date|Max Date of Matched Lines|Date|readonly=True, copy=False, store=True,


model|field|String|type|note
-----|-----|------|----|----
account.full.reconcile|name|Number|Char|required=True, copy=False
account.full.reconcile|partial_reconcile_ids|Reconciliation Parts|One2many|'account.partial.reconcile', 'full_reconcile_id'
account.full.reconcile|reconciled_line_ids|Matched Journal Items|One2many|'account.move.line', 'full_reconcile_id'
account.full.reconcile|exchange_move_id||Many2one|account.move



